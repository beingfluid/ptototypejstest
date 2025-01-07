```js
var Person = Class.create();
Person.prototype = {
    initialize: function(personName) {
        this.personName = personName;
    },
    say: function(message) {
        return this.personName + ': ' + message;
    },
    type: 'Person'
};
```

```js
var Pirate = Class.create();
Pirate.prototype = Object.extendsObject(Person, {
    say: function(message) {
        return this.personName + ':' + message + ', yarr!';
    },
    type: 'Pirate'
});
```

```js
function sumTwoNums(int1, int2) {
    var mySum = int1 + int2;
    gs.info("The sum of " + int1 + " + " + int2 + "= " + mySum);
}
```

```js
var ParentSI = Class.create();
ParentSI.prototype = {
    initialize: function() {
  gs.info("initialize: ParentSI method.");
    },
 parentFunc: function() {
  gs.info("parentFunc: ParentSI method.");
    },
 funcToBeOverriden: function() {
  gs.info("funcToBeOverriden: ParentSI method.");
    },

    type: 'ParentSI'
};
```

```js
var ChildSI = Class.create();
ChildSI.prototype = Object.extendsObject(ParentSI, {

    initialize: function() {
        gs.info("initialize: ChildSI method.");
        ParentSI.prototype.initialize.call(this);
    },

    childFunc: function() {
        gs.info("childFunc: ChildSI method.");
    },
    funcToBeOverriden: function() {
        gs.info("funcToBeOverriden: ChildSI method.");
    },


    type: 'ChildSI'
});
```

```js
var ConstantsSI = Class.create();
ConstantsSI.myConstVar = "myConstVar";
ConstantsSI.prototype = {
    myVar: "myVar",
    initialize: function() {},
    myFunc: function() {
        gs.info("myFunc");
    },

    type: 'ConstantsSI'
};
ConstantsSI.prototype.varFunc = function() {
    gs.info("varFunc");
};
ConstantsSI.constFunc = function() {
    gs.info("constFunc");
};
```

```js
new ConstantsSI().myFunc();

new ConstantsSI().varFunc();

ConstantsSI.constFunc();

gs.info(new ConstantsSI().myVar);

gs.info(ConstantsSI.myConstVar);

