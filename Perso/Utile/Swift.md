- Pour les icônes, utiliser SF symbole 6, c'est une librairie fourni par Apple avec des icônes qui ont des interactions
- Bien, penser à importer les assets de couleur et de logo…
- [Transitions de phases : active, inactive et arrière plan](https://developer.apple.com/tutorials/app-dev-training/responding-to-events) 
- Un seul @main

### Tips

- Si il y a trop d'élément sur dans un VStack autant utiliser **LazyVStack** pour que les éléments soient chargé seulement si ils sont affiché sur l'écran (pareil avec **HStack**)

Elements a prendre en compte lors du [design](design) : 

### Les @

**@main** : point d'entré de l'application (il n'y en a qu'un)

**@State** : pour gérer une variable réactive dans un fichier (local)
**@StateObject** : pour gérer une variable réactive qui sera passer entre plusieurs fichier

**@Published et @ObservableObject** : pour mettre a jour des vue lorsqu'une valeur change mais je n'ai pas encore tout a fait bien compris leur fonctionnement

### Stockage de données dans un fichier
```swift
import Foundation

@MainActor
class ScrumStore: ObservableObject {
    @Published var scrums: [DailyScrum] = []
    
    private static func fileURL() throws -> URL {
        try FileManager.default.url(
            for: .documentDirectory,
            in: .userDomainMask,
            appropriateFor: nil,
            create: false
        )
        .appendingPathComponent("scrums.data")
    }
    
    func load() async throws {
        let task = Task<[DailyScrum], Error> {
            let fileURL = try Self.fileURL()
            guard let data = try? Data(contentsOf: fileURL) else {
                return []
            }
            let dailyScrums = try JSONDecoder().decode([DailyScrum].self, from: data)
            return dailyScrums
        }
        let scrums = try await task.value
        self.scrums = scrums
    }
    
    func save(scrums: [DailyScrum]) async throws {
        let task = Task {
            let data = try JSONEncoder().encode(scrums)
            let outfile = try Self.fileURL()
            try data.write(to: outfile)
        }
        _ = try await task.value
    }
}
```

### NSCache
NSCache stocker des éléments en mémoire pour y accéder plus rapidement
```swift
let imageCache = NSCache<NSString, UIImage>()

func downloadImage(url: URL, completion: @escaping (UIImage?) -> Void) {
    if let cachedImage = imageCache.object(forKey: url.absoluteString as NSString) {
        completion(cachedImage)
    } else {
        DispatchQueue.global().async {
            if let data = try? Data(contentsOf: url), let image = UIImage(data: data) {
                imageCache.setObject(image, forKey: url.absoluteString as NSString)
                DispatchQueue.main.async {
                    completion(image)
                }
            } else {
                DispatchQueue.main.async {
                    completion(nil)
                }
            }
        }
    }
}
```
