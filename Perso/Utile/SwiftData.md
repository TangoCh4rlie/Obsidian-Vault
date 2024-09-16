Mettre un `@Model` au dessus des classes 

`@Attribute` est utile pour donner des propriétés à donner a la valeur [list](https://developer.apple.com/documentation/swiftdata/schema/attribute/option) 
`#Unique` pour créer des couples de uniques
Ex: 
```swift
@Model
final class Person {
    // Declare any unique constraints as part of the model definition.
    #Unique<Person>([\.id], [\.givenName, \.familyName])


    var id: UUID
    var givenName: String
    var familyName: String


    init(id: UUID, givenName: String, familyName: String) {
        self.id = id
        self.givenName = givenName
        self.familyName = familyName
    }
}
```
****
