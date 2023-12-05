[ABR](ABR)
```python
class noeud:
	valeur:INT|STRING
	filsGauche:noeud
	filsDroit:noeud
```

prefix : A B D E C F

infixe : D B E A F C

postfix: D E B F C A

niveau A B C D E F

J’empile quand je suis sur le noeud

je dépile quand je doit faire un retour en arrière et je vais au dernier noeud de la pile

j”empile quand je suis sur le noeud je regarde si il a des fils, gauche puis droite, je remonte d’un rang si il ny a pas de fils

## prefixe

```python
def prefixe():
	stack = []
	if noeud not sg or sd:
		return false
	while(noeud):
		print(noeud.data)
		if noeud.sg:
			if noeud.sd:
				stack.add(noeud.sd)
			noeud = noeud.sg
		else if noeud.sd:
			noeud = noeud.sd
		else:
			noeud = stack.last
```

prefixe postfixe infixe → pile(lifo)

par niveau → file(fifo)

# DS1 tout depuis le début

fonctions récursives

```python
def recherche (noeud, val) -> Bool:
	if (noeud == none):
		return false
	if (noeud.data == val):
		return true
	if (noeud.val != val):
		return (recherche(noeud.fg, val) or recheche(noeurd.fd, val))






	else if (noeud.filsGauche != null):
		recherche(noeud.filsGauche, val)
	else if (noeud.filsDroit != null):
		recherche(noeud.filsDroit, val) 
```

``` python 
def inverse (noeud) -> :
	if (noeud == none):
		return
	if (noeud.fg == none and noeud.fd != none):
		return inverse(noeud.fd)
	if (noeud.fg != none and noeud.fd == none):
		return inverse(noeud.fg)
	if (noeud.fg != none and noeud.fd != none):
		swap(noeud.fg, noeud.fd)
		return (inverse(noeud.fg) and inverse(noeud.fd))




def inverse (noeuf):
	if noeud.fg != None or noeud.fd != None:
		swap(noeud.fg, noued.fd)
		inverse(noeud.fd)
		inverse(noeud.fg)


```

```python
def hauteur (noeud, taille) -> int:
	if (noeud == none):
		return hauteur
	taille += 1;
	hauteur(noeud.fg, taille)
	hauteur(noeud.fd, taille)


def hauteur(noeud):
	if noeud == None:
		return -1
	else:
	return 1 + max(hauteur(fg), hauteur(fd))

```

```python
def minimum(noeud) -> int:
	if noeud == None:
		return INFINITY
	else:
		min(minimum(noeud.fg), minimum(noeud.fd), noeud.val)
```

```python
def del_feuille(noeud):
	if noeud.fd == None and noeud.fg == None:
		del noeu
	if noeud.fd != None:
		feuille(noeud.fd)
	else:
		feuille(noeud.fg)
```

