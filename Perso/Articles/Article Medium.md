Vous voulez intégrer une solution d'authentification sécurisé sans avoir à taper aucune ligne de code dans votre application? Pour autoriser un petit nombre d'utilisateur à accéder à votre application, vous pouvez utiliser l'outil Zero Trust de CloudFlare combiné à l'utilisation d'un Worker serverless pour la vérification des token JWT.

Vous avez seulement besoin d'un compte [CloudFlare](https://dash.cloudflare.com/) avec le plan gratuit pour réaliser les prochaines étapes.

Toutes les ressources disponibles se trouveront sur mon [GitHub](https://github.com/TangoCh4rlie)

Premièrement hébergez avec CloudFlare Pages une page web. Utilisez la techno que vous souhaitez mais faites en sorte que votre page ai deux routes. Un "/" et un "/secure". Vous pouvez forker le [projet react](https://github.com/TangoCh4rlie/medium-react-projet) sur mon repo pour avoir la base.

Publiez le simplement en allant sur **Compute (Worker)** > **Workers & Pages** puis "Create". Connectez votre compte Github pour récupérer le répo. Suivez les instructions en fonction du langage utilisé et déployez votre application. Vous devriez avoir une url comme https://[le-nom-de-votre-projet].pages.dev. 

Rendez-vous sur l'onglet **Zero Trust** pour vous créer un nom de team. Une fois que votre espace Zero Trust est créé, retournez sur les paramètre de votre Page. Dans la partie **Générale** activez Access Policy. Cela aura pour but de créer une nouvelle application dans la section **Zero Trust** > **Access** > **Application**. Cliquez sur cette dernière pour modifier les règles. Dans **Overview** vous aurez la possibilité de sélectionner quelle route ou sous domaine est protégé par Zero Trust. Dans notre cas dans **Subdomain** retirez l'étoile et dans **Path** rajoutez "secure". Cela aura pour effet de sécuriser seulement l'access de la route "/secure".

Sauvegardez votre application et rendez vous sur https://[le-nom-de-votre-projet].pages.dev pour vous assurer que tout fonctionne correctement. Normalement vous devriez voir "Welcome. There is no authentication". Si vous vous rendez sur "/secure" vous deviez avoir une page généré par CloudFlare sur laquelle vous devez renseigner un email pour pouvoir continuer. Un code de vérification vous sera envoyé et une fois renseigné vous pourrez poursuivre sur la route "/secure" sur laquelle vous pourrez voir "Wow I feel so safe here".

Par défaut seule l'email du créateur de l'application Zero Trust est autorisé à se connecter et accéder aux pages sécurisé. Si vous souhaitez qu'une autre adresse mail puisse accéder à votre application il vous suffit de retourner sur la configuration de votre application Zero Trust dans l'onglet **Policies**. Sélectionnez "Allow Members - Cloudflare Pages" pour l'éditer, dans **Configure rules** rajoutez dans **Values** l'email de l'utilisateur souhaité.

La première étape de cette article est terminé, nous avons sécurisé une route de notre application mais un acteur malveillant pourrait appeler des endpoints de notre api que nous souhaitons réserver aux utilisateurs authentifiés.

Nous allons instancier un Worker CloudFlare pour nous permettre d'avoir une API.

Pour créer un worker nous allons utiliser la CLI wrangler. Rentrez la commande `npm create cloudflare@latest auth-worker`. Sélectionnez "Hello World example" puis "Hello World Worker" puis "TypeScript". Vous pouvez initialiser un git mais dans notre cas le worker sera déployé à la main. Sélectionnez "No" pour ne pas déployer l'application.

Installez `jose` et `cookie` avec la commande suivante `npm install jose cookie`.

Dans le src/index.ts collez le code suivant que nous allons détailler : 
```ts
import { createRemoteJWKSet, jwtVerify } from 'jose';  
import { parse } from 'cookie';  
  
async function verifyToken(request: Request, env: { POLICY_AUD: string }): Promise<any> {  
  const TEAM_DOMAIN = "https://<team-name>.cloudflareaccess.com";  
  const CERTS_URL = `${TEAM_DOMAIN}/cdn-cgi/access/certs`;  
  const JWKS = createRemoteJWKSet(new URL(CERTS_URL));
  
  const AUD = env.POLICY_AUD;  
  
  const COOKIE_NAME = "CF_Authorization";  
  
  const cookie = parse(request.headers.get("Cookie") || "");  
  const token = cookie[COOKIE_NAME];  
  
  if (!token) {  
   throw new Error('Missing required CF authorization token');  
  }  
  
  try {  
   await jwtVerify(token, JWKS, {  
    issuer: TEAM_DOMAIN,  
    audience: AUD,  
   });  
  } catch (error) {  
   throw new Error('Token verification failed: ' + error);  
  }  
}  
  
export default {  
  async fetch(request: Request, env: { POLICY_AUD: string }): Promise<Response> {  
   try {  
    await verifyToken(request, env);  
    return new Response('Access authorized', { status: 200 });  
   } catch (error) {  
    return new Response('Forbidden' + error, { status: 403 });  
   }  
  },  
};
```

Le code se découpe en deux parties. La première avec le `export default` va être le point d'entré de toute requête sur notre Worker. La deuxième est la méthode nous permettant de vérifier le token passé dans la requête.

Détaillons cette dernière :

- La fonction `createRemoteJWKSet` de la librairie Jose nous permet de configurer le gestionnaire de récupération des clés de notre application d'authentification via CERTS_URL.

- La variable AUD est initialisé avec la valeur d'environnement POLICY_AUD du worker. Il nous faudra la configurer une fois le worker déployé.

- La fonction `parse` de la librairie Cookie nous permet de récupérer les cookies pour vérifier l'authentification de l'expéditeur de la requête. Si il n'y en a pas une Erreur est retournée

- La fonction `jwtVerify` de la librairie Jose nous permet de vérifier la validité du token JWT transmit dans la requête

Déployons ce worker avec la commande `npx wrangler deploy`. Le worker devrait être déployé et accessible sur **Compute (Worker)** > **Workers & Pages**. Configurez la variable d'environnement `POLICY_AUD` dans **Settings** > **Variables and Secrets** de votre worker en ajoutant une variable de type "Secret". Nommez votre variable `POLICY_AUD` et dans **Value** insérez le token AUD que vous trouverez dans **Zero Trust** > **Access** > **Application** > [votre-app] > **Overview** > **Application Configuration**.

Cela aura pour but de redéployer votre worker pour qu'il soit opérationnel. Si vous vous rendez sur https://[worker-name].workers.dev/ vous devriez avoir l'erreur suivante : "ForbiddenError: Missing required CF authorization token"

Si on intègre cet appel à notre application web le cookie sera automatiquement passé et l'authentification au niveau de l'api sera fonctionnelle.

Pour cela rajoutez ce code dans le composant `SecurePage.tsx` votre application web et redéployez la sur CloudFlare Pages en versionnant votre code sur la branche main du projet.

```tsx
import { useEffect, useState } from 'react'

export default function SecurePage() {
	const [state, setState] = useState(null);

	useEffect(() => {
		const sendRequest = async () => {
			const response = await fetch('https://[worker-name].workers.dev');
			setState(await response.json());
		}

		sendRequest()
	}, [])
	return (
		<div>
			<h1>Wow I feel so safe here</h1>
			{state && <p>{state}</p>}
		</div>
	);
}
```







