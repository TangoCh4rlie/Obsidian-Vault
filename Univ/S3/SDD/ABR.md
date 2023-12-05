```python
def planter(abr, val):
	if bar is None:
		return False
	if val <= noeud:
```

```python
def rechercher(abr,val)
	if abr.est_vide():
		return False
	else:
		temp = abr.racine
		while temp != None:
			if temp.val == val:
				return True
			elif temp.val > val:
				temp = temp.fd
			else:
				temp = temp.fd
		return False