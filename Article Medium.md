Vous voulez intégrer une solution d'authentification sécurisé sans avoir à taper aucune ligne de code dans votre application? Pour autoriser un petit nombre d'utilisateur à accéder à votre application, vous pouvez utiliser l'outil Zero Trust de CloudFlare combiné à l'utilisation d'un Worker serverless pour la vérification des token JWT.

Vous avez seulement besoin d'un compte [CloudFlare](https://dash.cloudflare.com/) avec le plan gratuit pour réaliser les prochaines étapes.

Toutes les ressources disponibles se trouveront sur mon [GitHub](https://github.com/TangoCh4rlie)

Premièrement hébergez avec CloudFlare Pages une page web. Utilisez la techno que vous souhaitez mais faites en sorte que votre page ai deux routes. Un "/" et un "/secure". Vous pouvez forker le [projet react](https://github.com/TangoCh4rlie/medium-react-projet) sur mon repo pour avoir la base.

Publiez le simplement en allant sur **Compute (Worker)** > **Workers & Pages** and after "Create". Connectez votre compte Github pour récupérer le répo. Suivez les instructions en fonction du langage utilisé et déployez votre application. Vous devriez avoir une url comme https://[le-nom-de-votre-projet].pages.dev. 

Rendez-vous sur l'onglet **Zero Trust** pour vous créer un nom de team. Une fois que votre espace Zero Trust est créé, retournez sur les paramètre de votre Page. Dans la partie **Générale** activez Access Policy. Cela aura pour but de créer une nouvelle application dans la section **Zero Trust** > **Access** > **Application**. Cliquez sur cette dernière pour modifier les règles. Dans **Overview** vous aurez la possibilité de sélectionner quelle route ou sous domaine est protégé par Zero Trust. Dans notre cas dans **Subdomain** retirez l'étoile et dans **Path** rajoutez "secure". Cela aura pour effet de sécuriser seulement l'access de la route "/secure".

Sauvegardez votre application et rendez vous sur https://[le-nom-de-votre-projet].pages.dev pour vous assurer que tout fonctionne correctement. Normalement vous devriez voir "Welcome. There is no authentication". Si vous vous rendez sur "/secure"



