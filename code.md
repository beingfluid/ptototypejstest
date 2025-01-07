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
    testArr: ["ATF", "Jasmine", "ServiceNow"],
    testString: "ATF and Jasmine make ServiceNow testing sweet!",

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

(function(outputs, steps, params, stepResult, assertEqual) {
    // add test script here

    // Basic concepts
    xdescribe('my suite of script tests', function() {
        it('should meet expectations', function() {
            expect(true).not.toBe(false);
        });
    });

    // Matchers
    describe('Calculator', function() {
        it('should initialize the total', function() {
            var calculator = new Calculator();

            expect(calculator.total).toBe(0);
        });

        it('should add numbers to total', function() {
            var calculator = new Calculator();
            calculator.add(5);

            expect(calculator.total).toBe(5);
            // expect(10).toBe(5);
        });
        it('should substract numbers from total', function() {
            var calculator = new Calculator();
            calculator.total = 30;
            calculator.substract(5);

            expect(calculator.total).toBe(25);
        });
        it('should multiply total by number', function() {
            var calculator = new Calculator();
            calculator.total = 100;
            calculator.multiply(2);

            expect(calculator.total).toBe(200);
        });
        xit('should divide total by number', function() {
            var calculator = new Calculator();
            calculator.total = 200;
            calculator.divide(2);

            expect(calculator.total).toBe(100);

            /*
            calculator.divide(0);
            expect(calculator.total).toBe(0);
            */
        });
        it('should deep compare: ex1', function() {
            var calculator = new Calculator();

            var calculator2 = new Calculator();

            expect(calculator).not.toBe(calculator2);
            expect(calculator).toEqual(calculator2);

        });
        it('should deep compare: ex2', function() {
            var calculator = new Calculator();
            calculator.total = 200;

            var calculator2 = new Calculator();

            expect(calculator).not.toEqual(calculator2);

        });

        it('should test toBeTruthy/toBeFalsy', function() {
            var calculator = new Calculator();

            expect(calculator).toBeTruthy();
            expect(calculator.total).toBeFalsy();

        });
        it('should test toBeDefined/toBeUndefined', function() {
            var calculator = new Calculator();

            expect(calculator.add).toBeDefined();
            expect(calculator.add).not.toBeUndefined();

        });
        it('should test toBeNull', function() {
            var calculator = new Calculator();
            calculator.total = null;

            expect(calculator.total).toBeNull();

        });
        it('should test toContain', function() {
            var calculator = new Calculator();

            expect(calculator.testArr).toContain("Jasmine");
            expect(calculator.testString).toContain("Jasmine");

        });
        it('should test toBeNaN', function() {
            var calculator = new Calculator();
            calculator.total = 3;
            calculator.multiply("a");

            expect(calculator.total).toBeNaN();

        });
        it('should test toThrow/toThrowError', function() {
            var calculator = new Calculator();
            calculator.total = 3;

            expect(function() {
                calculator.divide(0);
            }).toThrow();

            expect(function() {
                calculator.divide(0);
            }).toThrowError(Error);

            expect(function() {
                calculator.divide(0);
            }).toThrowError(Error, "Can not divide by Zero.");

        });
        it('should test toMatch/anything', function() {
            var calculator = new Calculator();
            calculator.total = 50;

            expect(calculator.add(20)).toBe(70);
            expect(calculator.total).toMatch(/-?\d+/);
            expect(typeof(calculator.total)).toMatch("number");

            expect(typeof(calculator.total)).toEqual(jasmine.anything());

        });
    });

})(outputs, steps, params, stepResult, assertEqual);
// uncomment the next line to execute this script as a jasmine test
jasmine.getEnv().execute();
```

```js

(function(outputs, steps, params, stepResult, assertEqual) {
    // add test script here

    // Matchers
    describe('Calculator', function() {

        beforeAll(function() {
            // Runs once before all tests
            gs.info('Starting Calculator test suite.');
        });

        afterAll(function() {
            // Runs once after all tests
            gs.info('Finished Calculator test suite.');
        });

        // var calculator;

        beforeEach(function() {
            // Runs before each tests
            gs.info('Creating a new Calculator instance: Test started.');
            this.calculator = new Calculator();
        });

        afterEach(function() {
            // Runs after each tests
            gs.info('Test finished.');
        });

        it('should add numbers to total', function() {

            this.calculator.add(5);

            expect(this.calculator.total).toBe(5);
            // expect(10).toBe(5);
        });
        it('should substract numbers from total', function() {

            this.calculator.total = 30;
            this.calculator.substract(5);

            expect(this.calculator.total).toBe(25);
        });
        it('should multiply total by number', function() {

            this.calculator.total = 100;
            this.calculator.multiply(2);

            expect(this.calculator.total).toBe(200);
        });
        it('should divide total by number', function() {

            this.calculator.total = 200;
            this.calculator.divide(2);

            expect(this.calculator.total).toBe(100);

        });
        xit('test should be failed', function() {

            fail("Test is failed");

        });

        xit('test should be peding', function() {

            pending("Test is peding");

        });

        it('validates expression: ex1', function() {

            spyOn(this.calculator, 'updateResult').and.stub();

            this.calculator.calculate("a+3");

            expect(this.calculator.updateResult).toHaveBeenCalled();

            expect(this.calculator.updateResult).toHaveBeenCalledTimes(1);

            expect(this.calculator.updateResult).toHaveBeenCalledWith("Operation not recognized");

        });

        it('validates expression: ex2', function() {

            var spy = spyOn(this.calculator, 'updateResult').and.stub();

            this.calculator.calculate("a+3");

            expect(spy).toHaveBeenCalled();

            expect(spy).toHaveBeenCalledTimes(1);

            expect(spy).toHaveBeenCalledWith("Operation not recognized");

        });

        it('validates that the add function: ex1', function() {

            spyOn(this.calculator, 'add').and.callThrough();
            spyOn(this.calculator, 'updateResult').and.stub();

            this.calculator.calculate("1+3");

            expect(this.calculator.updateResult).toHaveBeenCalledWith(4);

        });

        it('validates that the add function: ex2', function() {

            spyOn(this.calculator, 'add').and.callFake(function() {
                return 4;
            });
            spyOn(this.calculator, 'updateResult').and.stub();

            this.calculator.calculate("1+3");

            expect(this.calculator.updateResult).toHaveBeenCalledWith(4);

        });

        it('validates that the add function: ex3', function() {

            spyOn(this.calculator, 'add').and.returnValue(4);

            spyOn(this.calculator, 'updateResult').and.stub();

            this.calculator.calculate("1+3");

            expect(this.calculator.updateResult).toHaveBeenCalledWith(4);

        });

        it('validates that the add function: ex4', function() {

            spyOn(this.calculator, 'add').and.returnValues(1, 4);

            spyOn(this.calculator, 'updateResult').and.stub();

            this.calculator.calculate("1+3");

            expect(this.calculator.updateResult).toHaveBeenCalledWith(4);

        });

        it('tests throwError', function() {

            spyOn(this.calculator, 'add').and.throwError("Test Error");

            var self = this; // To ensure the correct context
            expect(function() {
                self.calculator.calculate("1+3");
            }).toThrowError("Test Error");

        });


    });

})(outputs, steps, params, stepResult, assertEqual);
// uncomment the next line to execute this script as a jasmine test
jasmine.getEnv().execute();
```

```js

```

```js

```

```js

```
