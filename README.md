> Currently unmaintained since I have moved from Microfocus Service Manager to ServiceNow - Sorry guys!

# servicemanager-classier

This class extending engine is a fork from https://github.com/ironboy/classier.

It includes only the required changes to make it work inside the service manager.

A detailed description how this engine works is available here: https://classier.cloudeducation.se/


# Limitations

* You have to define the `_class` variable, because the service manager has no DOM or something else which is required to use the existing functionality from the classier engine

* The definition of private and protected variables has no effect. It's always possible to access private & protected variables - The reason for this is the old javascript version.

# Real Life Example

* https://github.com/noxify/servicemanager-table-builder

# Simple Example

## ScriptLibrary: Animal

```js
var classier = system.library.classier.getClass();

var Animal = classier.$extend({

    _class : "Animal",

    __init__ : function(name, age) {
        this.name = name;
        this.age = age;
    },

    health: 100,
    _secret: "I'm always hungry.",
    __extraSecret: "I'm scared of humans.",

      // as well as methods
    die : function() {
        this.health = 0;
    },

    eat : function(what) {
        this.health += 5;
    },

    tellSecret : function() {
        return this._secret;
    },

    tellExtraSecret : function() {
        return this.__extraSecret;
    }

});

var Tiger = Animal.$extend({

    _class : "Tiger",

    eat : function(animal) {
        this.$super(animal);
        animal.die();
    }
});

var Sheep = Animal.$extend({

    _class : "Sheep",

    __init__ : function(name, age, shorn) {
        this.$super(name, age);
        this.shorn = shorn;
    }

});

function getClass() {
	return {
		'animal' : Animal,
		'tiger' : Tiger,
		'sheep' : Sheep
	};
}
```

## ScriptLibrary: AnimalTest

```js
var Animals = system.library.Animal.getClass();
var Animal = Animals['animal'];
var Tiger = Animals['tiger'];
var Sheep = Animals['sheep'];

var Anni = new Animal('Anni', 5);
var Leo = new Tiger('Leo',3);
var Molly = new Sheep('Molly', 1);

/*
print(Anni.name+" age: "+Anni.age) // => Anni age: 5;
print(Leo.name+" age: "+Leo.age); // => Leo age: 3
print(Molly.name+" age: "+Molly.age); // => Molly age: 1
*/

/*
print(Anni instanceof Animal); // => true
print(Anni instanceof Tiger); // => false
print(Anni instanceof Sheep); // => false
*/

/*
print(Leo instanceof Animal); // => true
print(Leo instanceof Tiger); // => true
print(Leo instanceof Sheep); // => false
*/

/*
print(Molly instanceof Animal); // => true
print(Molly instanceof Tiger); // => false
print(Molly instanceof Sheep); // => true
*/

/*
Leo.eat(Molly);
print("Leo health: "+Leo.health); // => 105
print("Molly health: "+Molly.health); // => 0
*/
```
