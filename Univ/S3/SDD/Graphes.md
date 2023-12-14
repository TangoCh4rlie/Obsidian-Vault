```python
def composante_connexe_orienté(graphe): 
	nb_comp = 0 
	temp = graphe.entre 
	while(True): 
		while(temp != None and (temp.ariv == None or temp.dep == None)): 
			nb_comp += 1 
			current = temp.ls 
			temp.dep = True # PLUS 
			while(current != None): 
				marque_ariv(graphe,current.val) # MOINS 
				current = current.next 
			temp = temp.next 
		if(temp == None): 
			break 
	return nb_comp 

def marque_ariv(graphe,nd): 
	temp = graphe.entree 
	while(temp != None and temp != nd.val): 
		temp = temp.next 
	temp.ariv = True