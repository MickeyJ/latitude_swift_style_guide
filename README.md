Swift Style Guide
=================

### Prefer ```let``` over ```var```

Only use ```var``` when you know the value will change.

### Return Early

Instead of:
```js
if thing.isTrue {
    // do stuff
} else {
    return
}
``` 

Use:
```js
guard thing.isTrue else {
    return
}

// do stuff
``` 

### Use ```guard``` Over ```if```

Instead of:
```js
if !box.isChecked {
    box.isChecked = true
} else {
    box.isChecked = false
}
```

Use:
```js
guard !box.isChecked else {
    box.isChecked = false
    return
}
    
box.isChecked = true
```

### Avoid Force-Unwrapping Optionals

Instead of:
```js
let thing = stuff.getThing(id) as! MyThing

thing.doStuff()
``` 

Use:
```js
if let thing = stuff.getThing(id) as? MyThing {
    thing.doStuff()
} else {
    stuff.makeThing()
}
```

Or:
```js
guard let thing = stuff.getThing(id) as? MyThing else {
    stuff.makeThing()
    return
}

thing.doStuff()

``` 

### Only Specify ```self``` If Necessary

Instead of:
```js
class MyThing {
    private var id: Int!
    
    func changeThingID(newID: Int){
        self.id = newID
    }
}
```

Use:
```js
class MyThing {
    private var id: Int!
    
    func changeID(newID: Int){
        id = newID
    }
}
```

Necessary when parameter names conflict:
```js
class MyThing {
    private var id: Int!
    private var stuff: String!

    init(id: Int, stuff: String){
        self.id = id
        self.stuff = stuff
    }
}
```

Necessary in a closure:
```js
class MyThing {
    private var id: Int!
    private var stuff: String!
    
    func doStuff(){
        DataSource.getStuff(id, then:{ betterStuff in
            self.stuff = betterStuff
        })
    }
}
```


