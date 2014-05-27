## TEHTÄVÄ 4 - OLIOT JA PERIYTYMINEN

#### Vastauksia

1. Miten JavaScriptillä voidaan toteuttaa olio-ohjelmointia?

```js
function Person() { }
var person1 = new Person();
var person2 = new Person();

```

2. Kuinka periytyminen toteutetaan JavaScriptissä?

First, we will make a Parenizor class that will have set and get methods for its value, and a toString method that will wrap the value in parens.

```js

function Parenizor(value) {
    this.setValue(value);
}

Parenizor.method('setValue', function (value) {
    this.value = value;
    return this;
});

Parenizor.method('getValue', function () {
    return this.value;
});

Parenizor.method('toString', function () {
    return '(' + this.getValue() + ')';
});
```


The syntax is a little unusual, but it is easy to recognize the classical pattern in it. The method method takes a method name and a function, adding them to the class as a public method.

So now we can write

```js

myParenizor = new Parenizor(0);
myString = myParenizor.toString();
```

As you would expect, myString is "(0)".

Now we will make another class which will inherit from Parenizor, which is the same except that its toString method will produce "-0-" if the value is zero or empty.

```js

function ZParenizor(value) {
    this.setValue(value);
}

ZParenizor.inherits(Parenizor);

ZParenizor.method('toString', function () {
    if (this.getValue()) {
        return this.uber('toString');
    }
    return "-0-";
});
```

The inherits method is similar to Java's extends. The uber method is similar to Java's super. It lets a method call a method of the parent class. (The names have been changed to avoid reserved word restrictions.)

So now we can write

```js

myZParenizor = new ZParenizor(0);
myString = myZParenizor.toString();
This time, myString is "-0-".
```

JavaScript does not have classes, but we can program as though it does.


