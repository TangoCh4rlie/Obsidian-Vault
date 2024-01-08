Singleton
private static **volatile** Singleton singleton

private Singleton() {
	singleton = db connection
}

public static **synchronized** getInstance() {
	if singleton == null {
		singleton = new Stingleton()
	} 
		return singleton
}

interdir le clonage 

protected Singleton clone() throws CloneNotSupportedException{
	throw new CloneNotSupportedException();
		return (Singleton) super clone()
}

### EXO
[[EXO-TD4]]

quand ya une modif originator.saf() et history.push() (dans le caretaker)

**Organisator**
enregistre 
**ConcreteMemento**
**Caretaker**
