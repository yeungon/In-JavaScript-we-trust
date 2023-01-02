In JS we trust - The best way to learn is by building/coding and teaching. I create the challenges to help my friends learn JavaScript and in return it helps me embrace the language in much deeper level. Feel free to clone, fork and pull.

---

###### 1. What's the output?

```javascript
function a(x) {
  x++;
  return function () {
    console.log(++x);
  };
}

a(1)();
a(1)();
a(1)();

let x = a(1);
x();
x();
x();
```

- A: `1, 2, 3` and `1, 2, 3`
- B: `3, 3, 3` and `3, 4, 5`
- C: `3, 3, 3` and `1, 2, 3`
- D: `1, 2, 3` and `3, 3, 3`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

This question revisits closure - one of the most confusing concepts in JavaScript. Closure allows us to create a `stateful function` and such a function can access to the variable outside of its scope. In a nutshell, a closure can have access to the `global` variable (scope), `father function` scope and `its` own scope.

We have here, the only one correct answer, 3, 3, 3 and 3, 4, 5 because first we simply call the function `a()`. It works like a normal function and we have not seen anything so-called `stateful` yet. In the following code, we declare a variable `x` and it stores the value of function `a(1)`, that is why we get 3. 4. 5 rather than 3, 3, 3.

This kind of gotcha gives me the feeling of `static` variable in PHP world.

</p>
</details>

---

###### 2. What's the output?

```javascript
function Name(a, b) {
  this.a = a;
  this.b = b;
}

const me = Name("Vuong", "Nguyen");

console.log(!(a.length - window.a.length));
```

- A: `undefined`
- B: `NaN`
- C: `true`
- D: `false`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

We get true in the console. The tricky part is when we create an object from the constructor function Name but we DO NOT USE `new` keywork. That makes the variable `a` global one and get the value "Vuong". Remember that it is actually a property of the global object `window` (in the browser) or `global` in the nodejs.

We then get `a.length` ~ 5 and `window.a.length` ~ 5 which return 0. !0 returns true.

Imagine what would happen when we create the instance `me` with the `new` keywork. That is an interesting inquire!

</p>
</details>

---

###### 3. What's the output?

```javascript
const x = function (...x) {
  let k = (typeof x).length;
  let y = () => "freetut".length;
  let z = { y: y };

  return k - z.y();
};

console.log(Boolean(x()));
```

- A: `true`
- B: 1
- C: -1
- D: `false`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The spread operator `...x` might help us obtain the parameter in the function in the form of array. Yet, in Javascript the typeof array return "object" rather than "array". It is totally odd if you are coming from PHP.

That is said, we now have the length of the string `object` which returns 6. z.y() simply returns the length of the string 'freetut' (7).

Be aware that the function x() (in the form of `function express` or `anonymous function` (if you are coming from PHP) return -1 when being called and when converted to bool with `Boolean(-1)` return true instead of false. Noted that `Boolean(0)` return false.

</p>
</details>

---

###### 4. What's the output?

```javascript
(function js(x) {
  const y = (j) => j * x;

  console.log(y(s()));

  function s() {
    return j();
  }

  function j() {
    return x ** x;
  }
})(3);
```

- A: `undefined`
- B: 18
- C: 81
- D: 12

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The function `js()` can be automatically executed without calling it and known as IIFE (Immediately Invoked Function Expression). Noted the parameter `x` of the function `js` is actuallly passed with the value 3.

The value return of the function is y(s())), meaning calling three other functions `y()`, `s()` and `j()` because the function `s()` returns `j()`.

j() returns 3^3 = 27 so that s() returns 27.

y(s()) means y(27) which returns 27\*3 = 81.

Note that we can call `declare function` BEFORE the function is actually declared but not with `expression function`.

</p>
</details>

---

###### 5. What's the output?

```javascript
var tip = 100;

(function () {
  console.log("I have $" + husband());

  function wife() {
    return tip * 2;
  }

  function husband() {
    return wife() / 2;
  }

  var tip = 10;
})();
```

- A: "I have \$10";
- B: "I have \$100";
- C: "I have \$50";
- D: "I have \$NaN";

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

We have here an IIFE (Immediately Invoked Function Expression). It means we do not have to call it but it will be excuted automatically when declared. The flow is as: husband() returns wife()/2 and wife() returns tip\*2.

We might think that tip = 100 because it is a global variable when declaring with `var` keyword. However, it is actually `undefined` because we also have `var tip = 10` INSIDE the function. As the variable `tip` is hoisted with default value `undefined`, the final result would be D. We know that `undefined` returns NaN when we try to divide to 2 or multiple with 2.

If we do not re-declare `var tip = 10;` at the end of the function, we will definately get B.

JS is fun, right?

</p>
</details>

---

###### 6. What's the output?

```javascript
const js = { language: "loosely type", label: "difficult" };

const edu = { ...js, level: "PhD" };

const newbie = edu;

delete edu.language;

console.log(Object.keys(newbie).length);
```

- A: 2;
- B: 3;
- C: 4;
- D: 5;

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

This challenge revises the ES6's feature regarding `spread operator ...` Spread operator is quite useful for retrieving parameter in function, to `unite` or `combine` object and array in JavaScript. PHP also has this feature.

In the variable `edu`, we use `...js` (spread operator here) to combine both objects into one. It works in the same way with array.

Then we declare another variable named `newbie`. IMPORTANT note: By declaring the variable like that, both variables point to the SAME POSITION in the memory. We may have known something like `$a = &$b` in PHP, which let both varibles work in the same way. We might have known about `pass by reference` in the case.

Then we have 2 as `edu.language` is deleted. Both objects now have only two elements.

Now is time to think about coping an object in JS either shallow or deep one.

</p>
</details>

---

###### 7. What's the output?

```javascript
var candidate = {
  name: "Vuong",
  age: 30,
};

var job = {
  frontend: "Vuejs or Reactjs",
  backend: "PHP and Laravel",
  city: "Auckland",
};

class Combine {
  static get() {
    return Object.assign(candidate, job);
  }

  static count() {
    return Object.keys(this.get()).length;
  }
}

console.log(Combine.count());
```

- A: 5;
- B: 6;
- C: 7;
- D: 8;

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The buit-in method `Object.assign(candidate, job)` merges the two objects `candidate` and `job` into one object. Then the method `Object.keys` counts the number of `key` in the object.

Note that two methods `get()` and `count()` are defined as `static`, so they need to be called statically using `Class.staticmethod()` syntax. Then the final object get 5 elements.

</p>
</details>

---

###### 8. What's the output?

```javascript
var x = 1;

(() => {
  x += 1;
  ++x;
})();
((y) => {
  x += y;
  x = x % y;
})(2);
(() => (x += x))();
(() => (x *= x))();

console.log(x);
```

- A: 4;
- B: 50;
- C: 2;
- D: 10;

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

Initially `x` is declared with the value 1. In the first IIFE function, there are two operations. First `x` becomes 2 and then 3.

In the second IIFE function, `x = x + y` then the current value is 5. In the second operation, it returns only 1 as it undergoes `5%2`.

In the third and fouth IIFE functions, we get 2 `x = x + x` and then 4 `x = x * x`. It is more than simple.

</p>
</details>

---

###### 9. What's the output?

```php
$var = 10;

$f = function($let) use ($var) {
    return ++$let + $var;
};

$var = 15;
echo $f(10);
```

```javascript
var x = 10;

const f = (l) => ++l + x;

x = 15;
console.log(f(10));
```

- A: 26 and 26;
- B: 21 and 21;
- C: 21 and 26;
- D: 26 and 21;

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

This question illustrates the diffences between PHP and JavaScript when handling closure. In the first snippet, we declare a closure with the keyword `use`. Closure in PHP is simply an anonymous function and the data is passed to the function using the keyword `use`. Otherwise, it is called as `lambda` when we do not use the keyword `use`. You can check the result of the snippet here https://3v4l.org/PSeMY. PHP `closure` only accepts the value of the variable BEFORE the closure is defined, no matter where it is called. As such, `$var` is 10 rather than 15.

On the contrary, JavaScript treats the variable a bit different when it is passed to anonymous function. We do not have to use the keyword `use` here to pass variable to the closure. The variable `x` in the second snippet is updated before the closure is called, then we get 26.

Note that in PHP 7.4, we have arrow function and we then do not have to use the keyword `use` to pass the variable to function. Another way to call a `global` ariable inside a function in PHP is to use the keyword `global` or employ the built-in GLOBAL variable \$GLOBALS.

</p>
</details>

---

###### 10. What's the output?

```javascript
let x = {};
let y = {};
let z = x;

console.log(x == y);
console.log(x === y);
console.log(x == z);
console.log(x === z);
```

- A: true true true true;
- B: false false false false;
- C: true true false false;
- D: false false true true;

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

Technically, `x` and `y` have the same value. Both are empty objects. However, we do not use the value to compare objects.

`z` is `x` are two objects referring to the same memory position. In JavaScript, array and object are passed by `reference`. `x` and `z` therefore return true when being compared.

</p>
</details>

---

###### 11. What's the output?

```javascript
console.log("hello");

setTimeout(() => console.log("world"), 0);

console.log("hi");
```

- A: "hello" -> "world" -> "hi"
- B: "hello" -> "hi" -> "world"
- C: "hi" -> "world" -> "hello"
- D: "hi" -> "hello" -> "world"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Given that the function setTimeout() will be kept in the `task queue` before jumping back to `stack,` "hello" and "hi" will be printed first, then A is incorrect. That is also the case of the answers C and D.

No matter how many seconds you set to the `setTimeout()` function, it will run after synchronous code. So we will get "hello" first as it is put into the call stack first. Though the `setTimeout()` is then being put into the call stack, it will subsequently offload to web API (or Node API) and then being called when other synchronous codes are cleared. It means we then get "hi" and finally "world".

So B is the correct answer.

Credit: @kaitoubg (voz) for your suggestion regarding the ` timeout throttled` by which I have decided to alter the question slightly. It will ensure that readers will not get confused as the previous code might bring out different results when tested on other browsers or environments. The main point of the question is about the discrepancy between the synchronous code and asynchronous code when using `setTimeout.`.

</p>
</details>

---

###### 12. What's the output?

```javascript
String.prototype.lengthy = () => {
  console.log("hello");
};

let x = { name: "Vuong" };

delete x;

x.name.lengthy();
```

- A: "Vuong";
- B: "hello";
- C: "undefined"
- D: "ReferenceError"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

`String.prototype.someThing = function () {}` is the common way to define a new built-in method for `String`. We can do the same thing with `Array`, `Object` or `FunctionName` where FunctionName is the function designed by ourself.

That is not challenging to realise that `"string".lengthy()` always returns `hello`. Yet, the tricky part lies in the `delete object` where we might think that this expression will entirely delete the object. That is not the case as `delete` is used to delete the property of the object only. It does not delete the object. Then we get `hello` rather than `ReferenceError`.

Note that if we declare object without `let, const` or `var`, we then have a global object. `delete objectName` then return `true`. Otherwise, it always returns `false`.

</p>
</details>

---

###### 13. What's the output?

```javascript
let x = {};

x.__proto__.hi = 10;

Object.prototype.hi = ++x.hi;

console.log(x.hi + Object.keys(x).length);
```

- A: 10
- B: 11
- C: 12
- D: NaN

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

First we have an empty object `x`, then we add another property `hi` for x with `x.__proto__.hi`. Note this is equivalent to `Object.prototype.hi = 10` and we are adding to the `father` object `Object` the property `hi`. It means every single object will inherit this propety. The property `hi` becomes a shared one. Say now we declare a new object such as `let y = {}`, `y` now has a propery `hi` inherited from the `father` `Object`. Put it simply `x.__proto__ === Object.prototype` returns `true`.

Then we overwrite the property `hi` with a new value 11. Last we have 11 + 1 = 12. `x` has one property and `x.hi` returns 11.

Updated (July 27th 2021). If you write `Object.prototype.hi = 11;` instead of `Object.prototype.hi = ++x.hi;` as written in the code above, then `Object.keys(x)` will return an empty array as `Object.keys(object)` only returns the property of the object itself, not the inherited ones. It means the final result will be 11 rather than 12. For some reason, the code ``Object.prototype.hi = ++x.hi;` will create a property for the object `x` itself and then `Object.keys(x)` gives us the array `["hi"]`.

Yet, if you run `console.log(x.hasOwnProperty("hi"))` it still returns `false`. By the way, when you deliberately add a property for x such as `x.test = "testing"`, then `console.log(x.hasOwnProperty("test"))` returns `true`.

</p>
</details>

---

###### 14. What's the output?

```javascript
const array = (a) => {
  let length = a.length;
  delete a[length - 1];
  return a.length;
};

console.log(array([1, 2, 3, 4]));

const object = (obj) => {
  let key = Object.keys(obj);
  let length = key.length;
  delete obj[key[length - 1]];

  return Object.keys(obj).length;
};

console.log(object({ 1: 2, 2: 3, 3: 4, 4: 5 }));

const setPropNull = (obj) => {
  let key = Object.keys(obj);
  let length = key.length;
  obj[key[length - 1]] = null;

  return Object.keys(obj).length;
};

console.log(setPropNull({ 1: 2, 2: 3, 3: 4, 4: 5 }));
```

- A: 333
- B: 444
- C: 434
- D: 343

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

This question examines how the `delete` operator works in JavaScript. In short, it does nothing when we write `delete someObject` or `delete someArray`. It nonetheless completely deletes and removes a property of an object when writing something like `delete someObject.someProperty`. In the case of array, when we write `delete someArray[keyNumber]`, it only removes the `value` of the `index`, keep the `index` intact and the new `value` is now set to `undefined`. For that reason, in the code first snippet, we get (the length) 4 elements as in the original array but only 3 properties left in the object passed when the function object() is called, as in the second snippet.

The third snippet gives us 4 as declaring an object's propery to either `null` or `undefined` does not completely remove the property. The key is intact. So the length of the object is immutable.

For those who are familiar with PHP, we have `unset($someArray[index])` that remove the array element, both key and value. When `print_r` the array, we might not see the key and value that have been unset. However, when we push (using `array_push($someArray, $someValue)`) a new element in that array, we might see that the previous key is still kept, but no value and not being displayed. That is something you should be aware of. Have a look at https://3v4l.org/7C3Nf

</p>
</details>

---

###### 15. What's the output?

```javascript
var a = [1, 2, 3];
var b = [1, 2, 3];

var c = [1, 2, 3];
var d = c;

var e = [1, 2, 3];
var f = e.slice();

console.log(a === b);
console.log(c === d);
console.log(e === f);
```

- A: true true true
- B: false false true
- C: true true false
- D: false true false

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

`a` and `b` returns false because they point to different memory location even though the values are the same. If you are coming from PHP world, then it will return true obviously when we compare either value or value + type. Check it out: https://3v4l.org/IjaOs.

In JavaScript, value is passed by reference in case of `array` and `object`. Hence in the second case, `d` is the copy of `c` but they both point to the same memory position. Everything changes in `c` will result in the change in `d`. In PHP, we might have `$a = &$b;`, working in the similar way.

The third one gives us a hint to copy an array in JavaScript using `slice()` method. Now we have `f`, which is the copy of `e` but they point to different memory locations, thus they have different "life". We get `false` accordingly when they are being compared.

</p>
</details>

---

###### 16. What's the output?

```javascript
var languages = {
  name: ["elixir", "golang", "js", "php", { name: "feature" }],
  feature: "awesome",
};

let flag = languages.hasOwnProperty(Object.values(languages)[0][4].name);

(() => {
  if (flag !== false) {
    console.log(
      Object.getOwnPropertyNames(languages)[0].length <<
        Object.keys(languages)[0].length
    );
  } else {
    console.log(
      Object.getOwnPropertyNames(languages)[1].length <<
        Object.keys(languages)[1].length
    );
  }
})();
```

- A: 8
- B: NaN
- C: 64
- D: 12

<details><summary><b>Answer</b></summary>
<p>

#### Answer: 64

The code snippet is quite tricky as it has a couple of different built-in methods handling object in `JavaScript`. For example, both `Object.keys` and `Object.getOwnPropertyNames` are used even thought they are quite similar except that the latter can return non-enumerable properties. You might want to have a look at this thoroughly written reference https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyNames

`Object.values` and `Object.keys` return the property value and property name of the object, respectively. That is nothing new. `object.hasOwnProperty('propertyName')` returns a `boolean` confirming whether a property exists or not.

We have `flag` true because `Object.values(languages)[0][4].name` returns `feature`, which is also the name of the property.

Then we have 4 << 4 in the `if-else` flow that returns the bitwise value, equivalent to `4*2^4` ~ `4*16` ~ 64.

</p>
</details>

---

###### 17. What's the output?

```javascript
var player = {
  name: "Ronaldo",
  age: 34,
  getAge: function () {
    return ++this.age - this.name.length;
  },
};

function score(greeting, year) {
  console.log(
    greeting + " " + this.name + `! You were born in  ${year - this.getAge()}`
  );
}

window.window.window.score.call(window.window.window.player, "Kiora", 2019);

score.apply(player, ["Kiora", 2009]);

const helloRonaldo = window.score.bind(window.player, "Kiora", 2029);

helloRonaldo();
```

- A: "Kiora Ronaldo! You were born in 1985", "Kiora Ronaldo! You were born in 1985", "Kiora Ronaldo! You were born in 1985"
- B: "Kiora Ronaldo! You were born in 1991", "Kiora Ronaldo! You were born in 1991", "Kiora Ronaldo! You were born in 1999"
- C: "Kiora Ronaldo! You were born in 1991", NaN, "Kiora Ronaldo! You were born in 1980"
- D: "Kiora Ronaldo! You were born in 1991", "Kiora Ronaldo! You were born in 1980", "Kiora Ronaldo! You were born in 1999"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

We can use `call()`, `apply()` and `bind()` to apply a function to any object. At first sight, it seems that three functions do the same thing. Yet there are some situations where they are differently employed to handle respective contexts or solve particular problems.

Of the three, only `bind()` can be executed after binding. We can create a variable to store the result as `helloRonaldo()` in the code snippet above. `apply()` and `call()` will bind and execute the function at the same time. `apply()` hints us `a` ~ array where we need to pass an array as parameter. `call()` hints us `c` or comma where we pass parameters with a comma. You might want to have a look at this post https://stackoverflow.com/questions/15455009/javascript-call-apply-vs-bind

Note that `window.window.window.score` or `window.score` or simply `score` do the same thing. It points to the `score()` function in the global scope.

The correct anwser is D. The `score()` and `getAge()` functions are nothing special. The only tricky part is that `this.age` is incremented each time you call the funtion `getAge()`;

</p>
</details>

---

###### 18. What's the output?

```javascript
var ronaldo = { age: 34 };

var messi = { age: 32 };

function score(year, tr, t) {
  if (typeof tr === "function" && typeof t === "function") {
    console.log(`You score ${tr(year, t(this.age))} times`);
  }
}

const transform = (x, y) => x - y;

const title = (x) => ++x + x++;

const helloRonaldo = score.bind(ronaldo, 2029, transform, title);

helloRonaldo();

const helloMessi = score.bind(messi, 2029, transform, title);

helloMessi();
```

- A: "You score 1989 times" and "You score 1963 times"
- B: "You score 1959 times" and "You score 1989 times"
- C: "You score 1989 times" and "You score 1953 times"
- D: "You score 1959 times" and "You score 1963 times"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

`bind()` allows us to bind a function declared with any object. Here we bind `score()` and both `ronaldo` and `messi`.

In `score()` we pass three parameters `year`, `tr` and `t` in which both `tr` and `t` are function. They handle simple things as defined afterwards.

When we bind `score()` with `ronaldo` and `messi`, we pass three parameters as declared in the `score()` function wherein `transform` and `title` are functions.

</p>
</details>

---

###### 19. What's the output?

```javascript
var person = {};

Object.defineProperties(person, {
  name: {
    value: "Vuong",
    enumerable: true,
  },
  job: {
    value: "developer",
    enumerable: true,
  },
  studying: {
    value: "PhD",
    enumerable: true,
  },
  money: {
    value: "NZD",
    enumerable: false,
  },
});

class Evaluate {
  static checkFlag(obj) {
    return Object.getOwnPropertyNames(obj) > Object.keys(obj)
      ? Object.getOwnPropertyNames(obj)
      : Object.keys(obj);
  }
}

const flag = Evaluate.checkFlag(person);

console.log(flag.length);
```

- A: 1
- B: 2
- C: 3
- D: 4

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

`Object.keys(obj)` is almost identical to `Object.getOwnPropertyNames(obj)` except the fact that the latter returns any type of object's property regardless of `enumerable`. By default `enumerable` is true when creating object. Using `Object.defineProperties` or `Object.defineProperty` we can manually set this option to `false`.

As such the object `person` will get 3 using`Object.keys(obj)`but 4 with `Object.getOwnPropertyNames(obj)`. `In short Object.keys(obj)` only returns the property setting the enumerable as `true`.

</p>
</details>

---

###### 20. What's the output?

```javascript
const id = 10;

const getID = (...id) => {
  id(id);

  function id(id) {
    console.log(typeof id);
  }
};

getID(id);
```

- A: ReferenceError
- B: 10
- C: undefined
- D: 'function'

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

When declaring a function inside another function, we are working with Closure in JavaScript. Note that if a function is declared as normal (rather than function expression), it is hoisted. We might see several `id` in the code snippet above but in fact, some of them does nothing.

The result of the code depending on the operator `typeof id`, which is `function`. So `id` in this operation is the `id()` function.

</p>
</details>

---

###### 21. What's the output?

```javascript
var book1 = {
  name: "Name of the rose",
  getName: function () {
    console.log(this.name);
  },
};

var book2 = {
  name: { value: "Harry Potter" },
};

var bookCollection = Object.create(book1, book2);

bookCollection.getName();
```

- A: 'Harry Potter'
- B: 'Name of the rose'
- C: ReferenceError
- D: Object object

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

`Object.create` allows us to create an object which is based on another object. If we do not pass the second parameter - `book2` in this case - the `name` property of the object `bookCollection` will be `Name of the rose` inherited from the `book1`. It means we can provide additional properties when declaring object with `Object.create`.

`bookCollection` has its own property `name` and another one inherited from `book1`. In this case its own property `name` will show up as it has higher priority. That is why we get 'Harry Potter'.

</p>
</details>

---

###### 22. What's the output?

```javascript
(() => {
  const a = Object.create({});

  const b = Object.create(null);

  let f1 = a.hasOwnProperty("toString");

  let f2 = "toString" in b;

  let result =
    f1 === false && f2 === false
      ? console.log((typeof a.toString()).length)
      : console.log(b.toString());
})();
```

- A: ReferenceError
- B: undefined
- C: 0
- D: 6

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The two objects `a` and `b` are created using `Object.create()` operator. There is a bit of difference between them as `a` inherits from Object prototype but `b` is totally empty when we pass the `null` paramater. Yet `hasOwnProperty('toString')` always returns `false` neither `a` nor `b` given that `toString()` is not defined inside these objects. The method however is still available as it is inherited from Object prototype.

Both `f1` and `f2` return `false`. Note that we use `object.hasOwnProperty('key')` and `('key' in object)` to check the availability of a key in an object. There is a bit difference between the two as the latter also returns the key inherited. You might want to have a look here: https://stackoverflow.com/questions/455338/how-do-i-check-if-an-object-has-a-key-in-javascript

Then `typeof a.toString()` returns `string`, which gives us 6 with the `.length` property.

If the syntax is odd to you, you might look for 'self-invoking function' and 'arrow function' in JavaScript.

</p>
</details>

---

###### 23. What's the output?

```javascript
let promise = new Promise((rs, rj) => {
  setTimeout(() => rs(4), 0);

  Promise.resolve(console.log(3));

  console.log(2);
});

promise
  .then((rs) => {
    console.log(rs ? rs ** rs : rs);
    return rs;
  })
  .then((rs) => console.log(rs == 256 ? rs : rs * rs));
```

- A: 3, 2, 256, 256
- B: 3, 2, 256, 16
- C: 256, 16, 3, 2
- D: 16, 256, 3, 2

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

We first declare a promise-based code with `let` and then call it. Given that `setTimeout()` is an asynchronous action, it will run last even the time is set to 0 in `setTimeout(() => rs(4), 0);`. Although `Promise.resolve(console.log(3))` also returns a promise but it is a Microtasks, then it has a higher priority than Tasks as set by `setTimeout()`. You might want to have a look at this post https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/.

In `.then()` we chain the result so that we have `4^4` in the first then() and `4*4` in the second `then()`. Note that `return rs` returns the original value.

</p>
</details>

---

###### 24. What's the output?

```javascript
async function f() {
  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("done!"), 0);
  });

  setTimeout(() => console.log("world"), 0);

  console.log(await promise);

  console.log("hello");
}

f(setTimeout(() => console.log("kiora"), 0));
```

- A: ReferenceError
- B: done, hello, world
- C: hello, done, world
- D: kiora, done, hello, world

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

Though we do not declare any paramater for the function `f()`, we pass `setTimeout(()=>console.log("kiora"),0)` when call it. We therefore get 'kiora' first.

Given that the variable `promise` returns a solved promise and it is called with the keyword `await`, JavaScript will 'pause' at this line `console.log(await promise);` till the result is resolved. That is why we get "done" at the next result.

Why we do not get "world" or "hello" at the second ? As JavaScript "pauses" at the line with `await` keyword, we cannot get "hello" as usual (note that whenever we call setTimeout(), this function will run last because it is an asynchronous task operator), whereas `setTimeout(()=> console.log("world"), 0);` should always run last.

Here we might see a bit of difference when employing `await` keyword before asynchronous operator (in this case, we use `setTimeout()` as an example) or when call the function/operator without it.

</p>
</details>

---

###### 25. What's the output?

```javascript
function name() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("New Zealand");
    }, 10);
  });
}

function fruit() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Kiwi");
    }, 20);
  });
}

(async function countryandfruit() {
  const getName = await name();
  const getFruit = await fruit();

  console.log(`Kiora: ${getName} ${getFruit}`);
})();

(async function fruitandcountry() {
  const [getName, getFruit] = await Promise.all([name(), fruit()]);

  console.log(`Hello: ${getName} ${getFruit}`);
})();
```

- A: Null
- B: Kiora
- C: "Hello: New Zealand Kiwi" -> "Kiora: New Zealand Kiwi"
- D: "Kiora: New Zealand Kiwi" -> "Hello: New Zealand Kiwi"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Both `countryandfruit` and `fruitandcountry` are self invoking functions. Both are declared with the keyword `async`, it means the code inside will run step by step. It helps us control the flow of data much more concise as compared to Promise-based operator or callback way.

The first function returns `"Kiora: New Zealand Kiwi"` and the second one ouputs `"Hello: New Zealand Kiwi"`. We might think that the order will be the same but actually the order of the result is reversed because the function with `await` keyword will run step by step rather than in in parallel as Promise.all. It means `fruitandcountry` will run faster than `countryandfruit`.

You might want to have a look at the difference between the two at https://alligator.io/js/async-functions/

</p>
</details>

---

###### 26. What's the output?

```javascript
class MySort {
  constructor(object) {
    this.object = object;
  }

  getSort() {
    return Object.entries(this.object)[0][1].sort()[
      Object.values(this.object).length
    ];
  }
}

const object = {
  month: ["July", "September", "January", "December"],
};

const sortMe = new MySort(object);

console.log(sortMe.getSort());
```

- A: July
- B: September
- C: January
- D: December

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

`Object.entries` returns an array consisting of both key and value from an object while `Object.values` retuns an array of the values of object and `Object.keys` gives us an array of keys of the object. As such, `Object.entries(object)` in the code snippet above gives us a nested array with just one element in which the values are put in another nested array like that `[["month", ["July", "September", "January", "December"]]]`.

For that reason, `Object.entries(this.object)[0][1].sort()` will actually sort the value array and return a new order as "December" -> "January" -> "July" -> "September". Hence, when we get the element with the index given by `[Object.values(this.object).length]` we get `January` because `[Object.values(this.object).length]` give us 1 (the length of the array given by Object.values);

</p>
</details>

---

###### 27. What's the output?

```javascript
const flag = [] !== !!!!![];

let f = () => {};

console.log((typeof f()).length + flag.toString().length);
```

- A: NaN
- B: 12
- C: 13
- D: 14

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Comparing two arrays or two objects in JavaScript always return `false` because both are passed by reference, unlike primitive types such as string, number or boolean. That is why comparing [] and [] using either == or === returns `false`. The weird part is the `!==!!!!!` which is equivalent to `!==`, nothing special. So the `flag` is `true`.

In the expression function `f()`, we use arrow function here but and `{}` is a part of the function rather than an object. In case you want to return an object, you have to write as `let f = () => ({})` or simply using normal way to define function. With the keyword `return`, we can easily catch the content of the function when using normal way to define function.

Thus, the `typeof f()` returns `undefined` rathern `object`. We then get the length 9 and the flag (true) becomes 'true' (a string, by using toString() function), which returns 3 with the property `length`. We finally get 13.

</p>
</details>

---

###### 28. What's the output?

```javascript
(function (a, b, c) {
  arguments[2] = (typeof arguments).length;
  c > 10 ? console.log(c) : console.log(++c);
})(1, 2, 3);
```

- A: 4
- B: 5
- C: 6
- D: 7

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

We have a self-invoking function with three parameters declared. Note that `arguments` inside a function returns an object consisting of the parameters of the function.

The key part here is that when we assign a value to that array (it is array-like, as mentioned above) (or any element), the function will use that value rather than the value from the parameter we pass to it when calling the function. Hence, `c` will be `(typeof arguments).length;` (6) rather than 3.

As `c` has a new value of 6, it is definitely less than 10, so we get the final result `console.log(++c)`, which returns 7.

Note that `arguments` is not available on arrow functions. See more detailed here https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments

From ES6 onwards, it is recommended to use ...restParameter given that it is a true array. It means you can manipulate the parameter with native JavaScript functions such as map, reduce or filter.

For PHP developer, we have `func_get_args()` in PHP that does the same thing, but it will not override the value passed. Check it by yourself at https://3v4l.org/dMfhW

</p>
</details>

---

###### 29. What's the output?

```javascript
class Calculator {
  constructor(a, b) {
    this.a = a;
    this.b = b;
  }
  static getFlag() {
    return new Array(this.a).length == new Array(this.b).toString().length;
  }

  getValue() {
    return Calculator.getFlag() ? typeof this.a : typeof new Number(this.b);
  }
}

const me = new Calculator(5, 5);

console.log(me.getValue());
```

- A: NaN
- B: "string"
- C: "object"
- D: "number"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

We have a class named Calculator. When declaring a new instance of the object, we pass two parameters `a` and `b`. These two parameters have the same value but `new Array(this.a).length` is totally different from `new Array(this.b).toString().length` because the latter returns a string `",,,,"` meaning the length 4 while the former returns the length of an array and we therefore get 5.

For that reason `getFlag()` returns `false`. In `getValue()` we get `typeof new Number(this.b);` which returns `object`. That is a bit different from `typeof b`, which returns `number`.

</p>
</details>

---

###### 30. What's the output?

```javascript
var name = "Auckland";

const nz = {
  name: "Kiwi",

  callMe: function () {
    return this.name;
  },
};

let me = nz.callMe;

let she = nz.callMe.bind(nz);

let result = me() === nz.callMe() ? she() : `${me()} ${she()}`;

console.log(result);
```

- A: undefined
- B: "Auckland"
- C: "Kiwi"
- D: "Auckland Kiwi"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The key point in this question involves the keyword `this` in JavaScript. We have a simple object that contains one method and one string property `name`.

First, it is important to write down is that `let me = nz.callMe;` and then call `me()` is totally different from directly calling `nz.callMe()`. If we assign a variable to a method delared inside an object, `this` in that method will behave differently (when we call the variable as a method and when dirrectly call that method). In particular, in the first case, `this` is the `window` object while in the second one, `this` inside the function still points to property `name` in the object `nz`. It means `me()` returns "Auckland" while `nz.callMe` returns "Kiwi".

Then `result` will return `false` and we get the final output value `${me()} ${she()}`. Why `she()` is different from `me()`? You might easily guess that `she` still `bind` to the object `nz` rather than `window` object as in `me()`.

</p>
</details>

---

###### 31. What's the output?

```javascript
const club = {
  name: "Juventus",
  player: ["Ronaldo"],
  showMePlayer: function () {
    this.player.map(function (thename) {
      console.log(this.name.length);
    }, this);
  },
  showMe: function () {
    this.player.forEach(
      function (thename) {
        console.log(this.name.length);
      }.bind(this)
    );
  },
  show: function () {
    const self = this;
    this.player.map(function (thename) {
      console.log(self.name.length);
    });
  },
  Me: function () {
    this.player.map(function (thename) {
      console.log(this.name.length);
    });
  },
};

club.showMePlayer();
club.showMe();
club.show();
club.Me();
```

- A: 8 - 8 - 8 - 8
- B: "Juventus" - "Juventus" - "Juventus" - "Juventus"
- C: "Ronaldo" - "Ronaldo" - "Ronaldo" - "Ronaldo"
- D: 8 - 8 - 8 - 0

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The code snippet above is not a big challenge for you I guess. It simply gives you an example of `this` in different contexts when we declare an anonymous function inside a method of an object. The three first methods are common ways to handle `this` using `this` as second parameter in `map()`, by using `bind(this)` in `forEach` (or map()) or by `that = this`technique (you might see people use `self = this` rather than `that= this`).

The last method `Me()` will cause unexpected result because `this.name` does not bind to the object `club`. Note that you might get another result when testing the code on jsbin.com. On Chrome and Firefox, we get 0.

For further information, kindly have a look at http://speakingjs.com/es5/ch17.html#_pitfall_losing_this_when_extracting_a_method

</p>
</details>

---

###### 32. What's the output?

```javascript
((...a) => {
  const b = ["javascript", "new zealand"];

  const c = [...a, typeof a, ...b, "kiwi"];

  console.log(c.length + c[0].length);
})(new Array(10));
```

- A: 5
- B: 10
- C: 15
- D: 20

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

`...` can be used in two ways in JavaScript (and PHP) as either `spread operator` or `rest parameter`. You might have to check the following article about the two. They are the same as three dots, but the way they are employed vary considerably between the two. https://javascript.info/rest-parameters-spread-operator

We see both `spread operator` and `rest parameter` in the code snippet above. First the parameter `(...a)` in the self-invoking function is of course a `rest parameter` while the constant `c` we see the `spread operator`. In the former case, it simply means that you can pass to the function as many parameter as you want. Note that the `typeof a` in this case is `object` even though it is a native array in JavaScript. (I means native array because you might think about array-like if we use arguments. Please have a look at the question 28 or this link https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments).

`Spread operator` as in the constant `c` allows us to combine array. So `...a` in the code above is `rest parameter` when it is used as function parameter but in this case it is the syntax of `spread operator`.

Finally, we get `c` with 5 elements (`...a` is a nested array, so the `length` is 1) but the first element has 10 child elements (when we pass to the function `new Array(10)`). The length of both then returns 15.

</p>
</details>

---

###### 33. What's the output?

```javascript
function Kiora(name, ...career) {
  this.name = name;

  return Array.isArray(career) === true && typeof career === "object" ? {} : "";
}

var student = new Kiora("Vuong");

console.log(student.name);
```

- A: "Vuong"
- B: undefined
- C: ErrorReference
- D: false

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

We have a function constructor `Kiora` (written with a capital letter, but that is optional) that can be used to create object, as the `student` object in the code above. In the function, we have two parameters with the second one is actually a `rest parameter`. The typeof operator is `object` but if we check with `Array.isArray(array)` it also returns true.

For that reason, `Array.isArray(career) === true && typeof career === "object"` returns true. Hence the `return` operator finally returns an object `{}`.

You might be surprised when `console.log(student.name);` outputs `undefined` given that the constructor function `Kiora` returns an object. Otherwise, we might simply get the value `name`.

</p>
</details>

---

###### 34. What's the output?

```javascript
class Filter {
  constructor(element) {
    this.element = element;
  }
  filter() {
    return this.type() === "object" ? this.element[0].name : "hello";
  }

  type() {
    return typeof this.element;
  }
}

let countries = [
  { name: "New Zealand", isdeveloped: true },
  { name: "Vietnam", isdeveloped: false },
];

let x = new Filter(countries);

const filter = countries.filter((item) => {
  return !item.isdeveloped;
});

console.log(x.filter().length + filter[0].name.length);
```

- A: 15
- B: 16
- C: 17
- D: 18

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

Apologize that the code snippet is a bit longer than usual. But actually it is not really challenging as you might think. You can easily get the correct result after spending a little of time to debug.

First we declare a class that has two methods. The first method `filter()` will returns the first element of the array (of the propterty `element`) or simply returns `hello` depending on the `type()` method. We know that `typeof of array` will return `object` so the `filter()` method return `this.element[0].name`.

Try to make you feel confused, we then call the built-in `filter()` method. This native method returns a new array depending on the condition we pass to the call-back function. Note that `!item.isdeveloped` means `false`. It means we get `Vietnam`.

Finally we get `New Zealand`.length and `Vietnam`.length, which in total returns 18.

</p>
</details>

---

###### 35. What's the output?

```javascript
async function abc() {
  console.log(8);

  await Promise.resolve(2).then(console.log);

  console.log(3);
}

setTimeout(() => {
  console.log(1);
}, 0);

abc();

queueMicrotask(() => {
  console.log(0);
});

Promise.resolve(4).then(console.log);

console.log(6);
```

- A: 6 - 8 - 3 - 0 - 4 - 2 - 1
- B: 8 - 2 - 3 - 0 - 4 - 6 - 1
- C: 6 - 8 - 2 - 0 - 4 - 3 - 1
- D: 8 - 6 - 2 - 0 - 4 - 3 - 1

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

D is correct anwser. The order of the asynchronous code's output depends on the MicroTask or MacroTask. MicroTask has a higher priority. Note that the synchronous code always be executed before asynchronous code. So in essense, we have the order as follows:

      1) synchronous code
      2) microtask code (promise, queueMicrotask)
      3) macrotask code (setTimeout, setInterval)

Be awared that in Nodejs environment, we also have `process.nextTick(callback)` which has the highest priority but we dont have it in this code.

So, first callback in the `setTimeout()` will be executed last given that this is a MacroTask. That is why we got 1 last.

Second, the function `abc()` is called next. Then we have 8 printed out in the console first. As the next line of code inside that function is an asynchrnous code with the keyword "await", we then `console.log(6)` as `Promise.resolve(4).then(console.log)` is an asynchrnous code. That is why we got 6.

Now is the time for `Promise.resolve(2)`, so we get 2. At this point, you might have some sort of confusion. What will happend if we do not pass the keyword "await" before `Promise.resolve(2)` ?

As we have `await`, the code will be blocked here. Then what? We get 0 and 4 not 3. `Promise` and `queueMicrotask` are both microtask and they are already to run before `console.log(3)`. The reason is that microtask queue need to be emptied before any other codes can be called in the callstack.

In the next step, we get 3 and the last one is 1.

What would happend if we do not have the `await` keyword? Then the order of the output will be 8 - 3 - 6 - 2 - 0 - 4 -1.

</p>
</details>

###### 36. What's the output?

```javascript
function myAccount(money) {
  let myMoney = money;

  return {
    status: function () {
      return `You have $ ${myMoney} in your account`;
    },
    dePoSit: function (amount) {
      myMoney = myMoney + amount;
    },
    withDraw: function (amount) {
      if (amount > myMoney) {
        return `You cannot withdraw money now`;
      }
      myMoney = myMoney - amount;
    },
  };
}

const vuong = myAccount(1000);

vuong.withDraw(500);

vuong.withDraw(200);

vuong.dePoSit(100);

vuong.withDraw(50);

console.log(vuong.status());
```

- A: "You have \$ 950 in your account"
- B: "You have \$ 1000 in your account"
- C: "You have \$ 550 in your account"
- D: "You have \$ 350 in your account"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

As the "state" of the data is preserved each time we call `dePoSit()` or `withDraw()`, hence we get \$350 after all.

Noted that that is a kind of "factory" function with "preload" data. You might think about another object when pass to `myAccount(somedata);` some other data. That is a really helpful way to create multiple objects from a factory function.

</p>
</details>

###### 37. What's the output?

```javascript
const hoccoban = {
  x: "youtube.com/hoccoban".length,
  getMe() {
    const inner = function () {
      console.log(++this.x);
    };
    inner.bind(this)();
  },
};

hoccoban.getMe();
```

- A: 20
- B: 21
- C: 22
- D: 23

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

We get 21. First "youtube.com/hoccoban" returns 20 as we are using the property length of the string. Then it is being added one more value in `++this.x`. The question here seems trivial but it is actually not. There is a crucial note we should keep in mind is that `console.log(++this.x)` will not work as `x` is undefined when it is called outside of the object.

We can solve the problem with `this` in this case by using arrow function in the inner so that is can become something like `const inner = () => {}` as the arrow function does not actually have `this`. It will automatically look around and call the available object when the function is executed.

The second solution is that we can somehow "bypass" the tricky `this` by using that/this solution. We just need to declare a new variable `const that = this` inside getMe() and before declaring inner function. That is a quite common practice.

The third solution is to take advantage of call(), bind() and apply() which are native methods of function (yes, function is also an object in JavaScript). In this case, we implement `bind(this)` to "bind" the function and the object so that `this` can actually point to the object when the function is executed. Note that bind() cannot be instantlly executed so that we need to add () after we bridge the function and the object. If we replace bind() with call(), then we do not need to pass () as in the above example. So `inner.bind(this)();` will become `inner.call(this);`. They are technically equal. In practice, we tend to create a new variable to get the result from the binding of the function and the object.

</p>
</details>

###### 38. What's the output?

```javascript
function* hocCoBan() {
  yield "js.edu.vn";
  yield "youtube.com/hoccoban";
  yield "Vuong Nguyen";
}

let data = hocCoBan();

console.log((typeof data).length + data.next().value.length);
```

- A: NaN
- B: 10
- C: Error
- D: 15

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

First, take a closer look at the function. It has a asterisk (\*) next to the keyword "function". We do not have `return` keyword inside the function itself. What is going on here?

It you have already known about generator, then this code snippet is not a big deal at all. We do not use generator very often, but this native JavaScript feature is the basis for async/await function, which is supported in ES7 that allows us to handle the flow of asynchronous code much easily.

The operator `typeof data` will return `object` rather than `function`, which is the same case with `typeof hocCoBan()`. Of course, `typeof hocCoBan` still returns `function`. But it is actually a normal function. Basically, we get 6 in the operator `(typeof data).length`.

Then `data.next()` calls the the built-in method `next()` which will output the value in the first `yield`, which is declared in the function. Then we get the length 9 with the string `js.edu.vn`.

After all, we get 15. Not that understanding generator is quite important if you really want to understand `async/await` function.

</p>
</details>

###### 39. What's the output?

```javascript
const a = [1, 2, "chó", 3, 1, "chó", "mèo", 3];

const b = [...new Set(a)];

b.length = "chó".length;

console.log(b);
```

- A: 4
- B: [1, 2, "chó", 3, "mèo"]
- C: [1, 2, "chó", "mèo"]
- D: [1, 2, "chó"]

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

When using ... in array, it is called spread operator in JavaScript which, technically, is similar to rest parameter (using in the context of function). It provides a more elegant way to concat (combine) or copy array. In the code above, b is a copy of a. However, as we pass a in to a `Set`, it will return the unique value only in a. It means, now we have `[1, 2, "chó", 3, "mèo"] in b.

However, we then set the length for b as 3. Note that "chó".length returns 3 but in PHP, strlen("chó") returns 4, just in case you are coming from PHP world.

As we set the length for the array b, we also cut down the array itselt. That is the reason why we get [1, 2, "chó"] printing out in the console.

</p>
</details>

###### 40. What's the output?

```javascript
const mot = function (m) {
  return arguments[0];
};

const hai = function (...m) {
  return arguments[arguments[0]];
};

const a = [mot(123), hai(1, 2, 3)];

console.log(typeof a !== "object" ? a[0] : a[1]);
```

- A: 1
- B: 2
- C: 3
- D: 123

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

First, it should be noted that `arguments` cannot be used in an arrow function, so in order to take advantage of this feature, we have to write the function in the casual form. `arguments` returns an array-like object that contains any parameter we pass into the function when executing it.

`...` is a `rest operator`. We use this feature in function and array. Noted that in the context of array, it is called `spread operator` and it behaves differently. When declaring a function with ..., we can pass as many parameters into the function itselt when executing it as we want.

Note that in the function `hai`, we return `arguments[arguments[0]]` which means `hai(1, 2, 3)` will return 2 rathern than 1 because `arguments[0]` return 1 and then `arguments[1]` returns 2.

The last thing we have to take note is that the typeof operator of an array will return `object`, here the trick seems more daunting. The final anwser is 2 as we got it in `a[1]`, or `hai(1, 2, 3)`.

</p>
</details>

###### 41. What's the output?

```javascript
class Component {
  constructor(age) {
    this.age = age + `${typeof Coder}`.length;
  }

  getAge() {
    return ++this.age;
  }
}

class Coder extends Component {
  constructor(age) {
    super(age);
    this.age = age - `${typeof Coder}`.length;
  }
}

const a = new Coder(16);

console.log(a.getAge());
```

- A: 7
- B: 8
- C: 9
- D: 10

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

We have two simple classes in which Coder extends Component. Nothing fancy. As `typeof ClassName` returns `function` rather than `class`, we then get 8 in the operator `"function".length`.

Though we implement `super(age)` in the Coder class, we actually overwrite the contructor of the parent class Component in the child class Coder. Therefore, when initiating the object `a`, the following code is automatically triggered `this.age = age -`\${typeof Coder}`.length;`. The difference between the child and parent 's constructor is minus (-) and plus (+) in the above code.

As such, we have 16 - 8 rather than 16 + 8, which returns 8. The function `getAge()` returns 9, so the corrent answer is C.

Bear in mind that JavaSCript is not a "real" OOP programming language even though we can now implement `class` and `object` as in other languages.

</p>
</details>

###### 42. What's the output?

```javascript
class RemoveFalse {
  constructor(element) {
    this.element = element;

    this.length = this.removeFalse().length;
  }

  removeFalse() {
    this.element = this.element.filter(Boolean);

    return this.element;
  }
}

const theArray = [true, false, 1, 0, NaN, undefined, "", null, "js.edu.vn"];

const a = new RemoveFalse(theArray);

console.log(a.length);
```

- A: false
- B: true
- C: 2
- D: 3

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The key message that can be taken away in the code snippet above is `filer(Boolean)` which can be taken into consideration in case you want to eliminate `falsy values` in an array. We can use `filter(callback)` or `filter(Boolean)` in particular in this case to do that. Note that we have to pass into the filter function a callback and in this case Boolean is actually a function. You can check `typeof Boolean` to see it.

Similar to `map` or `reduce` function, `filter` always returns a new array from the exisiting one. `[true, false, 1, 0, NaN, undefined, "", null, "js.edu.vn"].filter(Boolean);` will return `[true, 1, "js.edu.vn"];`, hence calling the function `removeFalse()` gives us 3. So the correct answer is 3.

</p>
</details>

###### 43. What's the output?

```javascript
const coderfarm = [1, [], {}, [], 2, 3];

const converted = Number(coderfarm instanceof Array);

const result = coderfarm.indexOf(converted + true);

console.log(result);
```

- A: []
- B: {}
- C: 2
- D: 4

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

We have a simple array in the code snippet above that includes some digits, two other arrays and one object. Using the built-in function `Number`, we can convert any value passing to the function into `digit`. As `coderfarm instanceof Array` returns `true`, then `converted` get 1. Noted that you can use another way to check the type of an array is `Array.isArrray(arrayToBeChecked)` which return a `boolean` value. Suprisingly, the operator `typeof []` returns `object` rather than `array`.

The built-in function `indexOf` will return the index of the element that is being checked. So as `converted + true` return 2, we are going to check the index of the element with the value 2 in the array `coderfarm`.

We get 4 in the `console.log` and the correct answer is D.

</p>
</details>

###### 44. What's the output?

```javascript
const converter = (arrayInput) => {
  return { ...arrayInput };
};

const content = ["function", "object", "decorator"];

const checking = content[Number(false)];

const result = typeof converter(content) === content[1];

console.log(checking ? (result ? (typeof converter).length : false) : false);
```

- A: 6
- B: NaN
- C: true
- D: 8

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The operator `...` in JavaScript is very handy. The function `converter` is quite trivial, it takes advantege of `...` (rest operator || spread operator) to turn an array into an object.

First we have the constant `checking` with the value `function` given that `Number(false)` gives us 0 and that is the first index in the array `content`.

Second, the constant `result` gives us the value `true` as the `typeof converter(content)` is `function`, which is also the value of `content[1]`.

Then in the final code, we have `checking = true`, and then `result = true` as well, so the final result is `(typeof converter).length` which is equivalent to `"function".length` because the `typeof of converter` is simply `function`. We get 8 after all and the correct answer is D.

So the key message here is that we can take advantate of the `spread operator` (or `...`) to turn an array to an object. For example: `const a = ["hello", 2]`, then we can have a go with `const b = {...a}` and b is now an object with the following value: `{0: "hello", 1: 2}`. The key of the object is actually the index of the original array.

</p>
</details>

###### 45. What's the output?

```javascript
function* js(length) {
  for (let i = length.length; i > 0; --i) {
    yield i;
  }
}

let getJS = js(typeof js);

let result = getJS.next().value;

console.log(result + getJS.next().value);
```

- A: 10
- B: 14
- C: 15
- D: 16

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

We have a generator function in the code snippet above, which is defined with the \*. Noted that we can "store" as many result as we want in a generator thanks to the keyword `yield`.

As the `typeof js` is `function`, so the length of the string `function` is 8. So when calling `getJS.next().value;`, we get 8. However, in the next calling, it returns 7, and in the following calling after that, we get 6. That is why generator can "store" and "release" (or return) as many value as we want.

So the answer is C, which is 8 (first execution of the generator) + 7 (second execution of the generator).

</p>
</details>

###### 46. What's the output?

```javascript
var ages = [10, 15, 20, 25];

let response = [];

ages.some(function (currentValue, index, ages) {
  if (currentValue > ages[ages.length - index])
    response.push(currentValue + ages.length);
});

console.log(response);
```

- A: [20]
- B: [20, 25]
- C: [25, 29]
- D: [29]

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

`Array.prototype.some()` is a built-in function facilitating us to iterate the array using a callback. As in the code snippet above, there are three parameters in the callback, namely `currentValue` (the value of the current element that is being checked), `index` (the index of the element in the array that is being checked/evaluated) and `ages` (the array itself).

The function `some()` returns a `boolean` value. The code `currentValue > ages[ages.length - index]` returns `true` only one time, which is the last element. Let 's examine the code when it runs through each element:

1. 10 > ages[4 - 0]. As ages[4] returns `undefined`, and `10 > undefined` returns `false`, it stops.

2. 15 > ages[4 - 1]. As ages[3] returns 25, it breaks as the operator returns `false`.

3. 20 > ages[4 - 2]. As ages[2] returns 20, it breaks as the operator returns `false`.

4. 25 > ages[4 - 3]. As ages[1] returns 10, it returns `true`. Only this value is being pushed to the array `response`.

So `response.push(currentValue + ages.length)` will add the value 25 + 4 to the array `response`, D is the correct answer.

</p>
</details>

###### 47. What's the output?

```javascript
const getSTring = (string, method = false) => {
  if (method === true) {
    return string.slice(1, 4).length;
  }

  return string.substr(1, 4).length;
};

console.log(getSTring("hello", true) + getSTring("hello"));
```

- A: 6
- B: 7
- C: 8
- D: 9

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

`getString()` is an arrow function with two parameters. As you can see that the parameter `method` has the default value `false`, then if you do not pass any value to it when executing the function, the default value will be used.

The key thing to take note from the code above is the difference betweet `slice(1, 4)` (which returns 3 characters) and `substr(1, 4)` (which returns 4 ones).

Finally `console.log(getSTring("hello", true) + getSTring("hello"))` returns 7 because `slice` and `substr` are both used.

</p>
</details>

###### 48. What's the output?

```javascript
(function (a, b, c) {
  console.log(Boolean([...arguments].slice(2, 3)[0].slice(3, 4)));
})("hello", "world", "new zealand");
```

- A: "new"
- B: true
- C: "land"
- D: false

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

The code above is a self-executing function. It runs when it is being declared. We have three parameters and three arguments passed are `"hello", "world"` and `"new zealand"`.

First, `arguments` returns an object consisting of arguments passed to the function when executing it. However, using spread operator `...`, we then convert the object to an array. We can also do it by using `Array.from(object)`.

Second, `slice(2, 3)` extracts the element from the index 2 to the index 3, which returns `"new zealand"`. It is still an array. We then extract the element with the index `[0]` and we get the string `"new zealand"` rather than an array.

Third, `"new zealand".slice(3, 4)` gives us an empty string (with a space between) `" "`. The `Boolean(" ")` gives us `true`. Noted that if there is no space in the empty string, we get `false` instead.

So the correct answer is B.

</p>
</details>

###### 49. What's the output?

```javascript
class HocCoBan {
  name = "hello world";

  getSlice(slice) {
    return this.getName(slice).slice(true, this.name.length);
  }

  getName(space) {
    return this.name.split(space);
  }
}

HocCoBan.prototype.split = function (argument) {
  return this.getSlice(argument);
};

const a = new HocCoBan();

console.log(a.split("").length);
```

- A: NaN
- B: true
- C: 10
- D: 11

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The code above is nothing much special. However it is written in a complicated way on purpose. First, we have a class named "HocCoBan" with two methods and one property. Then we add another method `split` using the tradional way (via `prototype`). Note that `class` in JavaScript is simply a syntactic sugar of `function` given that `typeof ClassName` return `function`.

When we call the method `split`, we pass the an empty string to it. This method then call other methods. The flow is as follows:

`split("")` ==> `this.getSlice("")` ==> `this.getName("")` ==> `this.name.split("")`. Here `split` is a built-in function that convert a string to an array.

Noted that in `getSlice()`, we also use `.slice(true, this.name.length)` to `slice` (cut) the array from the index 1 to 11. So the length is 10.

So the final answer is C.

This code might help us master the concept function `prototype` in JavaScript and the understand the difference between the built in function `String.prototype.split` and the function we declare by ourself `HocCoBan.prototype.split`.

</p>
</details>

###### 50. What's the output?

```javascript
function javaScript(node) {
  let mot = node.includes("I") ? "love" : "you";

  return function (deno = mot) {
    let hai = node.replace(deno, "done");

    return function (done = hai) {
      return (node + deno + done).length;
    };
  };
}

console.log(javaScript("I love you")()());
```

- A: 18
- B: 24
- C: 20
- D: 25

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Apart from learning some built-in functions to handle string such as `replace` and `inclues`, we are reviving the concept of `currying function` in JavaScript. Say you want to declare a function with three parameters, you may consider refactoring the code by declaring 3 nested functions, each with one parameter you wish to pass to. Basically, both of them work in the same way. However, noted that only the outerest (the main) function has the name as `javaScript` in the code above. Both nested (inner) functions are declared without the name. We also use three `return` keywords in the code.

When executing the function, you then have three `()` as in the `javaScript("I love you")()()`. We do not pass any argument into the second and third functions (both are inner/nested functions without the name) and these functions will take the default value we have alreaded declared when being executing.

All in all, we have the final operator `return (node + deno + done).length;` in which `node` is "I love you", `deno` is "love" and `done` is "I done you". The length of these strings is 24, which you can calculate by yourself the concatenated string `I love youyou I done you`. Be aware of the `empty space`, which is also taken into account.

</p>
</details>

###### 51. What's the output?

```javascript
const www = ["hello", "coranovirus", "kiora", "world", "new zealand"];

const found = www.find(function (world) {
  return world > "victory";
});

const result = found[1] < www[0][0] ? www[false ? 1 : 0] : www[true ? 0 : 1];

console.log(result);
```

- A: "hello"
- B: "world"
- C: "victory"
- D: "w"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The key information in the question above is about the method `Array.prototype.find()`. It returns the first element in the array that meets the condition declared in the callback function, which is passed to the function. The array is being iterated to check every single element. In the code above, we might easily see that the element `world` is the first element in the array that has a larger value than `victory`. Remember that "w" > "v" return trues if the two letters are compared. When two words are being compared, only the first letter in each word is being utilised to compare.

As the result, `found` is now `world` and thus `found[1]` returns the letter `w` whereas `www[0][0]` gives us the letter `h` in the element `hello`. It means `found[1] < www[0][0]` returns `false`.

So the final result is `www[true ? 0: 1]` or `www[0]`, which is `hello`. And the correct answer is A.

</p>
</details>

###### 52. What's the output?

```javascript
(function (flag) {
  let age = Boolean(NaN === NaN ? false : flag);

  console.log(age.toString()[Number(flag)]);
})([]);
```

- A: "f"
- B: "t"
- C: true
- D: false

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

We have a self-executing function with the parameter/argument is an empty array. Noted that `NaN === NaN` returns `false`, then `age` gets the value `flag`, which is an empty array. However, the boolean value is `true` when we call `Boolean([])`.

The function `toString()` returns the string `true` and the `Number([])` returns `0`. Then we get "t" in the console.log. The correct answer is B.

Keep in mind that `Boolean([])` ==> `true` but `Number([])` ==> `0`. And sadly `NaN === NaN` returns `false`.

</p>
</details>

###### 53. What's the output?

```javascript

1) console.log(Boolean([]));
2) console.log(Number([]));
3) console.log(Number(Boolean([])));
4) console.log(Boolean(Number([])));

5) console.log(Boolean({}));
6) console.log(Number({}));
7) console.log(Number(Boolean({})));
8) console.log(Boolean(Number({})));

9) console.log(Boolean(new Boolean(false)));

```

- A: true - 0 - 1 - false - true - 1 - 1 - false - false
- B: true - 0 - 1 - false - false - NaN - 1 - false - true
- C: true - 0 - 1 - false - false - false - 1 - false - false
- D: true - 0 - 1 - false - true - NaN - 1 - false - true

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

JavaScript is sometimes tedious to deal with given that it is a loosely type language. The data type of a variable can be changed depending on the value. An unexpected behaviour might unfortunately occur when you change/convert the original value to another one.

For example, the code 2 `Number([])` returns `0` and 6 `(Number({}))` returns `NaN`, although both `(Boolean([]))` and `(Boolean({}))` return `true`.

In the code 9 `Boolean(new Boolean(false))`, we get `true` even though we pass into the function constructor `Boolean()` a `false` (as the) parameter. However, if we do not use the keyword `new`, then `false` will return. It seems that in `Boolean(new Boolean(false))`, we have a valid opreration, so it is `true`. However, in the `Boolean(Boolean(false)))` where we do not use the keyword `new`, we then get `false` because now a `false` value is being evaluated rather than an operation.

So, the correct answer is D.

Credit: @tiepphan, Vietnamese Angular Facebook group.

</p>
</details>

###### 54. What's the output?

```javascript
const myYoutube = {
  name: "hoccoban",
  address: "youtube.com/hoccoban",
  getInfo() {
    return this;
  },
  content: () => (this === window ? myYoutube.getInfo() : this),
};

console.log(myYoutube.content().name);
```

- A: "hoccoban"
- B: window (object)
- C: NaN
- D: undefined

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

To answer the tricky question above, you might want to have a look at the concept of `this` in JavaScript (on browser environment). By default, `this` refers to `window` object. Note that `Window` (written in capital) is the Function constructor of the `window` object. In this regard, `console.log(this === window)` return true but `console.log(this === Window)` returns false.

As `content()` is an arrow function, `this` declared inside this function points to `window`, so `myYoutube.content()` returns `myYoutube.getInfo()`. Noted that we have to explicitly write `myYoutube.getInfo()` to make sure the code will run correctly as `this` in this case does not work as it does not refer to the currect object. In the function `getInfo()`, however, `this` actually refers to the currect object instead of `window` object because we use a normal function here.

Then we have the property `name` with the value "hoccoban". So the correct answer is A.

Credit: Thanks https://github.com/phanvigiaii for fixing the typo. Please make a pull request when you have time bro. Cheer.

</p>
</details>

###### 55. What's the output?

```javascript
const myArray = [1, 2, 3];

myArray.someProperty = this;

Array.prototype.someOtherProperty = "hello";

let result = [];

for (let key in myArray) {
  result.push(key);
}

for (let key in myArray) {
  if (myArray.hasOwnProperty(key)) {
    result.push(key);
  }
}

console.log(result.length);
```

- A: 10
- B: NaN
- C: 9
- D: 7

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

We have a simple array that consists of 3 elements. If checking the type of the array with the operator `typeof`, we will have `object`. (Hint, you can make use of `Array.isArray(array))` or `array instanceof Array` to check its type).

When declaring `myArray.someProperty`, we now add a new property to that array and when declaring `Array.prototype.someOtherProperty = "hello"`, we add a new property to every single array.

As a result, the `for... in` loop will iterate through the array in question and return its key/property and the inherited property as well. However, in the second iteration, we take advantage of the method `hasOwnProperty(key)` to check whether a particular key/property actually belongs to the array in question rather than the inherited one.

In short, in the first iteration, we get 5 (3 original ones, 1 property that is directly added to the array, 1 inherited from the Array.prototype. In the second one, we only get 4 as the inherited property is not taken into consideration.

Keep in mind that, we use `for... of` to loop through an array or the traditional `for` loop. It is not a good practice to use `for ... in` to loop through an array. It is often used to loop through an object.

</p>
</details>

###### 56. What's the output?

```javascript
const coderfarm = [1, 2, 3, 4, 5];

const [top, ...bottom] = (function (a) {
  let result = a;

  a.unshift(new Array(3));

  return result;
})(coderfarm);

console.log(top.length + bottom.length);
```

- A: 8
- B: 9
- C: 10
- D: 11

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

We are using destructure array (or object) technique to extract element of an array (or object). We also take advantage of `...` (spread parameter) here.

The array we are destructuring is returned from a self-executing function. First we pass the parameter `coderfarm`, which is the parameter `a` when declaring the function. Then we update this array with some additional value (an array with three `undefined` elements using `new Array(3)`) on the top of the array (using `unshift`). The array is updated now as `[[undefined, undefined, undefined], 1, 2, 3, 4, 5]`.

So `top` is the first element of the array or `[undefined, undefined, undefined]`, which returns 3 when we check the length.

The `bottom` returns the rest of the array in question, which is 5 when using `length` property.

The final number is 8 and thus the correct answer is A.

</p>
</details>

###### 57. What's the output?

```javascript
let age = { number: 10 };

const getAge = (flag) => {
  flag ? delete age.number : delete age;
  return age.number++;
};

console.log(getAge(false));

console.log(age.number);

console.log(getAge(true));

console.log(age.number);
```

- A: 10 - 10 - NaN - NaN
- B: 10 - 10 - undefined - undefined
- C: 10 - 11 - undefined - undefined
- D: 10 - 11 - NaN - NaN

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The operator `delete` only works on the property of an object, not the object itself. In the code snippet above, we have a simple function `getAge` with the parameter `flag`. When the `flag` is `true`, we trigger `delete age.number` and if it is `false`, we will use the operator `delete` upon the whole object.

As this operator does not work on an object, if we can say that, it turns out that `delete age` actually does nothing. As such, `console.log(getAge(false))` returns 10 and simultanously increases the value of `age.number` to 11. The value is now being kept in the memory. As such, `console.log(age.number)` will return 11.

When we pass the argument `flag` as `true` in the `console.log(getAge(true))`, we will trigger `delete age.number` which removes the value and the property `age.number` itself. It means `age.number` is now `undefined`. However, because we also attempt to increase the value of this `undefined` property using `++` operator, it returns `NaN`.

`console.log(age.number)` also returns `NaN` as well. So the correct answer is D.

</p>
</details>

###### 58. What's the output?

```javascript
const youtube = { name: "hoccoban" };

const copy = Object.create(youtube);

const cloneA = Object.assign({}, copy);

const cloneB = Object.assign({}, youtube);

console.log(cloneA.name);

console.log(cloneB.name);

console.log(copy.name);
```

- A: undefined - "hoccoban" - "hoccoban"
- B: "hoccoban" - "hoccoban" - "hoccoban"
- C: "hoccoban" - "hoccoban" - "undefined"
- D: undefined - "undefined" - "hoccoban"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

We have three outputs in the code snippet above.

First `console.log(cloneA.name);` will return `undefined` but why? We use `Object.assign` to clone a new object from an empty and from the object `copy`. The object `copy` itself is actually created from the original object `youtube` using `Object.create`. Noted that because we use `Object.create`, `copy` will inherit the data from the original one but it is still an empty object itself.

Second, both `console.log(cloneB.name)` and `console.log(copy.name)` return "hoccoban" because `cloneB.name` will have the actual property `name`. On the contrary, `copy.name` outputs the property `name` inherited from the `youtube`.

So the correct answer is A.

</p>
</details>

###### 59. What's the output?

```javascript
((x) => {
  const data = !Array.isArray(x) ? x : x.entries();

  console.log(data.next().value[1]);
})(["hello", "world", "vuong"]);
```

- A: NaN
- B: "hello"
- C: "world"
- D: "vuong"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

We have a self-invoking function here and we pass an array to it when the function is executed. Note that `Array.isArray(x)` return `true` but actually we use `!` before `Array.isArray(x)`. It means `data` will return `x.entries()`.

The method `array.entries()`, as you might have already known, returns a `gererator`. Here we will call `next()` to iterate through each element. Note that if you only call `next()` once, it will only return the first element instead of the whole iterator.

Then when we call `value`, it returns an array with the index and the value of the iterator. So what will we get if we call ` console.log(data.next().value[0])`. Sure, it returns `0` as `0` is the index.

So the correct answer is B.

</p>
</details>

###### 60. What's the output?

```javascript
let x = Symbol();

let y = Symbol();

console.log(x === y ? `${typeof x}`[1] : `${typeof x}`[2]);
```

- A: NaN
- B: "object"
- C: "y"
- D: "m"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

As `x` and `y` are both instances of `symbol`, they are unique in our codebase; therefore, the `===` comparison will return `false` as expected. In the simple code snippet above, we get the `else` operation.

It should be noted that the `typeof x` operation gives us `symbol`, and since a string in JavaScript is iterable, we get `m` as we pass in the index 2.

So the correct answer is D.

</p>
</details>

###### 61. What's the output?

```javascript
const frameworks = ["react", "angular", "vue"];

const iterator = frameworks[Symbol.iterator]();
const i = frameworks.entries();

iterator.next();
i.next();

console.log(iterator.next().value[1]);
console.log(i.next().value[1]);
```

- A: "react" - "angular"
- B: "react" - "react"
- C: "angular" - "angular"
- D: "n" - "angular"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

As `frameworks` is an array, it has a built-in method named `Symbol.iterator`. You can hence iterate through the whole array using commonly used methods such as `for... of`, normal `for loop`, `forEach` or `map`, among others. That is relatively trivial, I suppose.

This code challenge above is written to help us understand the concept of iteration better. First, we use the built-in method called `entries()` to create a new iteration. So does [Symbol.iterator](). Both seem to do the same thing.

Each time we call `next()` method, the iteration will output one element. We then can call `value()` to get the value. The difference between `iterator` and `i` is that the former shows the value itself while the latter outputs an array consisting of the index and the value. It means that in the code above, `iterator.next().value` returns `angular` and `i.next().value` gives us `[1, angular]`.

So the correct answer is D.

</p>
</details>

###### 62. What's the output?

```javascript
class React {
  theName = "Not React";
}

class Author extends React {
  static theName = "Real React";

  render() {
    return this.theName;
  }

  static render() {
    return this.theName;
  }
}

const me = new Author();

console.log(me.render());

console.log(Author.render());
```

- A: "Not React" - "Real React"
- B: "Not React" - Error
- C: Error - Error
- D: Error - "Real React"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

We have two classes in the code snippet above. It sounds we are imitating React. The `React` class has only one property named `theName,` and no method is declared here. Providing that `Author` extends the `React` class, it inherits that property, surely. However, we have also declared another property with the same name in the `Author` classs. The difference is that the property declared in the child class is given the keyword `static.`

The `Author` class also has two methods with the same name `render()`, one as regular methods and another with `static` keyword. Will that work in JavaScript?

It turns out that JavaScript is quite flexible. It supports both property and method if they are declared with the same name as long as they are either regular property (or method) or static property (or method).

The last thing you should be aware of is that the method `static render()` only calls the static property, here is `static theName = "Real React";` So does the regular method `render().` As such, the code does not run into any issues.

So the correct answer is A.

</p>
</details>

###### 63. What's the output?

```javascript
class js {
  say = "hello";
}

js.prototype.say = "goodbye";
console.log(new js().say);

js.prototype.thename = "google";
console.log(new js().thename);
```

- A: Error - Error
- B: "hello" - "google"
- C: "goodbye" - "google"
- D: Error - "google"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

`js` is a standard class declared in the code snippet above that has only one property with the name `say.` Then we again declare another property with the same name `say` for it. You might think that the property `say` has been overwritten with a new value `goodbye.`

That is not the case as we will get `hello` when we run `console.log(new js().say);`. It is clear that the JavaScript engine prioritizes the property declared inside the class more than the property declared later using the prototype mechanism.

If the property has not been declared inside the class itself, we can then add a new one with the help of `prototype` as in `thename`. Without the doubt, the code `console.log(new js().thename);` gives us `google` as expected.

So the correct answer is B.

</p>
</details>

###### 64. What's the output?

```javascript
const App = ([y, x, z]) => {
  return () => {
    ++x;
    return () => {
      return x++;
    };
  };
};

console.log(App([10, 20, 30, 40])()());
```

- A: 10
- B: 32
- C: 21
- D: 22

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

To answer the question raised on the above code snippet, you might want to revisit two concepts, `currying function` and `destructing array or object.`

First, `currying function` means we convert a function with multiple parameters into multiple functions with a SINGLE parameter. Then you can easily manipulate the flow of the data. Noted that `currying function` is relevant to `higher-order function`, you might want to have a look.

`destructing array or object` means we attempt to extract a complex array or object more conveniently. For example, `[y, x, z] = [10, 20, 30, 40]` will extract y, x and z with the value 10, 20 and 30 respectively.

The last thing is incremental operator here `++x` returns 21 but `x++` does not as it still returns 21.

So the correct answer is C.

</p>
</details>

###### 65. What's the output?

```javascript
const numbers = [5, 6, 7];

function callback(accumulator, currentValue) {
  return accumulator + currentValue;
}

const theCallBack = (accumulator, currentValue) => accumulator + currentValue;

const sum = numbers.reduce(
  callback,
  numbers.reduce(theCallBack, numbers.reduce(theCallBack, 7))
);

console.log(sum);
```

- A: 54
- B: 55
- C: 60
- D: 61

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

`Array.prototype.reduce()` is a bit perplexed built-in method that allows you to manipulate data in an array. It returns a single value from the array predefined as in the case with `map` or `filter`. The syntaxt of the function is `arr.reduce(callback( accumulator, currentValue, [, index[, array]] )[, initialValue])`, so it accepts a callback function with four arguments including `accumulator`, `currentValue`, `currentIndex` (optional) and `array` (optional).

The second argument of the `reduce` method, which is optional, is called `initialValue` that will be counted as the first element with the index 0 when `reduce` is executing. If `initialValue` is not provided, then `reduce` will run with the index 1 instead. `reduce()` sounds complicated, but truly it is not. In case you want to revise the function, kindly take a look at MDN here: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce

The above code has two callback functions named `callback` and `thecallback`, which do the same thing. The seemingly creepy code is the variable `sum`, which is returned by a couple of nested `reduce` functions. It turns out that there is only one "real" `reduce` function and the other ones give us `initialValue` only.

- The first `initialValue` is 7;
- The first nested `reduce` function gives us 7 (initialValue) + 5 + 6 + 7 = 25.
- The second nested `reduce` has 25 as the initialValue, which we get from the above. Then it returns 25 + 5 + 6 + 7 = 43;
- The "real" `reduce` function now has 43 as the initialValue, the we get the final result: 43 + 5+ 6 + 7 = 61.

So the correct answer is D.

</p>
</details>

###### 66. What's the output?

```javascript
const a = { name: "hoccoban.com" };
const b = { name: "youtube.com/hoccoban" };

const first = { ...a }.name.length;
const second = { ...a, ...b }.name.length;
const third = { ...a, ...b, name: "hello" }.name.length;

console.log(first + second + third);
```

- A: 12
- B: 37
- C: 5
- D: 20

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

The code snippet above is relatively trivial. What we can learn from it is all about the `spread operator` (three-dot ...). Sometimes it is also used as a `rest operator` to extract data from an object or array.

We have two simple objects which both have the same key `name` but different values. The constant `first` gives us the length of the string value of the keyword `name` that is copied from `a`. So, `first` is now 12.

The constant `second` merges `a` and `b` into one object. However, as `b` has the same key `name` with `a`, the object created by merging two objects will have the value of `b`. It means the constant `second` gives us the length of `youtube.com/hoccoban`, which is 20.

`third` does the same thing with `first` and `second` as it merges two objects into one. However, it also adds another key-value to the object. Coincidently, the key now is `name`, which is the same with the key attained from `a` and `b`. Hence, this key and value will take over the merged object. That means `third` is the length of the string `hello`, which is 5.

In total, we have 12 + 20 + 5, and the final result is 37.

So the correct answer is B.

</p>
</details>

###### 67. What's the output?

```javascript
const hocCoBan = {};

Object.defineProperty(hocCoBan, "domain", {
  value: "hoccoban.com",
});

async function App({ year, age }) {
  return year - age + hocCoBan.domain.length;
}

App({ year: 2021, age: 30 }).then((r) => console.log(r));
```

- A: 2051
- B: 2001
- C: 30
- D: 2003

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The code snippet above seems complicated regarding how we take advantage of `Object.defineProperty` to add key and value to the object `hocCoBan`. In fact, `Object.defineProperty` has a couple of handy features that allow us to control the behavior of the object in some situations where we want to make sure that the object created is mutable or not, whether it is iterable (using `for..in`) and so for. For example, if we set `configurable: false` when we declare an object with `Object.defineProperty`, we cannot use `delete` operator to delete the object's property. We cannot change the value of that property as well.

The second "take away" message when reading the code above is the unpacking object technique, or a more frequent term is the destructing object. Say you have an object with two keys called `year` and `age`, then you can get them by using the destructing object technique as follows: `{year, age} = theOBject;`. In the code above, when declaring the function `App`, we also use destructing object technique to get the key from the object and use them as the parameters.

If you are familiar with asynchronous code in JavaScript when using the keyword `async,` it is not a big deal to understand why we need to use `then` to get the function `App` being called. It fact, `async` always returns a promise, so we need to use `then` method to get the data we want.

The flow of the code is: 2021 - 30 + `"hoccoban.com".length` (which is 12).

The final result is 2003. So the correct answer is D.

</p>
</details>

###### 68. What's the output?

```javascript
class hoccoban {
  #thisyear = 2021;
  constructor(covidTheFirstYear) {
    this.covidTheFirstYear = covidTheFirstYear;
  }

  getThisYear() {
    return this.#thisyear;
  }

  getCovidFirstYear() {
    return this.covidTheFirstYear;
  }
}

const message = new hoccoban(2019);

const result =
  hoccoban.hello ?? message.getThisYear() - message.getCovidFirstYear();

console.log(result);
```

- A: NaN
- B: 2019
- C: undefined
- D: 2

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

This challenge partly illustrates the newest features of JavaScript detailed in ECMAScript 2020 or ES11.

Now you can declare a private property in a class thanks to the symbol `#`. Like other languages, a private property in JavaScript can only be accessed from inside the class. It will trigger an error when you attempt to call it outside the class, surely.

The second feature you might see on the code snippet above is the `nullish coalescing operator` or `??`. When declaring some variable such as `let myVariable = number ?? 7`, if the variable `number` is either `undefined` or `null`, the variable `myVariable` will be assigned the value `7`.

So `hoccoban.hello` means `undefined` because we have not added any value yet. Then by using `nullish coalescing operator` with `??` the variable `result` simply returns 2 as `message.getThisYear()` gives us 2020 and `message.getCovidFirstYear()` gives us 2019. Note that we can access the private property outside of the class via a method, as in the method `getThisYear()`.

So the correct answer is D.

</p>
</details>

###### 69. What's the output?

```javascript
const keyWords = "hello world";

const entries = keyWords.split(" ");

const collections = [];

entries.forEach((entry, index) => {
  collections.push([entry, index]);
});

const objectResult = Object.fromEntries(collections);

const { world } = objectResult;

console.log(world);
```

- A: 0
- B: true
- C: 1
- D: "hello"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The code snippet above is not challenging for those who have had decent experience working with ES6 I suppose. First we turn `keywords` into an array using `split()` function. Then we create a variable named `collection`, which initially is an empty array.

Take a closer look at the `forEach` function, which allows us to run a for loop through the whole array `entries`, you might realize that `push([entry, index]);` add an array to `collections` rather than an element.

The next step is by taking advantage of `Object.fromEntries()` that converts an array with at least two elements (the form of key-value) to an object. This built-in method is the reversing version of `Object.entries()`, which extracts key and value from an object to an array.

`const { world } = objectResult;` is nothing special as we unpack the object using destructing object technique supported since ES6. As the object `objectResult` has `hello` and `world` with two respective values 0 and 1, we get 1 when printing out `world`, so the correct answer is C.

</p>
</details>

###### 70. What's the output?

```javascript
const target = {
  domainname: "hoccoban.com",
  author: "vuong",
};

const handler = {
  get: function (thetarget, prop, receiver) {
    if (prop === "domainname") {
      return thetarget.author.length;
    } else {
      return thetarget.domainname.length;
    }
  },
};

const proxyObject = new Proxy(target, handler);

console.log(proxyObject.domainname > proxyObject.author);
```

- A: true
- B: false
- C: 12
- D: 5

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

We have implemented a basic use case of `Proxy` in the code snippet above. Each `proxyObject` object has two parameters (`target` and `handler`). `handler` is also an object.

Apart from `get()` as you might see, `handler` also has a handful of other methods such as `set`, `defineProperty()`, `has()` and so forth. Sometimes, people may say a `method is a trap` of a proxy object.

Back to the code above, the `get` method allows us to modify how the proxy object will display the value of the original object. `thetarget` is the original object, and `prop` is the property of that object as you might guess. You might choose another name in the `get` function if you want when creating your handler.

The `handler` above calculates the length of the string value of the two properties. Based on the flow of `if - else` code, it swaps the returned value.

So `proxyObject.domainname` now should be understood as `target.author.length` which means 5 and `proxyObject.author` means `target.domainname.length` which gives us 12. So the output is `false`. The correct answer is B.

If you do the same thing with the original, it should be something like `console.log(target.domainname.length > target.author.length)` which returns `true`.

I believe that `Proxy` is worth to have a closer look. If that is the case, no place is better than MDN. So have a go at: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy

</p>
</details>

###### 71. What's the output?

```javascript
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => resolve("hello"), 5000);
});

const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => resolve("world"), 4000);
});

(async () => {
  console.time("timeleap");

  const p1 = await promise1;

  const p2 = await promise2;

  console.log(`${p1} ${p2}`);

  console.timeEnd("timeleap");
})();
```

- A: Promise { <pending> } - "hello world" - timeleap: ~ 5000 ms
- B: Promise { <pending> } - "hello world" - timeleap: ~ 9000 ms
- C: Promise { <pending> } - "hello world" - timeleap: ~ 4000 ms
- D: Promise { <pending> } - "hello world" - timeleap: ~ 1000 ms

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

We have already had a couple of questions regarding asynchronous code in general and handling the data flow with promise in particular. If you understand how JS works, I am sure that the code challenge above is not difficult.

We have two promises; each takes 5 or 4 seconds to complete the code and returns "hello" (in `promise1`) and "world" (in `promise2`) in the `resolve` methods, respectively.

Then we take advantage of the `async` function to chain the two promises to get the result we want. As `async` function returns a `promise` so to get the returned value from `async` function, we have to use `then()` method. As we do not do that here, then we get `Promise { <pending> }`.

The question is, does `p2` have to wait and only run after `p1` complete? It turns out that it does not. Both `p1` and `p2` run simultaneously in the task queue thanks to web API or nodejs API (the environments by which JavaScript engine runs). So it will not take 9 seconds to finish the code but solely around 5. It means `promise1` takes 5 seconds to complete and at the same time, `promise2` reaches the bottom within only 4 seconds.

That is why A is the correct answer.

Updated: What happens if `promise2` takes 6 seconds instead of 4 ? Well, as `promise2` runs almost at the same time with `promise1`, it will only take 1 second after the `promise1` completes. So in total, it takes approximately 6 seconds.

</p>
</details>

###### 72. What's the output?

```javascript
const promise1 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve("hello"), 5000);
  });
};

const promise2 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve("world"), 4000);
  });
};

(async () => {
  console.time("timeleap");

  const p1 = await promise1();

  const p2 = await promise2();

  console.log(`${p1} ${p2}`);

  console.timeEnd("timeleap");
})();
```

- A: Promise { <pending> } - "hello world" - timeleap: ~ 5000 ms
- B: Promise { <pending> } - "hello world" - timeleap: ~ 9000 ms
- C: Promise { <pending> } - "hello world" - timeleap: ~ 4000 ms
- D: Promise { <pending> } - "hello world" - timeleap: ~ 1000 ms

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

The 72nd challenge is almost identical to the 71st. Please take a closer look.

The difference lies in the way we declare a promise. In question 71st, we use two constants, and both return promise, but in question 72, we declare functions and each returns a promise.

If you run the code, you might be surprised with the result as it takes around 9 seconds to complete the code in place of 5 seconds as in the previous question.

It means that `const p1 = await promise1;` and `const p1 = await promise1();` are different as the latter (a function) might block the callstack and `const p2 = await promise2();` can only be called after the `p1` completes. The two do not run in parallel as the two promises in the previous question.

As it takes 9 seconds to finish, B is the correct answer.

</p>
</details>

###### 73. What's the output?

```javascript
let history = {
  year: 2021,
  getYear: function () {
    console.log(this.year);
  },
};

setTimeout(history.getYear, 0);
setTimeout(history.getYear.bind(history), 10);

const { year, getYear } = history;
getYear();
```

- A: undefined - undefined - 2021
- B: undefined - 2021 - 2021
- C: 2021 - undefined - 2021
- D: 2021 - 2021 - 2021

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

We have three outputs on the code above. First, we have a simple object with one property and one method. Noted that the method point to the property `year` using `this` keyword. The problem now happens when we attempt to extract data from the object.

Be aware of the `setTimeout` method, which will create a separated context that is different from the original object's context. Even though in `setTimeout(history.getYear, 0);` we have explicitly called the object `history`, setTimeout will still execute the function `history.getYear` with`this` pointing to the global object. So it returns `undefined.`

`getYear();` is extracted from the object we have defined in the beginning. But as `this` is out of the original context when executing the function, it returns `undefined`. This code is called last, but the output is displayed first on the console window as it is a synchronous code.

`setTimeout(history.getYear.bind(history), 10);` runs last and will give us 2021 as it is bound to the object `history`. Finally, we get `undefined - undefined - 2021,` and A is the correct answer.

</p>
</details>

###### 74. What's the output?

```javascript
class handleCovid {
  constructor(start) {
    this.start = start;
  }

  calculate(someValue) {
    this.start = this.start + someValue;
    return this.start;
  }

  vaccine() {
    ++this.start;
    return this;
  }

  delaying() {
    ++this.start;
    return this;
  }

  static getFinal(result) {
    return result * 2;
  }
}

const now = new handleCovid(2019);

console.log(handleCovid.getFinal(now.vaccine().delaying().calculate(2020)));
```

- A: 2019
- B: 8082
- C: 8080
- D: 8084

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

The code snippet above is ugly and sounds complicated at first. Yet, you might encounter a situation when some good "take away" messages might be given. The flow of the code is not hard to understand, I suppose.

First, a function in JavaScript can accept another function as its parameter. With regard to the `static` keyword, it means we can directly call a static method in the form of `className.staticmethod` without invoking the object created by the normal way `new ClassName`.

Besides, you might want to have a look at how we chain more than one method together. That is possible if these methods `return this`.

Now let break it down:

- `calculate(2020)` --> 2019 + 2020 = 4039;
- `delaying().calculate(2020)` --> 4040;
- `now.vaccine().delaying().calculate(2020)` --> 4041;
- `handleCovid.getFinal(now.vaccine().delaying().calculate(2020)` --> 4041 \* 2 = 8082;

So the correct answer is B.

</p>
</details>

###### 75. What's the output?

```javascript
function HappyNewYear() {
  return "hello";
}

const year2021 = new HappyNewYear();
year2021.__proto__.greeting = "happy";
HappyNewYear.prototype.say = "new year";

console.log(year2021.__proto__ === HappyNewYear.prototype);
console.log(Object.getPrototypeOf(year2021) === HappyNewYear.prototype);
console.log(Reflect.getPrototypeOf(year2021) === HappyNewYear.prototype);

console.log(year2021.__proto__ === Object.prototype);
console.log(year2021 instanceof HappyNewYear);
console.log(year2021 instanceof Object);

const thisyear = new HappyNewYear();
console.log(`${thisyear.greeting} ${thisyear.say}`);
```

- A: true - true - true - false - true - false - "happy new year"
- B: true - true - true - false - false - true - "happy new year"
- C: true - true - true - true - true - true - "happy new year"
- D: true - true - true - false - true - true - "happy new year"

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The code snippet above helps us revise the concept of `prototype` in JavaScript with two essential keywords: `__proto__` and `FunctionName.prototype`. I believe that the code `console.log(year2021.__proto__ === HappyNewYear.prototype);` is the key to understand the difference between the two. So, in short, every single object in JavaScript has a built-in property `__proto__` that gives us an overview of the built-in (internal) [[Prototype]]. They are the things (property and method) the object inherits from the "parent" function constructor or class).

For example, if you declare a literal object such as `const a = {}` then `a.__proto__ === Object.prototype` returns `true` because `a` inherits the prototype from the "parent" `Object`. However, if an object is created using function constructor then the "parent" prototype is function constructor itself instead of the `Object`. So while `console.log(year2021.__proto__ === HappyNewYear.prototype);` returns `true`, `console.log(year2021.__proto__ === Object.prototype);` gives us `false`.

Be aware of `Object.getPrototypeOf (object)` and `Reflect.getPrototypeOf(object)`. The two are recommended to use as `__proto__` is being deprecated.

You might want to read more about `__proto__` at MDN https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/proto

The correct answer is D, and btw "happy new year"!

</p>
</details>

###### 76. What's the output?

```javascript
const address = {
  name: "hoccoban.com",
  author: "Vuong Nguyen",
};

const key = Reflect.has(address, "author")
  ? Reflect.ownKeys(address)[0]
  : "hello";

Reflect.set(address, "language", "JavaScript");

const totalKeys = Reflect.ownKeys(address).length;

const name = Reflect.get(address, key).length;

const language = Reflect.get(address, "language").length;

console.log(totalKeys + name + language);
```

- A: 22
- B: 10
- C: 20
- D: 25

<details><summary><b>Answer</b></summary>
<p>

The correct answer is D. Why? Now let break it down:

- `Reflect.has(address, 'author')` gives us `true` given that the object `address` has the key `author`. Simple as it is. So the value of the variable `key` is now `Reflect.ownKeys(address)[0]`, which in fact is the key `name`.

- `Reflect.set(address, 'language', 'JavaScript');` set another key-value to the object `address`.

- `Reflect.ownKeys(address).length;` gives us 3 because now it has three keys, so `totalKeys` is now 3.

- `Reflect.get(address, key).length;` gives us the length of the string `hoccoban.com` which is 12.

- `Reflect.get(address, 'language').length` is the length of the string `JavaScript`, which is 10.

- The final answer is 3 + 12 + 10 = 25.

#### Answer: D

</p>
</details>

###### 77. What's the output?

```javascript
const myModule = (function () {
  const covidYear = 2019;

  const year = 2021;

  function getYear() {
    return year;
  }

  function getCovidYear() {
    return covidYear;
  }

  function exposeYear() {
    return getYear();
  }

  function exposeCovidYear() {
    return getCovidYear();
  }

  return {
    nothing: undefined ?? null ?? null ?? undefined,
    exposeYear,
    exposeCovidYear,
  };
})();

const result =
  myModule.nothing ?? myModule.exposeYear() + myModule.exposeCovidYear();

console.log(result);
```

- A: 2021
- B: 2019
- C: 4040
- D: undefined

<details><summary><b>Answer</b></summary>
<p>

The challenge above will help you revise the `revealing pattern` and thanks to it you can declare a private variable in JavaScript. Note that we can now declare a `private` property in a class in modern JavaScript, so the above way of writing a private variable seems old-fashioned.

First, we have an IIFE function - immediately invoked function expressions. There are two variables and two functions as well. However, in the `return`, there are three key-values. We can not directly access the two variables `covidYear` and `year` except for using some already-built functions inside the IIFE.

If you feel the keyword `??` is odd, then you might want to have a look at the latest syntax supported in modern JavaScript called "Nullish Coalescing Operator". It means, if the left element is either `undefined` or `null`, the value of the right element will be assigned.

In short, we have `myModule.exposeYear()` (2021) and `myModule.exposeCovidYear()` (2019). In total, the final result is 4040. So the correct answer is C.

#### Answer: C

</p>
</details>

###### 78. What's the output?

```javascript
class HocCoban {
  constructor(address) {
    this.address = address;
    this.youtube = "";
  }
  get getAddress() {
    return this.address;
  }

  set setYoutube(channel) {
    this.youtube = channel;
  }

  getYoutube() {
    return this.youtube.length;
  }
}

const web = new HocCoban("hoccoban.com");

web.setYoutube = "youtube.com/hoccoban";

console.log(web.getAddress);

console.log(web.youtube);

console.log(web.getYoutube());
```

- A: "hoccoban.com" - "youtube.com/hoccoban" - 20
- B: "hoccoban.com" - function() - 20
- C: function() - "youtube.com/hoccoban" - 20
- D: function() - function() - 20

<details><summary><b>Answer</b></summary>
<p>

`set` and `get` are commonly called setter and getter. When declaring a method in a class and putting the keyword `set` or `get` before it, you can then call them without using `parenthesis - ()`. Put another way, when using `get` and `set`, you can directly get or set the value of/for the properties. Somehow it might be convenient in some cases.

Be aware of the methods declared with a `getter` as we just need to call the method as we call a property (without using parenthesis).

If you know how a traditional method works in JavaScript, then the code challenge above is not difficult, I suppose. The answer is A.

#### Answer: A

</p>
</details>

###### 79. What's the output?

```javascript
const result = ["ronaldo", "messi", "neymar", "Ronaldo", "LuKaKUUUU"].sort();

console.log(result);
```

- A: ["LuKaKUUUU", "Ronaldo", "messi", "neymar", "ronaldo"]
- B: ["LuKaKUUUU", "messi", "neymar", "Ronaldo","ronaldo"]
- C: ["LuKaKUUUU", "messi", "neymar", "ronaldo", "Ronaldo"]
- D: ["messi", "neymar", "ronaldo", "Ronaldo", "LuKaKUUUU"]

<details><summary><b>Answer</b></summary>
<p>

In JavaScript, the built-in `sort()` method sorts the elements of an array. It returns a sorted array in ascending order. Note that each element will be converted to strings and then compared according to the sequences of UTF-16 code unit values. What does it mean?

It means, "banana" < "cherry" or 80 < 9 (because "80" < "9" in the Unicode order).

If you run the following code `const result = [9, 11, 89].sort();`, the constant `result` will be sorted as `[11, 8, 9]` rather than `[9, 11, 89]` because the engine will convert the number value to string.

The following codes might give you a hint about the relationship between character and number. Ultimately, as the computer can only understand 0 and 1, all characters and even decimal numbers are then converted to 1 and 0. `charCodeAt()` gives us the decimal value of any string evaluated.

`console.log("LuKaKUUUU".charCodeAt(0))` or `console.log("LuKaKUUUU".charCodeAt())` ==> 76
`console.log("Ronaldo".charCodeAt(0))` or `console.log("Ronaldo".charCodeAt())` ==> 82
`console.log("messi".charCodeAt(0))` or `console.log("messi".charCodeAt())` ==> 109
`console.log("neymar".charCodeAt(0))` or `console.log("neymar".charCodeAt())` ==> 110
`console.log("ronaldo".charCodeAt(0))` or `console.log("ronaldo".charCodeAt())` ==> 114
`console.log("9".charCodeAt())` or `console.log("99".charCodeAt())` ==> 57
`console.log("80".charCodeAt())` or `console.log("8".charCodeAt())` ==> 56

Noted that if index is not a number, it defaults to 0. The answer is A.

#### Answer: A

</p>
</details>

###### 80. What's the output?

```javascript
const anArray = typeof [];
const aTypeOfNull = typeof null;

const weirdFirst = null instanceof Object;
const weirdSecond = [] instanceof Object;
const weirdThird = [] instanceof Array;

console.log(anArray);
console.log(aTypeOfNull);

console.log(weirdFirst);
console.log(weirdSecond);
console.log(weirdThird);
```

- A: "array" - "null" - false - true - true
- B: "array" - "object" - false - true - true
- C: "object" - "object" - false - false - true
- D: "object" - "object" - false - true - true

<details><summary><b>Answer</b></summary>
<p>

In the 80th challenge question, we will review some fundamental "issue" or "weird" features in JavaScript relating to the `typeof` and `instance` operators. Given that the original version of the JavaScript language was designed in just 10 days, there are a bundle of inconsistent behaviors that cannot be fixed. They are permanent features existing in the modern language. If we fix it, a lot of websites might crash.

The above code shows us some of the weird features in JavaScript. For example, `[]` is an array but the `typeof []` gives us `object`. Note that you might take advantage of `Array.isArray([])` rather than `typeof` to examine whether a variable is an array or not.

`typeof null;` is another weird operator as it returns `object`. However `null instanceof Object;` returns `false`. ~WhatTheHell~!!!

Man, `[] instanceof Object;` and `[] instanceof Array;` both return `true`. How inconsistent it is.

The answer is D.

#### Answer: D

</p>
</details>

###### 81. What's the output?

```javascript
class Dog {
  speak() {
    return this.say();
  }

  say() {
    console.log("hello world");
  }
}

class Cat {
  speak() {
    return this.say();
  }

  say() {
    console.log("kia ora");
  }
}

const animal = new Dog();
animal.speak();
Object.setPrototypeOf(animal, Cat.prototype);
animal.speak();
```

- A: "hello world" - undefined
- B: "kia ora" - "kia ora"
- C: "hello world" - "kia ora"
- D: "hello world" - "hello world"

<details><summary><b>Answer</b></summary>
<p>

The central issue/concept mentioned in the code above is the method `Object.setPrototypeOf(object, prototype)`. It is one of the features in ES6, or ECMAScript 2015. Another way to set the prototype of an object is `Object.prototype.__proto__` but the latter is controversial.

At first, `animal.speak();` gives us "hello world" which is no surprise. Yet, in the second call, we get "kia ora" instead of "hello world". When checking the prototype with `Object.getPrototypeOf(animal)`, you might see that `Cat` is the prototype of the object `animal` rather than `Dog`.

The answer is C.

By the way, `kia ora` means `hello` in the Māori language.

#### Answer: C

</p>
</details>

###### 82. What's the output?

```javascript
const js = [9, 10];

function mutate(a, b) {
  a.push(b);
}

mutate(js, 1);
console.log(js);
```

- A: [9, 10]
- B: [9, 10, 1]
- C: [1, 9, 10]
- D: ReferenceError

<details><summary><b>Answer</b></summary>
<p>

The code snippet might be pretty trivial if you have already obtained a solid understanding of the two different concepts: `reference` and `value.` In JavaScript, non-primitive type such as array and object does not store the value but the reference.

Also, as the arguments in function are passed by the reference, the function `mutate` will push another element into the array `js`. Finally, the initial variable 'js' is updated with the new value `[9, 10, 1]`.

If the variable `js` is assigned a primitive value such as string or number, no matter how the function `mutate`, it will not mutate the initial variable 'js'. However, if the variable is an object, then it will also be mutated, as in the case of an array in the code above.

B is the correct answer.

#### Answer: B

</p>
</details>

###### 83. What's the output when running the code on a browser?

```javascript
console.log(this === window);
console.log(this === frames);
console.log(this === globalThis);
console.log(this === self);
console.log(this === global);
```

- A: true - true - true - true - "ReferenceError"
- B: true - false - true - true - "ReferenceError"
- C: true - true - true - true - true
- D: true - true - "ReferenceError" - true - "ReferenceError"

<details><summary><b>Answer</b></summary>
<p>

The code snippet above might output different results if running on other environments than the browser. For example, there is no `self`, `window`, or `frames` on Nodejs.

`global` plays the role of the global object in Nodejs, but that is not the case in the browser environment. In contrast, `globalThis` is available in both browser and Nodejs environments.

The first takeaway message is that Nodejs does have `this`, `global`, and `globalThis`. Browser environment has 5 ones including `this`, `globalThis`, `window`, `frames`, and `self`.

The second takeaway message is that Web Worker only has `self` as the global object.

Ultimately, A is the correct answer.

#### Answer: A

</p>
</details>

###### 84. What's the output ?

```javascript
class StackHocCoBan {
  constructor() {
    this.stack = [];
  }

  push(thing) {
    return this.stack.push(thing);
  }

  pop() {
    return this.stack.pop();
  }

  peek() {
    return this.stack[this.length - 1];
  }

  get length() {
    return this.stack.length;
  }

  isEmpty() {
    return this.length === 0;
  }
}

const firstThing = new StackHocCoBan();

firstThing.push(firstThing.length);
firstThing.push(firstThing.length);
!firstThing.isEmpty() ? firstThing.push(firstThing.length) : firstThing.length;
firstThing.pop();

console.log(firstThing.peek() + firstThing.length + firstThing.pop());
```

- A: 3
- B: 4
- C: 5
- D: 6

<details><summary><b>Answer</b></summary>
<p>

The code challenge above is a bit lengthy, frankly. But it might practically help you to revise the concept of `stack` implemented in JavaScript. Such a concept is quite crucial when it comes to the algorithm, so to say. It appears that `stack` and `queue` are blood brothers, and as a developer, you are always advised to master these concepts along with array, linked list, tree, graphs, and so on.

In my opinion, both `stack` and `queue` are simply arrays, but they are exclusively built to serve some particular jobs with strict requirements. You might see `pop()` or `push()` in the code above are standard native methods we often use when working with the array.

So now `firstThing` is an object initiated by the class `StackHocCoBan`. As the class's construct initially triggers an empty array ` this.stack = [];`, first the code `firstThing.push(firstThing.length);` will actually push the number 0 into the array given that `firstThing.length` returns 0 as the stack, at the beginning` is empty.

Then `firstThing.push(firstThing.length);` (the second one) pushes number 1 to the stack as we have already had one item (the number 0).

`firstThing.isEmpty()` returns `false` because we have two things in the stack. Yet, be causious with "!" before it. As we write `!firstThing.isEmpty()`, the code with call `firstThing.push(firstThing.length)` rather than `firstThing.length;`. It is a simply short-hand of `if-else`.

So, the stack is pushed the number 2 because `firstThing.length` returns 2. So now the stack is as [0, 1, 2], beautiful, right?

`firstThing.pop()` will eliminate the number 2 and the stack is now [0, 1].

The last line of the code above is `firstThing.peek()` (1) + `firstThing.length` (2) + `firstThing.pop()` (1).

So B is the correct answer.

#### Answer: B

</p>
</details>

###### 85. What's the output ?

```javascript
class QueueHocCoBan {
  constructor() {
    this.queue = [];
  }

  enqueue(item) {
    return this.queue.unshift(item);
  }

  dequeue() {
    return this.queue.pop();
  }

  peek() {
    return this.queue[this.length - 1];
  }

  get length() {
    return this.queue.length;
  }

  isEmpty() {
    return this.queue.length === 0;
  }
}

const items = new QueueHocCoBan();

items.enqueue("constructor");
items.enqueue("QueueHocCoBan");
items.enqueue("hoccoban.com");

const item = items.peek().length - items.length;

console.log(item);
```

- A: 6
- B: 7
- C: 8
- D: 9

<details><summary><b>Answer</b></summary>
<p>

Following up the question 85th, we now pay the attention to another important concepts - `queue` - which is a bit different from `stack`. While `stack` leverages two native array methods `push()` (for adding new item) and `pop()`(for extracting new item), `queue` utilises `unshift()` (for adding new item) and `pop()` (for extracting new item). In essense, both `stack` and `queue` are array and thus the difference between them, IMO, lays in the way `push()` and `unshift()` are implemented for adding new item. While `push()` adds a new item/element at the end/tail of the array, `unshift()` adds the new one to the top/head of the array itself.

First, the object `items` will add three new elements into the array (initiated by the constructor) at the top one by one, thanks to the method `enqueue`. The array will look like this ["hoccoban.com", "QueueHocCoBan", "constructor"];

Now `items.peek()` gives us "constructor" and thus `items.peek().length` returns 11. `items.length` simply returns 3 and so the final result will be 8.

So C is the correct answer.

By way of summarisation, using `queue`, we can only take out the first element (also the tail of the array) with the method `dequeue().` You might need to find another way to extract other elements of the queue.

#### Answer: C

</p>
</details>

###### 86. What's the output ?

```javascript
const domains = new Map();

domains.set("site", "hoccoban.com");
domains.set("youtube", "youtube.com/hoccoban");

const keys = domains.keys();
const values = domains.values();

let result = domains.has("hoccoban.com")
  ? values.next().value
  : keys.next().value;

console.log(result);
```

- A: "site"
- B: "hoccoban.com"
- C: "youtube"
- D: "youtube.com/hoccoban"

<details><summary><b>Answer</b></summary>
<p>

There are two ways hash tables are implemented in JavaScript: object and Map(). Hash tables are data structures created to store information in the form of key-value.

While the native object defined as {} is trivial for a JavaScript developer, a new way to design a hash table has been recently added into the language. When writing `const domains = new Map();`, we have declared an object with a couple of different features as opposed to the veteran one declared in the form of `{}` or `new Object` we all know.

You are advised to take advantage of the built-in methods such as `set()`, `get()`, `has()` or `delete()` among others to manipulate the map object.

Note that a map object can be iterated using `for of`. You might need to use `next().value` to extract the raw information written. At this point, you might want to revisit `function generator` to see why we need to do that.

Both `keys()` and `values()` are native methods of the class `Map`. You might see that they works on a map object as in a normal object. Back to the code snippet above, `let result = domains.has("hoccoban.com") ? values.next().value: keys.next().value` returns `keys.next().value` given that `domains.has("hoccoban.com")` returns `false`.

So `console.log(result)` gives us "site", so A is the correct answer.

Note that if you want to extract "youtube", you must run `keys.next().value` twice.

#### Answer: A

</p>
</details>

###### 87. What's the output ?

```javascript
function inner(flag) {
  hello = 10;
  if (flag) {
    return ++hello;
  }
  return --hello;
}

var hello = 12;
inner(hello > 11 ? false : true);
console.log(hello);
```

- A: 9
- B: 10
- C: 11
- D: 12

<details><summary><b>Answer</b></summary>
<p>

As a variable in JavaScript can be declared without any functional keyword such as var, let, or const standing before the variable name, as seen on the code above, this challenge sounds a bit odd as now developers tend to use `const` or `let` everywhere. What happened when we do that? The variable will have a global scope no matter where it has been written initially. So first, the variable `hello` will be accessed anywhere outside of the function scope whenever (after to be exact) the function inner has been executed.

Then we redeclare the `hello` variable with a different value.

The code `inner(hello>11? false: true)` is translated to `inner(false)`, so the variable `hello` declared inside this function is mutated to 9.

As `hello` is now 9 instead of 12, A is the correct answer.

#### Answer: A

</p>
</details>

###### 88. What's the output ?

```javascript
const collections = ["a", [123], true, "c", { abc: "hello world" }];
const iterator = collections.values();

const a = iterator.next().value.length;
const b = iterator.next().value.length;
const c = iterator.next().value.toString().length;
const d = iterator.next().value.length;
const e = Object.values(iterator.next().value)[Number(a > b)].length;

console.log(a + b + c + d + e);
```

- A: 12
- B: 14
- C: 16
- D: 18

<details><summary><b>Answer</b></summary>
<p>

The code snippet above is frankly tedious as it does not solve any big problem but is still written in a very cryptic manner, honestly. I want you to pay a bit more attention to the native function to manipulate array `values()`. For your information, I also use `Object.values()` so that you can somehow make a comparison between the two by yourself.

In the beginning, we have a very simple array packed with different types of data such as boolean, string, array and object. The code `collections.values();` returns an iterator, so you can not simply access to each element as an usual array. You might run a `for of` loop here to render all of the elements in this iterator. By doing that, the way iterator works is likely a typical array.

So how do we access a single element in this iterator? We need to use `next().value`. Each time we call it, the iterator will render the value, one by one, starting with the first element.

It means `const a = iterator.next().value.length;` returns 1. So a is 1. So does b. C is a bit different and we have 4 here as `true`, a boolean, is converted to a string. d is 1. So

The code in e is not fascinating, I suppose. `Object.values` gives us an array of value defined in the object `{ abc: "hello world" }`. `[Number(a > b)]` give us [0]. So e is simply the length of the string "hello world", which is 11.

Finally, in the console we have 1 + 1 + 4 + 1 + 11 = 18. So D is the correct answer.

#### Answer: D

</p>
</details>

###### 89. What's the output ?

```javascript
const matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
];

function matrixHandle(m) {
  let total = arguments[0][0][0];
  let length = m.length;
  for (let i = 0; i < length; i++) {
    for (let j = 0; j < m[i].length; j++) {
      total += m[i][j];
    }
  }
  return total;
}

console.log(matrixHandle(matrix));
```

- A: 44
- B: 45
- C: 46
- D: 47

<details><summary><b>Answer</b></summary>
<p>
You can easily create a two-dimensional array by nesting an array inside the parent one as the variable `matrix` above. To render all of the elements in the matrix, we implement a simple code with two for-loop functions which are nested.

`arguments[0][0][0];` gives us 1 because `arguments` has wrapped the variable `matrix` in an array. Note that `arguments` is a Array-like.

So the variable `total` at first is 1, and then the final value cumulated by looping through the matrix is 46.

In short, we have 1 + 1 + 2 + 3 + 4 + 5 + 6 + 7+ 8 + 9 = 46. So C is the correct answer.

#### Answer: C

</p>
</details>

###### 90. What's the output ?

```javascript
const container1 = {
  stack: "Docker",
  getStack: function () {
    return this.stack;
  },
};
const a = container1.getStack();

const container2 = {
  stack: "Kubernetes",
  getStack: () => this.stack,
};
const b = container2.getStack();

const container3 = {
  architect: "microservice",
  getStack: function () {
    const stack = ["K8s"];
    return stack.map(function (element) {
      return `${element} - ${this.architect}`;
    });
  },
};
const c = container3.getStack();

const container4 = {
  architect: "microservice",
  getStack: function () {
    const stack = ["K8s"];
    return stack.map((element) => `${element} - ${this.architect}`);
  },
};
const d = container4.getStack();

console.log(`${a} -> ${b} -> ${c} -> ${d}`);
```

- A: "Docker -> Kubernetes -> K8s - undefined -> K8s - microservice"
- B: "Docker -> Kubernetes -> K8s - microservice -> K8s - microservice"
- C: "Docker -> undefined -> K8s - microservice -> K8s - undefined"
- D: "Docker -> undefined -> K8s - undefined -> K8s - microservice"

<details><summary><b>Answer</b></summary>
<p>
The code above might help you revise how the arrow function works in different contexts, especially when dealing with the keyword `this` in JavaScript. There are two crucial takeaway messages you might need to keep in mind when using a function, as follows:

- First: The arrow function does not create a new `this` binding when you use them. It inherits from the parent one(environment) when it is defined.

- Second: The keyword `this` could be problematic when it is called in a callback function. For example when implementing `setTimeout`, `setInterval` or `map`, `filter`, `reduce` or `some`, `every` among others, you will need to pass a callback function. Given that the callback function changes the context, `this` might therefore change to `global` object and no longer point to the parent object.

We have 4 objects in the snippet above. Each has a simple property and a trivial method. `a` returns `docker` because `this.stack` exactly points to the object declared `container1`. However, `b` returns `undefined` because `this` in the arrow function points to the global one rather than `container2`. Why? As we mentioned above, the arrow function does not create a context for itself, so `container2.getStack()` is still bound to the global object. `this.stack` becomes `undefined` as a result.

Next `c` gives us `K8s - undefined` because `this` is called in the callback function when we use `map`. A new context is now created by the function `map`, so `this` will not point to the object `container3`. The callback function implemented with `map` or `filter` always creates a new context so that `this` changes.

We get `K8s - microservice"` in `d` because the arrow function helps us fix the problem caused by switching context as in the object `container3`. Here are some lessons learned when dealing with context, nested functions (or implementing callback function):

- Use normal function rather than arrow function when you write a method inside an object in which the method does not have a nested function(method) or callback one. Arrow function is not recommended when creating object prototypes, classes along with object literals as well.

- Use the arrow function when you want to access to `this`, especially in the case of nested method (function) or when using callback function. Otherwise, `this` will no longer point to the object in these cases (nested method or using callback function with map, filter). There are two other techniques (old-fashion ones) to fix that.

- There are 3 ways to fix `this` issue relating to the nested method or callback function: using arrow function as mentioned above, use `self = this` technique or explicitly binding with `call`, `bind` or `apply` method.

#### Answer: D

</p>
</details>

###### 91. What's the output ?

```javascript
class Angular {
  vendor = "Google";
  lang = "TypeScript";
  overview() {
    let report = [];
    report.push(this.lang);
    report = report.map(function (e) {
      return e.length + this.vendor.length;
    });

    return report;
  }
}

const me = new Angular();

console.log(me.overview());
```

- A: 16
- B: 106
- C: NaN
- D: TypeError

<details><summary><b>Answer</b></summary>
<p>

The code snippet above might help you revise the concept of context in conjunction with the way `this` is treated in JavaScript. In short, if you implement a callback function for the `map` method (or in another case: nested function), then you might need to pay attention to `this` binding.

While `report.push(this.lang);` works pretty well as `this` points to the property declared within the class `Angular`, the line `return e.length + this.vendor.length;` does not work as `this` no longer points to `vendor` we have already declared as a property in the class. The `map` function creates a new context here. As `vendor` is undefined inside the callback of the `map` function, we get `TypeError` in the console. So D is the correct answer.

How to fix that? We can quickly fix this one with one of three techniques: (1) use arrow function for the callback passing to `map`, (2) temporarily create an alternative `this` such as `let self = this` before we call map and use `self` instead of `this`. (3) explicitly bind the callback for `map` using bind, call or apply. We can also pass `this` as the second parameter for the map function. It also works.

#### Answer: D

</p>
</details>

###### 92. What's the output ?

```javascript
class FrameWork {
  constructor(options) {
    this.options = options ?? ["Angular", "React", "Vue"];
  }

  total() {
    return this.options.length;
  }

  filter() {
    const selected = this.options.filter(function (element) {
      return element[0] === "A";
    });
    return selected[0].length + this.total();
  }
}

const app = new FrameWork();

console.log(app.filter());
```

- A: 8
- B: 2
- C: 10
- D: 1

<details><summary><b>Answer</b></summary>
<p>

The code challenge above implements a simple class with two methods. There is only one point in the syntax that you might need to pay a bit more attention to is `??` (nullish coalescing operator ) which is quite similar to `||` (OR).

`??` returns the right-hand side value if the left-hand side is either `null` or `undefined` while `||` does the same thing for `falsy` value (false, null, undefined, 0, -0, 0n, NaN, "").length

So as we do not pass anything into the constructor when we initiate the object `app`, `this.options` takes the default value `["Angular", "React", "Vue"]`, then the method `total()` evaluates the length of the array, which is 3.

`filter()` gives us the length of "Angular", which is 8. So the final value is 10. The correct answer is C.

#### Answer: C

</p>
</details>

###### 93. What's the output ?

```javascript
const origin = [[[123], 321], 213];
const manipulated = origin.flat(origin.length);
console.log(manipulated.length + origin.length);
```

- A: 2
- B: 3
- C: 4
- D: 5

<details><summary><b>Answer</b></summary>
<p>

The challenge might hopefully help you have a grip on the native array method `flat()`, which is quite handy to flatten a nested array. `flat()` accepts a parameter that defines the level of the nested array you are going to manipulate. By default, this parameter is 1.

The method returns a manipulated array. So on the code about `origin.length` returns 2 given that the array `origin` has two elements. When flattening the original array named `origin` with `flat(2)`, we then have a new array `[123, 321, 213]`.

Finally, we have 5 in the console, and D is the correct answer.

#### Answer: D

</p>
</details>

###### 94. What's the output ?

```javascript
const pipe =
  (...funs) =>
  (v) => {
    funs.reduce((res, func) => {
      return func(res);
    }, v);
  };

const plusFour = (v) => v + 4;
const multiplyBySix = (v) => v * 6;
const divideByTwo = (v) => v / 2;

pipe(plusFour, multiplyBySix, divideByTwo, multiplyBySix, console.log)(1);
```

- A: 80
- B: 90
- C: 100
- D: 110

<details><summary><b>Answer</b></summary>
<p>

The `pipe` function can receive an unlimited number of arguments/parameters thanks to rest parameter `...funcs`. These arguments/parameters turn out are function as we call the parent function `pipe`. In JavaScript, it is quite common to pass a function as a parameter of another function.

Please call these functions, which are passed to `pipe`, are child functions. They are then looped and executed one by one with `reduce` method, no matter how many functions you attempt to pass to `pipe`. `v` in the code is simply the argument defined in each child function.

So first we have 1, then by executing `plusFour` it becomes 5. When `multiplyBySix` is called, the output turns to 30. It becomes 15 when we call `divideByTwo`. Finally, it becomes 90 as we multiply 15 \* 6 when the function `multiplyBySix` is called again.

So B is the correct answer.

<!-- Credit: https://www.freecodecamp.org/news/pipe-and-compose-in-javascript-5b04004ac937/ -->

#### Answer: B

</p>
</details>

###### 95. What's the output ?

```javascript
const quickSortRecursive = function (arrayInput) {
  if (!Array.isArray(arrayInput)) {
    console.log("The input data is not an array");
    return arrayInput;
  }
  const pivotIndex = arrayInput.length - 1;
  const pivot = arrayInput[pivotIndex];
  const left = [];
  const right = [];
  let currentItem;
  for (let i = 0; i < pivotIndex; i++) {
    currentItem = arrayInput[i];
    if (currentItem < pivot) {
      left.push(currentItem);
    } else {
      right.push(currentItem);
    }
  }

  return [...quickSortRecursive(left), pivot, ...quickSortRecursive(right)];
};

console.log(quickSortRecursive([1, 100, 8, 19, 8, 6]));
```

- A: [1, 100, 8, 19, 8, 6]
- B: [1, 6, 8, 8, 19, 100]
- C: [100, 19, 8, 8, 6, 1]
- D: 6

<details><summary><b>Answer</b></summary>
<p>

You might see a commonly used algorithm here in the code challenge called "quicksort" in which we apply the strategy "divide and conquer". We also use the "recursive" method when we want to recall the function until it meets our expectations. You might also need to know about the "rest parameter" in JavaScript, as shown by the three dots (...) above.

The code above helps us to arrange an array in such a way that the value will increase from left to right. Using the quicksort method, we need to create a pivot (likely the first item from right to left or the first item from left to right). First, we divide the original array into two parts: left and right, depending on the value compared to the pivot.

Next, by calling the function recursively, we keep creating new pivots for the right and left arrays created above for the purpose of sorting value.

Finally, the original array is sorted from left to right depending on the value.

So B is the correct answer.

<!-- Credit: https://www.freecodecamp.org/news/pipe-and-compose-in-javascript-5b04004ac937/ -->

#### Answer: B

</p>
</details>

###### 96. What's the output ?

```javascript
const hasOwn = (a) => {
  return function (o = { a: 10 }) {
    o.property = a[1];
    return (b) => {
      return o.a + o.property + b;
    };
  };
};

console.log(hasOwn([10, 20])()(10));
```

- A: 10
- B: 20
- C: 30
- D: 40

<details><summary><b>Answer</b></summary>
<p>

We have quite trivial nested functions. If you are familiar with the concept of `closure` in JavaScript, then it is not a big deal to read the code above. The final function, named hasOwn, has three parameters, and when we execute it, we only pass two arguments because we have already defined the default value for the second nested function.

The final result is as `o.a + o.property + b`, meaning 10 + 20 + 10. So D is the correct answer.

#### Answer: D

</p>
</details>



###### 97. What's the output ?

```javascript
function craft(text){
  const p = document.createElement("p");
  p.innerHTML = text;
  document.body.append(p)
}
craft("1 - sync A")
const fetchItem = new Promise((resolve) => {   
  craft("2 - eager sync B")  
  setTimeout(function(){      
      craft("3 - eager async C")
      resolve("4 - async - D");
  }, 2000)  
});
craft("5 - sync E") 

fetchItem.then(data => craft(data))
```

- A: 1 - 2 - 3 - 4 - 5 
- B: 1 - 2 - 5 - 3 - 4
- C: 1 - 2 - 5 - 4 - 3
- D: 1 - 2 - 3 - 5 - 4

<details><summary><b>Answer</b></summary>
<p>

The order will be: sync --> async. Given that Promise is eager, then we have 1 - 2 - 5 - 3 - 4. Note that if we do not call then(), the data handled by promise will not be casted out. 

#### Answer: B

</p>
</details>











