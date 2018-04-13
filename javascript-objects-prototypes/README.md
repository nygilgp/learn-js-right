# Learning JS Objects

## Creating JS Objects
*   Using Object Literals {}
```javascript
'use strict';
var dog = {
    name: 'tiger',
    color: 'balck & brown'
};
dog.age = 4;
dog.speak = function() {
    console.log('bow');
}
console.log(dog.name);
dog.speak();
```

*   Using new keyword or the constructor patter
```javascript
function Cat(name, color) {
    this.name = name;
    this.color = color
}
var cat = new Cat('Jack', 'white');
console.log(cat.name);
```

*   `this` keyword
    -   this refers to the current object that is executing the current bit of code

```javascript
function Cat() {
    //this.name = 'Jack'; // we have commented out name, as name will affect the window property
    this.color = 'white';
}
var cat = Cat();
console.log(cat); // undefined
console.log(window.color); // white, this will set it to window object when initialized 
```

*   Using Object.create
```javascript
var cat = Object.create(Object.prototype, {
	name: {
		value: 'fluffy'
	},
	color: {
		value: 'borwn'
	}
});
console.log(cat.color);
```

* ES6 class way

```javascript
'use strict';
class Cat{
    constructor(name, color){
        this.name = name;
        this.color = color;
    }

    speak() {
        console.log('Meow');
    }
}

let cat = new Cat('fluffy', 'black');
console.log(cat.speak());
```



## JS Object properties
*   Using square brakets to access properties is also possible
```javascript
'use strict';
var dog = {
    name: 'tiger',
    color: 'balck & brown',
    'eye color': 'gold'
};
console.log(dog['eye color']);
```

* See object properties
    -   Object.getOwnPropertyDescriptor(dog, 'name') //per property
    -   Object.getOwnPropertyDescriptors(dog) //for all
```javascript
'use strict';
var dog = {
    name: 'tiger',
    color: 'balck & brown'
};
console.log(Object.getOwnPropertyDescriptor(dog, 'name'));
/*
{value: "tiger", writable: true, enumerable: true, configurable: true}
*/
```

* writable object property
    -   writable propery has only access to its object value, not to the subsiquent levels
    -   for example if an object value is another object, we can overright the child value, even though the parent is set as writable false
    -   to avoid that we can use Object.freeze(dog.name) to avoid overright of children as well

```javascript
'use strict';
var dog = {
    name: {fname: 'bull', lname: 'buck'},
    color: 'balck & brown'
};

Object.defineProperty(dog, 'name', {writable: false});
dog.name.fname = 'blacky';
console.log(Object.getOwnPropertyDescriptor(dog, 'name'));
/*
value
:
{fname: "blacky", lname: "buck"}
writable
:
false
*/
```

```javascript
'use strict';
var dog = {
    name: {fname: 'bull', lname: 'buck'},
    color: 'balck & brown'
};

Object.defineProperty(dog, 'name', {writable: false});
Object.freeze(dog.name);
dog.name.fname = 'blacky';
console.log(Object.getOwnPropertyDescriptor(dog, 'name'));
/*
Uncaught TypeError: Cannot assign to read only property 'fname' of object '#<Object>'
*/
```


* enumerable object property
    -   enumerable propery helps in avoiding property being leaked into loops like for...in, Object.keys(dog), etc
    -   also avoided in JSON.stringify(dog)
    -   it doesn't affect the viewability of the propery, so you can access it via . or []
```javascript
'use strict';
var dog = {
    name: {fname: 'bull', lname: 'buck'},
    color: 'balck & brown'
};
dog.speak = function() {
    console.log('bow');
}
Object.defineProperty(dog, 'speak', {enumerable: false});

for(var propertyName in dog) {
    console.log(propertyName);
}
```


* configurable object property
    -   Locks properties (enumerable, configurable) from being changed later 
    -   writable property of the object can be changed
    -   delete dog.name will also be blocked

```javascript
'use strict';
var dog = {
    name: {fname: 'bull', lname: 'buck'},
    color: 'balck & brown'
};
Object.defineProperty(dog, 'name', {configurable: false});
Object.defineProperty(dog, 'name', {writable: true}); // works
Object.defineProperty(dog, 'name', {configurable: true}); // fails
delete dog.name; // fails
```

* getters and setters

```javascript
'use strict';
var dog = {
    name: {fname: 'bull', lname: 'buck'},
    color: 'balck & brown'
};
Object.defineProperty(dog, 'fullname', {
    get: function() {
        return this.name.fname + ' ' + this.name.lname;
    },
    set: function(value) {
        var nameParts = value.split(' ');
        this.name.fname = nameParts[0];
        this.name.lname = nameParts[1];
    }
});
dog.fullname = 'black buck';
console.log(dog.fullname);
```


## JS Object 
*   Using square brakets to access properties is also possible
```javascript
'use strict';
var dog = {
    name: 'tiger',
    color: 'balck & brown',
    'eye color': 'gold'
};
console.log(dog['eye color']);
```




*   Using new keyword
```javascript

```