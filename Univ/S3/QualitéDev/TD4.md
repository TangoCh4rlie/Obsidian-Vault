Singleton
private static Singleton singleton

private Singleton() {
	singleton = db connection
}

getInstance() {
	if singleton == null {
		singleton = new Stingleton()
	} 
		return singleton
}