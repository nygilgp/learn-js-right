#   JS Design Patterns

**What is the problem we are going to solve, and here is the design pattern for it**
*   Gang of Four
*   It solves a problem
*   It is a proven concept
*   The solution is not obvious
*   It describes a relationship(9/10)
*   It has significant human component

## Creational
-   Creating new objects
-   Adapting creation to the situation
-   Constructor
-   Module
-   Factory
-   Singleton

### Constructor
    -   Prototype => an encapsulation of properties that an object link to
    -   ClassName.prototype.methodName = function(arguments) {}
    -   In below script, the use of prototype function save is more efficient than complete, because every time a new object for Task is created a single copy of save is pointed with prototype, where as complete will be replicated in each object. 
    -   You can use ES6 class method also to obrain the same result
```Javascript
'use strict';

var Task = function(name) {
    this.name = name;
    this.completed = false;

    this.complete = function() {
        console.log('Task completed '+ this.name);
        this.completed = true
    }
}

Task.prototype.save = function() {
    console.log('Task saved ' + this.name);
}

var task1 = new Task('Task to create a blog');
var task2 = new Task('Task to create a document');
```

### Module
    -   Simple way to encapsulate methods
    -   Create a "Toolbox" of functions to use, eg:- functions for DB calls, like connect, reterive, etc.
```Javascript
var Module = {
    method: function(){ ... },
    otherMethod: function() { ... }
}
// calls like below can be achived 
Module.method();
```
    -   Now if we wrap it in function, private variables can be supported. ie a ##closure## 
```Javascript
var Module = function(){
    var privateVariable = 'I am private...';
    var db = {}
    return {
        method: function(){ ... },
        otherMethod: function() { ... }
    }
}
// calls like below can be achived 
Module.method();
```    
    -   A modification of this pattern is revealing module pattern
    -   Advantage is that it looks documented, by having a simple listing of 
```Javascript
var Module = function(){
    var privateVariable = 'I am private...';
    var db = {} // can be used only inside this module
    var method = function(){ ... }
    var otherMethod = function(){ ... }
    return {
        method: method,
        otherMethod: otherMethod
    }
}
module.export = Module(); // so it will have what ever in the return executed and ready to be used

// calls like below can be achived in the required js file
Module.method();
```   

### Factory 
    -   pattern for simplify object creation
    -   creating different objects based on need
    -   Repository creation 
    -   possible to add caching 

### Singleton
    -   restricts an object to a one instance of that object across the application
    -   remembers the last time you used it
    -   hands the same instance back
    -   To achive singleton in nodejs either of the below
        --  module.export = repo();
        --  modeul.export = new repo;

```Javascript
'use script';

var TaskRepo = (function(){
    var taskRepo;
    function createTaskRepo() {
        var taskRepo = new Object('Task');
        return taskRepo;
    }
    function gentInstance() {
        if(!taskRepo) {
            taskRepo = createTaskRepo();
        }
        return taskRepo;
    }
    return {
        gentInstance: gentInstance
    }
})();

var repo1 = TaskRepo.gentInstance();
var repo2 = TaskRepo.gentInstance();

if(repo1 === repo2) {
    console.log('same');
}
```

**Difference with constructor**, is that here in Module we only need to new this object once or never as we just use the functions inside it.

## Structural
-   Makeup of the actual objects themselfs
-   Concerned with how objects are made up and simplify relationship between objects
    --  Extend functionality
    --  Simplify functionality
-   Facade
-   Decorator
-   Flyweight

### Decorator
    -   Use to add new functionality to an existing object, without being obtrucsive
    -   complete inheritance
    -   wraps the object
    -   protects existing object
    -   allows extended functionality

```Javascript
'use strict';

var Task = function(name) {
    this.name = name;
    this.completed = false;
}

Task.prototype.complete = function() {
    console.log('Task completed '+ this.name);
    this.completed = true
}
Task.prototype.save = function() {
    console.log('Task saved ' + this.name);
}

var task1 = new Task('Task to create a blog');

var urgentTask = new Task('urgent task');
// decoration, with a new method
urgentTask.notify = function() {
    console.log('notify important people');
}

urgentTask.complete();
// decoration happens, without affecting the Task save
urgentTask.save = function() {
    this.notify();
    Task.prototype.save.call(this);
}
urgentTask.save()

```   

**more clean** way of doing decoration, with extending functionality 

```Javascript
'use strict';

var Task = function(name) {
    this.name = name;
    this.completed = false;
}

Task.prototype.complete = function() {
    console.log('Task completed '+ this.name);
    this.completed = true
}
Task.prototype.save = function() {
    console.log('Task saved ' + this.name);
}

var task1 = new Task('Task to create a blog');
task1.complete();
task1.save();

var urgentTask = function(name, priority) {
    Task.call(this, name);// calling parent constructor 
    this.priority = priority;
}
// this line will complete the inheritance
urgentTask.prototype = Object.create(Task.prototype);

// decoration, with a new method
urgentTask.prototype.notify = function() {
    console.log('notify important people');
}

// decoration happens, without affecting the Task save
urgentTask.prototype.save = function() {
    this.notify();
    Task.prototype.save.call(this);
}
var ut = new urgentTask('urgent task', 1);
ut.complete();
ut.save();
console.log(ut);
```      

### Facade 
*   used to provide a simplified interface to a complicated system
*   jQuery is well know facade for simplifying the DOM object manipulation


### Flyweight
*   Conserves memory by sharing portions of an object between objects.
    -   Like prototypes
*   Results in a smaller memory footprint
*   But only if you have larger number of objects 


## Behavioral 
-   How objects relate to each other, how they operate
-   Concerned with the assignment of responsibilities between objects and how they communicate
    --  Deals with the responsibilities of objects
    --  Help objects cooperate
    --  Assign clear hierarchy
    --  Can encapsulate requests
-   Command
-   Observer
-   Mediator

### Observer
*   Allows a collection of objects to watch an object and be notified of changes.
    -   allows for loosly coupled system
    -   one object is the focal point
    -   group of object watch for changes
    



