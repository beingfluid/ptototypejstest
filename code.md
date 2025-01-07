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

```

```js
var Calculator = Class.create();
Calculator.prototype = {
    initialize: function() {
        this.total = 0;
    },

    calculate: function(inputValue) {
        const expression = /\+|\-|\*|\//;
        const numbers = inputValue.split(expression);

        const numberA = parseInt(numbers[0]);
        const numberB = parseInt(numbers[1]);

        const operation = inputValue.match(expression);

        if (Number.isNaN(numberA) || Number.isNaN(numberB) || operation == null) {
            this.updateResult("Operation not recognized");
            return;
        }

        this.add(numberA);

        let result;

        switch (operation[0]) {
            case "+":
                result = this.add(numberB);
                break;
            case "-":
                result = this.substract(numberB);
                break;
            case "*":
                result = this.multiply(numberB);
                break;
            case "/":
                result = this.divide(numberB);
                break;
        }

        this.updateResult(result);
    },

    updateResult: function(result) {
        gs.info("result: " + result);
    },


    add: function(number) {
        return (this.total += number);
    },

    substract: function(number) {
        return (this.total -= number);
    },

    multiply: function(number) {
        return (this.total *= number);
    },

    divide: function(number) {
        if (number === 0) {
            throw new Error("Can not divide by Zero.");
        }
        return (this.total /= number);
    },

    type: 'Calculator'
};
```

```js

```

```js

```

```js

```

```js

```

```js

```
