Les matrices renvoyé par jordan() renvoie les matrice P et D

![[Pasted image 20241209162729.png]]

on en déduit que les racines sont 2 d'ordre 1 et 2 d'ordre 1

une base associé au sous espace propre de valeur 2 est {1,2,1}

![[Pasted image 20241209162816.png]]

![[Pasted image 20241209162854.png]]

On pouvait voir a l'aide de la commande jrodan ou bien en claculant le pol car et en déterminant ses racines que : 
- Les valeurs propres de A sont : 1 d'ordre 2 et 2 d'ordre 1
- Le polynome car est scindé (on le vois avec jordan par ce qu'il n'y a que des racines réeles)

*si xcas ne renvoie pas une matrice avec que des chiffres dans la diag on ne peut pas en déduire qu'elle n'est pas diagonalisable **il faut le prouver***

avec jordan on obtient directement un base du sep associé a la val propre 2 est {(1,2,1)} et une base du sous espace propre associé a la valeur propre de 1 : {(2,0,1), (0,2,1)} 

*que je peux retrouver en faisant :* 
![[Pasted image 20241209163744.png]]

On doit retomber sur A quand on fait 
$$
P*D*inv(P)
$$
![[Pasted image 20241209164420.png]]
------------------------------------------------------------------------------------------------
On obtiens un polynome caractéristique sous la forme factorisé
$$
(x-2 )(x-1)^3
$$
Les valeurs propres de A5 sont: 1 d'ordre 3 et 2 d'ordre 1
le plynome carac est scindé`

une base de e2 est : {(1,0,-2,-1)}
une base de e1 est : {(-1,0,0,-2),...}
![[Pasted image 20241209165205.png]]
Jordan renvoie une matrice inversible puisque 
$$
det(P5) = -1
$$
telles que 
$$
A = PDP^(-1)
$$
![[Pasted image 20241209165642.png]]------------------------------------------------------------------------------------------------
*si il y a des termes complexe sur la diagonalisable alors ce n'est pas diagonalisable sur R*

Xcas founit une matruce P et une matrice D mais étant donné quelles dépendant de a (qui pour xcas, n'est pas un réel), nous ne sommes pas sûrs que P est inversible
Il faut donc déterminer les cas pour lesquelles cette matrice P est inversible

$$
solve(det(P)=0, a)
$$
Pour a différent de -1 et 0 la matrice P fournie par Jordan est inversible et on alors bien P inversible et D diagonale telles que A=PDP^(-1)
DONC dans ces cas la, A est diagonalisable 

on va etdier les cas pour a = -1 et a = 0
$$
jordan(A(-1))
$$
le fait que xcas ne renvoie pas de matrice diagonale nous laisse penser  que A(-1) n'est pas diagonalisable MAIS IL FAUT LE MONTRER
Les valeurs propres sont 1 d'ordre 3
$$
dim(tran(ker(A(-1)-1))) = 2
$$
ainsi dim(E(-1))=2 != 3 donc pour a=-1, A n'est pas diagonalisable

$$
jordan(A(0))
$$
$$
dim(tran(ker(A(-1)-1))) = 2
$$
0 est valeur propre d'ordre 3 et dim(E0)=2 != 3 donc pour a = 0, A n'est pas diagonalisable

------------------------------------------------------------------------
![[Pasted image 20241209175607.png]]
![[Pasted image 20241209175622.png]]

Pour a différent de 0,1/2 et 1, P est inversible et on alors
P inversible et D diagonalisable telles que A=PDP^(-1) donc dans ces cas, A est inversible
il reste a étudier les 3 cas chiants

0 est une une valeur propre de multiplicité (ordre) 3 et dim(e0)=2 != 3 donc A n'est pas diagonalisable pour a=0

on a bien P inversivble et D diagonale tel que A=PDP^(-1) donc a est diagonalisable pour a=1

1 est une une valeur propre de multiplicité (ordre) 2 et dim(e1)=1 != 2 donc A n'est pas diagonalisable pour a=1/2

FINALEMENT A est diagonalisable pour a appartenant a IR-{0,1/2}



![[Pasted image 20241209175957.png]]
On a M=PDP^(-1) donc M^n=PD^nP^(-1)
**matpow** set a élever une matrice a la puissance n

[Ma session XCAS](https://xcas.univ-grenoble-alpes.fr/xcasjs/#exec&python=1&radian=1&cas=0,0,M%3A%3Dmatrix(3%2C3%2C%5B1%2C1%2C1%2C0%2C1%2C0%2C1%2C0%2C1%5D)&cas=0,200,P%2CD%3A%3Djordan(M)&cas=0,400,Dn%3A%3Ddiag(0%2C2%5En%2C1)&cas=400,0,matpow(M%2C%20assume(n%3E0)))