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

This question reminds us about Closure in JS. Closure allows us to create a `stateful function` and such function can access to variable outside of its scope. In a nutshell, a closure can have access to `global` variable (scope), `father function` scope and `its` own scope.

We have here 3, 3, 3 and 3, 4, 5 because first we simply call the function `a()`. It works like a normal function and we do not see something `stateful` here. In later case, we declare a variable `x` and it stores the value of function `a(1)`, that is why we get 3. 4. 5 rather than 3, 3, 3.

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

We can use `call()`, `apply()` and `bind()` to appy a function to any object. At first sight, it seems that three functions do the same thing. Yet there are some situations where they are differently employed to handle respective contexts or solve particular problems.

Of the three, only `bind()` can be executed after binding. We can create a variable to store the result as `helloRonaldo()` in the code snippet above. `apply()` and `call()` will bind and execute the function at the same time. `apply()` hints us `a` ~ array where we need to pass an array as parameter. `call()` hints us `c` or comma where we pass parameters with a comma. You might want to have a look at this post https://stackoverflow.com/questions/15455009/javascript-call-apply-vs-bind

Note that `window.window.window.score` or `window.score` or simply `score` do the same thing. It points to the `score()` function in the global scope.

The correct anwser is D. The `score()` and `getAge()` functions are nothing special.

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

The code snippet above is not a big challenge for you I guess. It simply gives you an example of `this` in different contexts when we declare an anonymous function inside a method of an object. The three first methods are common ways to handle `this` using `this` as second parameter in `map()`, by using `bind(this)` in `forEach` (or map()) or by `that = this`technique (we did use `seft` rathern `that`).

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

As `getInfo()` is an arrow function, `this` declared inside this function points to `window`, so `myYoutube.content()` returns `myYoutube.getInfo()`. Noted that we have to explicitly write `myYoutube.getInfo()` to make sure the code will run correctly as `this` in this case does not work as it does not refer to the currect object. In the function `getInfo()`, however, `this` actually refers to the currect object instead of `window` object because we use a normal function here.

Then we have the property `name` with the value "hoccoban". So the correct answer is A.

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
class Dog{	
	speak(){
		return this.say();
	}
	
	say(){
		console.log("hello world")
	}	
}

class Cat{
	speak(){
		return this.say();
	}
	
	say(){
		console.log("kia ora")
	}
}

const animal = new Dog();
animal.speak();
Object.setPrototypeOf(animal, Cat.prototype);
animal.speak();
```

- C: "hello world" -  undefined
- C: "kia ora"     -  "kia ora"
- C: "hello world" -  "kia ora"
- D: "hello world" -  "hello world"

<details><summary><b>Answer</b></summary>
<p>

The central issue/concept mentioned in the code above is the method `Object.setPrototypeOf(object, prototype)`. It is one of the features in ES6, or ECMAScript 2015. Another way to set the prototype of an object is `Object.prototype.__proto__` but the latter is controversial.

At first, `animal.speak();` gives us "hello world" which is no surprise. Yet, in the second call, we get "kia ora" instead of "hello world". When checking the prototype with `Object.getPrototypeOf(animal)`, you might see that `Cat` is the prototype of the object `animal` rather than `Dog`.

The answer is C.

By the way, `kia ora` means `hello` in the Māori language.

#### Answer: C

</p>
</details>

---

###### 82. What's the output?

```javascript
const obj = { a: 'one', b: 'two', a: 'three' };
console.log(obj);
```

- A: `{ a: "one", b: "two" }`
- B: `{ b: "two", a: "three" }`
- C: `{ a: "three", b: "two" }`
- D: `SyntaxError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

If you have two keys with the same name, the key will be replaced. It will still be in its first position, but with the last specified value.

</p>
</details>

---

###### 83. The JavaScript global execution context creates two things for you: the global object, and the "this" keyword.

- A: true
- B: false
- C: it depends

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The base execution context is the global execution context: it's what's accessible everywhere in your code.

</p>
</details>

---

###### 84. What's the output?

```javascript
for (let i = 1; i < 5; i++) {
  if (i === 3) continue;
  console.log(i);
}
```

- A: `1` `2`
- B: `1` `2` `3`
- C: `1` `2` `4`
- D: `1` `3` `4`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The `continue` statement skips an iteration if a certain condition returns `true`.

</p>
</details>

---

###### 85. What's the output?

```javascript
String.prototype.giveLydiaPizza = () => {
  return 'Just give Lydia pizza already!';
};

const name = 'Lydia';

name.giveLydiaPizza();
```

- A: `"Just give Lydia pizza already!"`
- B: `TypeError: not a function`
- C: `SyntaxError`
- D: `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

`String` is a built-in constructor, which we can add properties to. I just added a method to its prototype. Primitive strings are automatically converted into a string object, generated by the string prototype function. So, all strings (string objects) have access to that method!

</p>
</details>

---

###### 86. What's the output?

```javascript
const a = {};
const b = { key: 'b' };
const c = { key: 'c' };

a[b] = 123;
a[c] = 456;

console.log(a[b]);
```

- A: `123`
- B: `456`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Object keys are automatically converted into strings. We are trying to set an object as a key to object `a`, with the value of `123`.

However, when we stringify an object, it becomes `"[object Object]"`. So what we are saying here, is that `a["[object Object]"] = 123`. Then, we can try to do the same again. `c` is another object that we are implicitly stringifying. So then, `a["[object Object]"] = 456`.

Then, we log `a[b]`, which is actually `a["[object Object]"]`. We just set that to `456`, so it returns `456`.

</p>
</details>

---

###### 87. What's the output?

```javascript
const foo = () => console.log('First');
const bar = () => setTimeout(() => console.log('Second'));
const baz = () => console.log('Third');

bar();
foo();
baz();
```

- A: `First` `Second` `Third`
- B: `First` `Third` `Second`
- C: `Second` `First` `Third`
- D: `Second` `Third` `First`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

We have a `setTimeout` function and invoked it first. Yet, it was logged last.

This is because in browsers, we don't just have the runtime engine, we also have something called a `WebAPI`. The `WebAPI` gives us the `setTimeout` function to start with, and for example the DOM.

After the _callback_ is pushed to the WebAPI, the `setTimeout` function itself (but not the callback!) is popped off the stack.

<img src="../img/X5wsHOg.png" width="200">

Now, `foo` gets invoked, and `"First"` is being logged.

<img src="../img/Pvc0dGq.png" width="200">

`foo` is popped off the stack, and `baz` gets invoked. `"Third"` gets logged.

<img src="../img/WhA2bCP.png" width="200">

The WebAPI can't just add stuff to the stack whenever it's ready. Instead, it pushes the callback function to something called the _queue_.

<img src="../img/NSnDZmU.png" width="200">

This is where an event loop starts to work. An **event loop** looks at the stack and task queue. If the stack is empty, it takes the first thing on the queue and pushes it onto the stack.

<img src="../img/uyiScAI.png" width="200">

`bar` gets invoked, `"Second"` gets logged, and it's popped off the stack.

</p>
</details>

---

###### 88. What is the event.target when clicking the button?

```html
<div onclick="console.log('first div')">
  <div onclick="console.log('second div')">
    <button onclick="console.log('button')">
      Click!
    </button>
  </div>
</div>
```

- A: Outer `div`
- B: Inner `div`
- C: `button`
- D: An array of all nested elements.

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The deepest nested element that caused the event is the target of the event. You can stop bubbling by `event.stopPropagation`

</p>
</details>

---

###### 89. When you click the paragraph, what's the logged output?

```html
<div onclick="console.log('div')">
  <p onclick="console.log('p')">
    Click here!
  </p>
</div>
```

- A: `p` `div`
- B: `div` `p`
- C: `p`
- D: `div`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

If we click `p`, we see two logs: `p` and `div`. During event propagation, there are 3 phases: capturing, target, and bubbling. By default, event handlers are executed in the bubbling phase (unless you set `useCapture` to `true`). It goes from the deepest nested element outwards.

</p>
</details>

---

###### 90. What's the output?

```javascript
const person = { name: 'Lydia' };

function sayHi(age) {
  return `${this.name} is ${age}`;
}

console.log(sayHi.call(person, 21));
console.log(sayHi.bind(person, 21));
```

- A: `undefined is 21` `Lydia is 21`
- B: `function` `function`
- C: `Lydia is 21` `Lydia is 21`
- D: `Lydia is 21` `function`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

With both, we can pass the object to which we want the `this` keyword to refer to. However, `.call` is also _executed immediately_!

`.bind.` returns a _copy_ of the function, but with a bound context! It is not executed immediately.

</p>
</details>

---

###### 91. What's the output?

```javascript
function sayHi() {
  return (() => 0)();
}

console.log(typeof sayHi());
```

- A: `"object"`
- B: `"number"`
- C: `"function"`
- D: `"undefined"`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

The `sayHi` function returns the returned value of the immediately invoked function expression (IIFE). This function returned `0`, which is type `"number"`.

FYI: there are only 7 built-in types: `null`, `undefined`, `boolean`, `number`, `string`, `object`, and `symbol`. `"function"` is not a type, since functions are objects, it's of type `"object"`.

</p>
</details>

---

###### 92. Which of these values are falsy?

```javascript
0;
new Number(0);
('');
(' ');
new Boolean(false);
undefined;
```

- A: `0`, `''`, `undefined`
- B: `0`, `new Number(0)`, `''`, `new Boolean(false)`, `undefined`
- C: `0`, `''`, `new Boolean(false)`, `undefined`
- D: All of them are falsy

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

There are 8 falsy values:

- `undefined`
- `null`
- `NaN`
- `false`
- `''` (empty string)
- `0`
- `-0`
- `0n` (BigInt(0))

Function constructors, like `new Number` and `new Boolean` are truthy.

</p>
</details>

---

###### 93. What's the output?

```javascript
console.log(typeof typeof 1);
```

- A: `"number"`
- B: `"string"`
- C: `"object"`
- D: `"undefined"`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

`typeof 1` returns `"number"`.
`typeof "number"` returns `"string"`

</p>
</details>

---

###### 94. What's the output?

```javascript
const numbers = [1, 2, 3];
numbers[10] = 11;
console.log(numbers);
```

- A: `[1, 2, 3, 7 x null, 11]`
- B: `[1, 2, 3, 11]`
- C: `[1, 2, 3, 7 x empty, 11]`
- D: `SyntaxError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

When you set a value to an element in an array that exceeds the length of the array, JavaScript creates something called "empty slots". These actually have the value of `undefined`, but you will see something like:

`[1, 2, 3, 7 x empty, 11]`

depending on where you run it (it's different for every browser, node, etc.)

</p>
</details>

---

###### 95. What's the output?

```javascript
(() => {
  let x, y;
  try {
    throw new Error();
  } catch (x) {
    (x = 1), (y = 2);
    console.log(x);
  }
  console.log(x);
  console.log(y);
})();
```

- A: `1` `undefined` `2`
- B: `undefined` `undefined` `undefined`
- C: `1` `1` `2`
- D: `1` `undefined` `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The `catch` block receives the argument `x`. This is not the same `x` as the variable when we pass arguments. This variable `x` is block-scoped.

Later, we set this block-scoped variable equal to `1`, and set the value of the variable `y`. Now, we log the block-scoped variable `x`, which is equal to `1`.

Outside of the `catch` block, `x` is still `undefined`, and `y` is `2`. When we want to `console.log(x)` outside of the `catch` block, it returns `undefined`, and `y` returns `2`.

</p>
</details>

---

###### 96. Everything in JavaScript is either a...

- A: primitive or object
- B: function or object
- C: trick question! only objects
- D: number or object

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

JavaScript only has primitive types and objects.

Primitive types are `boolean`, `null`, `undefined`, `bigint`, `number`, `string`, and `symbol`.

What differentiates a primitive from an object is that primitives do not have any properties or methods; however, you'll note that `'foo'.toUpperCase()` evaluates to `'FOO'` and does not result in a `TypeError`. This is because when you try to access a property or method on a primitive like a string, JavaScript will implicitly wrap the primitive type using one of the wrapper classes, i.e. `String`, and then immediately discard the wrapper after the expression evaluates. All primitives except for `null` and `undefined` exhibit this behaviour.

</p>
</details>

---

###### 97. What's the output?

```javascript
[[0, 1], [2, 3]].reduce(
  (acc, cur) => {
    return acc.concat(cur);
  },
  [1, 2],
);
```

- A: `[0, 1, 2, 3, 1, 2]`
- B: `[6, 1, 2]`
- C: `[1, 2, 0, 1, 2, 3]`
- D: `[1, 2, 6]`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

`[1, 2]` is our initial value. This is the value we start with, and the value of the very first `acc`. During the first round, `acc` is `[1,2]`, and `cur` is `[0, 1]`. We concatenate them, which results in `[1, 2, 0, 1]`.

Then, `[1, 2, 0, 1]` is `acc` and `[2, 3]` is `cur`. We concatenate them, and get `[1, 2, 0, 1, 2, 3]`

</p>
</details>

---

###### 98. What's the output?

```javascript
!!null;
!!'';
!!1;
```

- A: `false` `true` `false`
- B: `false` `false` `true`
- C: `false` `true` `true`
- D: `true` `true` `false`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

`null` is falsy. `!null` returns `true`. `!true` returns `false`.

`""` is falsy. `!""` returns `true`. `!true` returns `false`.

`1` is truthy. `!1` returns `false`. `!false` returns `true`.

</p>
</details>

---

###### 99. What does the `setInterval` method return in the browser?

```javascript
setInterval(() => console.log('Hi'), 1000);
```

- A: a unique id
- B: the amount of milliseconds specified
- C: the passed function
- D: `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

It returns a unique id. This id can be used to clear that interval with the `clearInterval()` function.

</p>
</details>

---

###### 100. What does this return?

```javascript
[...'Lydia'];
```

- A: `["L", "y", "d", "i", "a"]`
- B: `["Lydia"]`
- C: `[[], "Lydia"]`
- D: `[["L", "y", "d", "i", "a"]]`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

A string is an iterable. The spread operator maps every character of an iterable to one element.

</p>
</details>

---

###### 101. What's the output?

```javascript
function* generator(i) {
  yield i;
  yield i * 2;
}

const gen = generator(10);

console.log(gen.next().value);
console.log(gen.next().value);
```

- A: `[0, 10], [10, 20]`
- B: `20, 20`
- C: `10, 20`
- D: `0, 10 and 10, 20`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Regular functions cannot be stopped mid-way after invocation. However, a generator function can be "stopped" midway, and later continue from where it stopped. Every time a generator function encounters a `yield` keyword, the function yields the value specified after it. Note that the generator function in that case doesn’t _return_ the value, it _yields_ the value.

First, we initialize the generator function with `i` equal to `10`. We invoke the generator function using the `next()` method. The first time we invoke the generator function, `i` is equal to `10`. It encounters the first `yield` keyword: it yields the value of `i`. The generator is now "paused", and `10` gets logged.

Then, we invoke the function again with the `next()` method. It starts to continue where it stopped previously, still with `i` equal to `10`. Now, it encounters the next `yield` keyword, and yields `i * 2`. `i` is equal to `10`, so it returns `10 * 2`, which is `20`. This results in `10, 20`.

</p>
</details>

---

###### 102. What does this return?

```javascript
const firstPromise = new Promise((res, rej) => {
  setTimeout(res, 500, 'one');
});

const secondPromise = new Promise((res, rej) => {
  setTimeout(res, 100, 'two');
});

Promise.race([firstPromise, secondPromise]).then(res => console.log(res));
```

- A: `"one"`
- B: `"two"`
- C: `"two" "one"`
- D: `"one" "two"`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

When we pass multiple promises to the `Promise.race` method, it resolves/rejects the _first_ promise that resolves/rejects. To the `setTimeout` method, we pass a timer: 500ms for the first promise (`firstPromise`), and 100ms for the second promise (`secondPromise`). This means that the `secondPromise` resolves first with the value of `'two'`. `res` now holds the value of `'two'`, which gets logged.

</p>
</details>

---

###### 103. What's the output?

```javascript
let person = { name: 'Lydia' };
const members = [person];
person = null;

console.log(members);
```

- A: `null`
- B: `[null]`
- C: `[{}]`
- D: `[{ name: "Lydia" }]`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

First, we declare a variable `person` with the value of an object that has a `name` property.

<img src="../img/TML1MbS.png" width="200">

Then, we declare a variable called `members`. We set the first element of that array equal to the value of the `person` variable. Objects interact by _reference_ when setting them equal to each other. When you assign a reference from one variable to another, you make a _copy_ of that reference. (note that they don't have the _same_ reference!)

<img src="../img/FSG5K3F.png" width="300">

Then, we set the variable `person` equal to `null`.

<img src="../img/sYjcsMT.png" width="300">

We are only modifying the value of the `person` variable, and not the first element in the array, since that element has a different (copied) reference to the object. The first element in `members` still holds its reference to the original object. When we log the `members` array, the first element still holds the value of the object, which gets logged.

</p>
</details>

---

###### 104. What's the output?

```javascript
const person = {
  name: 'Lydia',
  age: 21,
};

for (const item in person) {
  console.log(item);
}
```

- A: `{ name: "Lydia" }, { age: 21 }`
- B: `"name", "age"`
- C: `"Lydia", 21`
- D: `["name", "Lydia"], ["age", 21]`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

With a `for-in` loop, we can iterate through object keys, in this case `name` and `age`. Under the hood, object keys are strings (if they're not a Symbol). On every loop, we set the value of `item` equal to the current key it’s iterating over. First, `item` is equal to `name`, and gets logged. Then, `item` is equal to `age`, which gets logged.

</p>
</details>

---

###### 105. What's the output?

```javascript
console.log(3 + 4 + '5');
```

- A: `"345"`
- B: `"75"`
- C: `12`
- D: `"12"`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Operator associativity is the order in which the compiler evaluates the expressions, either left-to-right or right-to-left. This only happens if all operators have the _same_ precedence. We only have one type of operator: `+`. For addition, the associativity is left-to-right.

`3 + 4` gets evaluated first. This results in the number `7`.

`7 + '5'` results in `"75"` because of coercion. JavaScript converts the number `7` into a string, see question 15. We can concatenate two strings using the `+`operator. `"7" + "5"` results in `"75"`.

</p>
</details>

---

###### 106. What's the value of `num`?

```javascript
const num = parseInt('7*6', 10);
```

- A: `42`
- B: `"42"`
- C: `7`
- D: `NaN`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Only the first numbers in the string is returned. Based on the _radix_ (the second argument in order to specify what type of number we want to parse it to: base 10, hexadecimal, octal, binary, etc.), the `parseInt` checks whether the characters in the string are valid. Once it encounters a character that isn't a valid number in the radix, it stops parsing and ignores the following characters.

`*` is not a valid number. It only parses `"7"` into the decimal `7`. `num` now holds the value of `7`.

</p>
</details>

---

###### 107. What's the output?

```javascript
[1, 2, 3].map(num => {
  if (typeof num === 'number') return;
  return num * 2;
});
```

- A: `[]`
- B: `[null, null, null]`
- C: `[undefined, undefined, undefined]`
- D: `[ 3 x empty ]`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

When mapping over the array, the value of `num` is equal to the element it’s currently looping over. In this case, the elements are numbers, so the condition of the if statement `typeof num === "number"` returns `true`. The map function creates a new array and inserts the values returned from the function.

However, we don’t return a value. When we don’t return a value from the function, the function returns `undefined`. For every element in the array, the function block gets called, so for each element we return `undefined`.

</p>
</details>

---

###### 108. What's the output?

```javascript
function getInfo(member, year) {
  member.name = 'Lydia';
  year = '1998';
}

const person = { name: 'Sarah' };
const birthYear = '1997';

getInfo(person, birthYear);

console.log(person, birthYear);
```

- A: `{ name: "Lydia" }, "1997"`
- B: `{ name: "Sarah" }, "1998"`
- C: `{ name: "Lydia" }, "1998"`
- D: `{ name: "Sarah" }, "1997"`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

Arguments are passed by _value_, unless their value is an object, then they're passed by _reference_. `birthYear` is passed by value, since it's a string, not an object. When we pass arguments by value, a _copy_ of that value is created (see question 46).

The variable `birthYear` has a reference to the value `"1997"`. The argument `year` also has a reference to the value `"1997"`, but it's not the same value as `birthYear` has a reference to. When we update the value of `year` by setting `year` equal to `"1998"`, we are only updating the value of `year`. `birthYear` is still equal to `"1997"`.

The value of `person` is an object. The argument `member` has a (copied) reference to the _same_ object. When we modify a property of the object `member` has a reference to, the value of `person` will also be modified, since they both have a reference to the same object. `person`'s `name` property is now equal to the value `"Lydia"`

</p>
</details>

---

###### 109. What's the output?

```javascript
function greeting() {
  throw 'Hello world!';
}

function sayHi() {
  try {
    const data = greeting();
    console.log('It worked!', data);
  } catch (e) {
    console.log('Oh no an error:', e);
  }
}

sayHi();
```

- A: `It worked! Hello world!`
- B: `Oh no an error: undefined`
- C: `SyntaxError: can only throw Error objects`
- D: `Oh no an error: Hello world!`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

With the `throw` statement, we can create custom errors. With this statement, you can throw exceptions. An exception can be a <b>string</b>, a <b>number</b>, a <b>boolean</b> or an <b>object</b>. In this case, our exception is the string `'Hello world!'`.

With the `catch` statement, we can specify what to do if an exception is thrown in the `try` block. An exception is thrown: the string `'Hello world!'`. `e` is now equal to that string, which we log. This results in `'Oh an error: Hello world!'`.

</p>
</details>

---

###### 110. What's the output?

```javascript
function Car() {
  this.make = 'Lamborghini';
  return { make: 'Maserati' };
}

const myCar = new Car();
console.log(myCar.make);
```

- A: `"Lamborghini"`
- B: `"Maserati"`
- C: `ReferenceError`
- D: `TypeError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

When you return a property, the value of the property is equal to the _returned_ value, not the value set in the constructor function. We return the string `"Maserati"`, so `myCar.make` is equal to `"Maserati"`.

</p>
</details>

---

###### 111. What's the output?

```javascript
(() => {
  let x = (y = 10);
})();

console.log(typeof x);
console.log(typeof y);
```

- A: `"undefined", "number"`
- B: `"number", "number"`
- C: `"object", "number"`
- D: `"number", "undefined"`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

`let x = (y = 10);` is actually shorthand for:

```javascript
y = 10;
let x = y;
```

When we set `y` equal to `10`, we actually add a property `y` to the global object (`window` in browser, `global` in Node). In a browser, `window.y` is now equal to `10`.

Then, we declare a variable `x` with the value of `y`, which is `10`. Variables declared with the `let` keyword are _block scoped_, they are only defined within the block they're declared in; the immediately invoked function expression (IIFE) in this case. When we use the `typeof` operator, the operand `x` is not defined: we are trying to access `x` outside of the block it's declared in. This means that `x` is not defined. Values who haven't been assigned a value or declared are of type `"undefined"`. `console.log(typeof x)` returns `"undefined"`.

However, we created a global variable `y` when setting `y` equal to `10`. This value is accessible anywhere in our code. `y` is defined, and holds a value of type `"number"`. `console.log(typeof y)` returns `"number"`.

</p>
</details>

---

###### 112. What's the output?

```javascript
class Dog {
  constructor(name) {
    this.name = name;
  }
}

Dog.prototype.bark = function() {
  console.log(`Woof I am ${this.name}`);
};

const pet = new Dog('Mara');

pet.bark();

delete Dog.prototype.bark;

pet.bark();
```

- A: `"Woof I am Mara"`, `TypeError`
- B: `"Woof I am Mara"`, `"Woof I am Mara"`
- C: `"Woof I am Mara"`, `undefined`
- D: `TypeError`, `TypeError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

We can delete properties from objects using the `delete` keyword, also on the prototype. By deleting a property on the prototype, it is not available anymore in the prototype chain. In this case, the `bark` function is not available anymore on the prototype after `delete Dog.prototype.bark`, yet we still try to access it.

When we try to invoke something that is not a function, a `TypeError` is thrown. In this case `TypeError: pet.bark is not a function`, since `pet.bark` is `undefined`.

</p>
</details>

---

###### 113. What's the output?

```javascript
const set = new Set([1, 1, 2, 3, 4]);

console.log(set);
```

- A: `[1, 1, 2, 3, 4]`
- B: `[1, 2, 3, 4]`
- C: `{1, 1, 2, 3, 4}`
- D: `{1, 2, 3, 4}`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The `Set` object is a collection of _unique_ values: a value can only occur once in a set.

We passed the iterable `[1, 1, 2, 3, 4]` with a duplicate value `1`. Since we cannot have two of the same values in a set, one of them is removed. This results in `{1, 2, 3, 4}`.

</p>
</details>

---

###### 114. What's the output?

```javascript
// counter.js
let counter = 10;
export default counter;
```

```javascript
// index.js
import myCounter from './counter';

myCounter += 1;

console.log(myCounter);
```

- A: `10`
- B: `11`
- C: `Error`
- D: `NaN`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

An imported module is _read-only_: you cannot modify the imported module. Only the module that exports them can change its value.

When we try to increment the value of `myCounter`, it throws an error: `myCounter` is read-only and cannot be modified.

</p>
</details>

---

###### 115. What's the output?

```javascript
const name = 'Lydia';
age = 21;

console.log(delete name);
console.log(delete age);
```

- A: `false`, `true`
- B: `"Lydia"`, `21`
- C: `true`, `true`
- D: `undefined`, `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The `delete` operator returns a boolean value: `true` on a successful deletion, else it'll return `false`. However, variables declared with the `var`, `const` or `let` keyword cannot be deleted using the `delete` operator.

The `name` variable was declared with a `const` keyword, so its deletion is not successful: `false` is returned. When we set `age` equal to `21`, we actually added a property called `age` to the global object. You can successfully delete properties from objects this way, also the global object, so `delete age` returns `true`.

</p>
</details>

---

###### 116. What's the output?

```javascript
const numbers = [1, 2, 3, 4, 5];
const [y] = numbers;

console.log(y);
```

- A: `[[1, 2, 3, 4, 5]]`
- B: `[1, 2, 3, 4, 5]`
- C: `1`
- D: `[1]`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

We can unpack values from arrays or properties from objects through destructuring. For example:

```javascript
[a, b] = [1, 2];
```

<img src="../img/ADFpVop.png" width="200">

The value of `a` is now `1`, and the value of `b` is now `2`. What we actually did in the question, is:

```javascript
[y] = [1, 2, 3, 4, 5];
```

<img src="../img/NzGkMNk.png" width="200">

This means that the value of `y` is equal to the first value in the array, which is the number `1`. When we log `y`, `1` is returned.

</p>
</details>

---

###### 117. What's the output?

```javascript
const user = { name: 'Lydia', age: 21 };
const admin = { admin: true, ...user };

console.log(admin);
```

- A: `{ admin: true, user: { name: "Lydia", age: 21 } }`
- B: `{ admin: true, name: "Lydia", age: 21 }`
- C: `{ admin: true, user: ["Lydia", 21] }`
- D: `{ admin: true }`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

It's possible to combine objects using the spread operator `...`. It lets you create copies of the key/value pairs of one object, and add them to another object. In this case, we create copies of the `user` object, and add them to the `admin` object. The `admin` object now contains the copied key/value pairs, which results in `{ admin: true, name: "Lydia", age: 21 }`.

</p>
</details>

---

###### 118. What's the output?

```javascript
const person = { name: 'Lydia' };

Object.defineProperty(person, 'age', { value: 21 });

console.log(person);
console.log(Object.keys(person));
```

- A: `{ name: "Lydia", age: 21 }`, `["name", "age"]`
- B: `{ name: "Lydia", age: 21 }`, `["name"]`
- C: `{ name: "Lydia"}`, `["name", "age"]`
- D: `{ name: "Lydia"}`, `["age"]`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

With the `defineProperty` method, we can add new properties to an object, or modify existing ones. When we add a property to an object using the `defineProperty` method, they are by default _not enumerable_. The `Object.keys` method returns all _enumerable_ property names from an object, in this case only `"name"`.

Properties added using the `defineProperty` method are immutable by default. You can override this behavior using the `writable`, `configurable` and `enumerable` properties. This way, the `defineProperty` method gives you a lot more control over the properties you're adding to an object.

</p>
</details>

---

###### 119. What's the output?

```javascript
const settings = {
  username: 'lydiahallie',
  level: 19,
  health: 90,
};

const data = JSON.stringify(settings, ['level', 'health']);
console.log(data);
```

- A: `"{"level":19, "health":90}"`
- B: `"{"username": "lydiahallie"}"`
- C: `"["level", "health"]"`
- D: `"{"username": "lydiahallie", "level":19, "health":90}"`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The second argument of `JSON.stringify` is the _replacer_. The replacer can either be a function or an array, and lets you control what and how the values should be stringified.

If the replacer is an _array_, only the property names included in the array will be added to the JSON string. In this case, only the properties with the names `"level"` and `"health"` are included, `"username"` is excluded. `data` is now equal to `"{"level":19, "health":90}"`.

If the replacer is a _function_, this function gets called on every property in the object you're stringifying. The value returned from this function will be the value of the property when it's added to the JSON string. If the value is `undefined`, this property is excluded from the JSON string.

</p>
</details>

---

###### 120. What's the output?

```javascript
let num = 10;

const increaseNumber = () => num++;
const increasePassedNumber = number => number++;

const num1 = increaseNumber();
const num2 = increasePassedNumber(num1);

console.log(num1);
console.log(num2);
```

- A: `10`, `10`
- B: `10`, `11`
- C: `11`, `11`
- D: `11`, `12`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The unary operator `++` _first returns_ the value of the operand, _then increments_ the value of the operand. The value of `num1` is `10`, since the `increaseNumber` function first returns the value of `num`, which is `10`, and only increments the value of `num` afterwards.

`num2` is `10`, since we passed `num1` to the `increasePassedNumber`. `number` is equal to `10`(the value of `num1`. Again, the unary operator `++` _first returns_ the value of the operand, _then increments_ the value of the operand. The value of `number` is `10`, so `num2` is equal to `10`.

</p>
</details>

---

###### 121. What's the output?

```javascript
const value = { number: 10 };

const multiply = (x = { ...value }) => {
  console.log((x.number *= 2));
};

multiply();
multiply();
multiply(value);
multiply(value);
```

- A: `20`, `40`, `80`, `160`
- B: `20`, `40`, `20`, `40`
- C: `20`, `20`, `20`, `40`
- D: `NaN`, `NaN`, `20`, `40`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

In ES6, we can initialize parameters with a default value. The value of the parameter will be the default value, if no other value has been passed to the function, or if the value of the parameter is `"undefined"`. In this case, we spread the properties of the `value` object into a new object, so `x` has the default value of `{ number: 10 }`.

The default argument is evaluated at _call time_! Every time we call the function, a _new_ object is created. We invoke the `multiply` function the first two times without passing a value: `x` has the default value of `{ number: 10 }`. We then log the multiplied value of that number, which is `20`.

The third time we invoke multiply, we do pass an argument: the object called `value`. The `*=` operator is actually shorthand for `x.number = x.number * 2`: we modify the value of `x.number`, and log the multiplied value `20`.

The fourth time, we pass the `value` object again. `x.number` was previously modified to `20`, so `x.number *= 2` logs `40`.

</p>
</details>

---

###### 122. What's the output?

```javascript
[1, 2, 3, 4].reduce((x, y) => console.log(x, y));
```

- A: `1` `2` and `3` `3` and `6` `4`
- B: `1` `2` and `2` `3` and `3` `4`
- C: `1` `undefined` and `2` `undefined` and `3` `undefined` and `4` `undefined`
- D: `1` `2` and `undefined` `3` and `undefined` `4`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The first argument that the `reduce` method receives is the _accumulator_, `x` in this case. The second argument is the _current value_, `y`. With the reduce method, we execute a callback function on every element in the array, which could ultimately result in one single value.

In this example, we are not returning any values, we are simply logging the values of the accumulator and the current value.

The value of the accumulator is equal to the previously returned value of the callback function. If you don't pass the optional `initialValue` argument to the `reduce` method, the accumulator is equal to the first element on the first call.

On the first call, the accumulator (`x`) is `1`, and the current value (`y`) is `2`. We don't return from the callback function, we log the accumulator and current value: `1` and `2` get logged.

If you don't return a value from a function, it returns `undefined`. On the next call, the accumulator is `undefined`, and the current value is `3`. `undefined` and `3` get logged.

On the fourth call, we again don't return from the callback function. The accumulator is again `undefined`, and the current value is `4`. `undefined` and `4` get logged.

</p>
</details>
  
---

###### 123. With which constructor can we successfully extend the `Dog` class?

```javascript
class Dog {
  constructor(name) {
    this.name = name;
  }
};

class Labrador extends Dog {
  // 1
  constructor(name, size) {
    this.size = size;
  }
  // 2
  constructor(name, size) {
    super(name);
    this.size = size;
  }
  // 3
  constructor(size) {
    super(name);
    this.size = size;
  }
  // 4
  constructor(name, size) {
    this.name = name;
    this.size = size;
  }

};
```

- A: 1
- B: 2
- C: 3
- D: 4

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

In a derived class, you cannot access the `this` keyword before calling `super`. If you try to do that, it will throw a ReferenceError: 1 and 4 would throw a reference error.

With the `super` keyword, we call that parent class's constructor with the given arguments. The parent's constructor receives the `name` argument, so we need to pass `name` to `super`.

The `Labrador` class receives two arguments, `name` since it extends `Dog`, and `size` as an extra property on the `Labrador` class. They both need to be passed to the constructor function on `Labrador`, which is done correctly using constructor 2.

</p>
</details>

---

###### 124. What's the output?

```javascript
// index.js
console.log('running index.js');
import { sum } from './sum.js';
console.log(sum(1, 2));

// sum.js
console.log('running sum.js');
export const sum = (a, b) => a + b;
```

- A: `running index.js`, `running sum.js`, `3`
- B: `running sum.js`, `running index.js`, `3`
- C: `running sum.js`, `3`, `running index.js`
- D: `running index.js`, `undefined`, `running sum.js`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

With the `import` keyword, all imported modules are _pre-parsed_. This means that the imported modules get run _first_, the code in the file which imports the module gets executed _after_.

This is a difference between `require()` in CommonJS and `import`! With `require()`, you can load dependencies on demand while the code is being run. If we would have used `require` instead of `import`, `running index.js`, `running sum.js`, `3` would have been logged to the console.

</p>
</details>

---

###### 125. What's the output?

```javascript
console.log(Number(2) === Number(2));
console.log(Boolean(false) === Boolean(false));
console.log(Symbol('foo') === Symbol('foo'));
```

- A: `true`, `true`, `false`
- B: `false`, `true`, `false`
- C: `true`, `false`, `true`
- D: `true`, `true`, `true`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

Every Symbol is entirely unique. The purpose of the argument passed to the Symbol is to give the Symbol a description. The value of the Symbol is not dependent on the passed argument. As we test equality, we are creating two entirely new symbols: the first `Symbol('foo')`, and the second `Symbol('foo')`. These two values are unique and not equal to each other, `Symbol('foo') === Symbol('foo')` returns `false`.

</p>
</details>

---

###### 126. What's the output?

```javascript
const name = 'Lydia Hallie';
console.log(name.padStart(13));
console.log(name.padStart(2));
```

- A: `"Lydia Hallie"`, `"Lydia Hallie"`
- B: `" Lydia Hallie"`, `" Lydia Hallie"` (`"[13x whitespace]Lydia Hallie"`, `"[2x whitespace]Lydia Hallie"`)
- C: `" Lydia Hallie"`, `"Lydia Hallie"` (`"[1x whitespace]Lydia Hallie"`, `"Lydia Hallie"`)
- D: `"Lydia Hallie"`, `"Lyd"`,

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

With the `padStart` method, we can add padding to the beginning of a string. The value passed to this method is the _total_ length of the string together with the padding. The string `"Lydia Hallie"` has a length of `12`. `name.padStart(13)` inserts 1 space at the start of the string, because 12 + 1 is 13.

If the argument passed to the `padStart` method is smaller than the length of the array, no padding will be added.

</p>
</details>

---

###### 127. What's the output?

```javascript
console.log('🥑' + '💻');
```

- A: `"🥑💻"`
- B: `257548`
- C: A string containing their code points
- D: Error

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

With the `+` operator, you can concatenate strings. In this case, we are concatenating the string `"🥑"` with the string `"💻"`, resulting in `"🥑💻"`.

</p>
</details>

---

###### 128. How can we log the values that are commented out after the console.log statement?

```javascript
function* startGame() {
  const answer = yield 'Do you love JavaScript?';
  if (answer !== 'Yes') {
    return "Oh wow... Guess we're gone here";
  }
  return 'JavaScript loves you back ❤️';
}

const game = startGame();
console.log(/* 1 */); // Do you love JavaScript?
console.log(/* 2 */); // JavaScript loves you back ❤️
```

- A: `game.next("Yes").value` and `game.next().value`
- B: `game.next.value("Yes")` and `game.next.value()`
- C: `game.next().value` and `game.next("Yes").value`
- D: `game.next.value()` and `game.next.value("Yes")`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

A generator function "pauses" its execution when it sees the `yield` keyword. First, we have to let the function yield the string "Do you love JavaScript?", which can be done by calling `game.next().value`.

Every line is executed, until it finds the first `yield` keyword. There is a `yield` keyword on the first line within the function: the execution stops with the first yield! _This means that the variable `answer` is not defined yet!_

When we call `game.next("Yes").value`, the previous `yield` is replaced with the value of the parameters passed to the `next()` function, `"Yes"` in this case. The value of the variable `answer` is now equal to `"Yes"`. The condition of the if-statement returns `false`, and `JavaScript loves you back ❤️` gets logged.

</p>
</details>

---

###### 129. What's the output?

```javascript
console.log(String.raw`Hello\nworld`);
```

- A: `Hello world!`
- B: `Hello` <br />&nbsp; &nbsp; &nbsp;`world`
- C: `Hello\nworld`
- D: `Hello\n` <br /> &nbsp; &nbsp; &nbsp;`world`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

`String.raw` returns a string where the escapes (`\n`, `\v`, `\t` etc.) are ignored! Backslashes can be an issue since you could end up with something like:

`` const path = `C:\Documents\Projects\table.html` ``

Which would result in:

`"C:DocumentsProjects able.html"`

With `String.raw`, it would simply ignore the escape and print:

`C:\Documents\Projects\table.html`

In this case, the string is `Hello\nworld`, which gets logged.

</p>
</details>

---

###### 130. What's the output?

```javascript
async function getData() {
  return await Promise.resolve('I made it!');
}

const data = getData();
console.log(data);
```

- A: `"I made it!"`
- B: `Promise {<resolved>: "I made it!"}`
- C: `Promise {<pending>}`
- D: `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

An async function always returns a promise. The `await` still has to wait for the promise to resolve: a pending promise gets returned when we call `getData()` in order to set `data` equal to it.

If we wanted to get access to the resolved value `"I made it"`, we could have used the `.then()` method on `data`:

`data.then(res => console.log(res))`

This would've logged `"I made it!"`

</p>
</details>

---

###### 131. What's the output?

```javascript
function addToList(item, list) {
  return list.push(item);
}

const result = addToList('apple', ['banana']);
console.log(result);
```

- A: `['apple', 'banana']`
- B: `2`
- C: `true`
- D: `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

The `.push()` method returns the _length_ of the new array! Previously, the array contained one element (the string `"banana"`) and had a length of `1`. After adding the string `"apple"` to the array, the array contains two elements, and has a length of `2`. This gets returned from the `addToList` function.

The `push` method modifies the original array. If you wanted to return the _array_ from the function rather than the _length of the array_, you should have returned `list` after pushing `item` to it.

</p>
</details>

---

###### 132. What's the output?

```javascript
const box = { x: 10, y: 20 };

Object.freeze(box);

const shape = box;
shape.x = 100;

console.log(shape);
```

- A: `{ x: 100, y: 20 }`
- B: `{ x: 10, y: 20 }`
- C: `{ x: 100 }`
- D: `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

`Object.freeze` makes it impossible to add, remove, or modify properties of an object (unless the property's value is another object).

When we create the variable `shape` and set it equal to the frozen object `box`, `shape` also refers to a frozen object. You can check whether an object is frozen by using `Object.isFrozen`. In this case, `Object.isFrozen(shape)` returns true, since the variable `shape` has a reference to a frozen object.

Since `shape` is frozen, and since the value of `x` is not an object, we cannot modify the property `x`. `x` is still equal to `10`, and `{ x: 10, y: 20 }` gets logged.

</p>
</details>

---

###### 133. What's the output?

```javascript
const { name: myName } = { name: 'Lydia' };

console.log(name);
```

- A: `"Lydia"`
- B: `"myName"`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

When we unpack the property `name` from the object on the right-hand side, we assign its value `"Lydia"` to a variable with the name `myName`.

With `{ name: myName }`, we tell JavaScript that we want to create a new variable called `myName` with the value of the `name` property on the right-hand side.

Since we try to log `name`, a variable that is not defined, a ReferenceError gets thrown.

</p>
</details>

---

###### 134. Is this a pure function?

```javascript
function sum(a, b) {
  return a + b;
}
```

- A: Yes
- B: No

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

A pure function is a function that _always_ returns the same result, if the same arguments are passed.

The `sum` function always returns the same result. If we pass `1` and `2`, it will _always_ return `3` without side effects. If we pass `5` and `10`, it will _always_ return `15`, and so on. This is the definition of a pure function.

</p>
</details>

---

###### 135. What is the output?

```javascript
const add = () => {
  const cache = {};
  return num => {
    if (num in cache) {
      return `From cache! ${cache[num]}`;
    } else {
      const result = num + 10;
      cache[num] = result;
      return `Calculated! ${result}`;
    }
  };
};

const addFunction = add();
console.log(addFunction(10));
console.log(addFunction(10));
console.log(addFunction(5 * 2));
```

- A: `Calculated! 20` `Calculated! 20` `Calculated! 20`
- B: `Calculated! 20` `From cache! 20` `Calculated! 20`
- C: `Calculated! 20` `From cache! 20` `From cache! 20`
- D: `Calculated! 20` `From cache! 20` `Error`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The `add` function is a _memoized_ function. With memoization, we can cache the results of a function in order to speed up its execution. In this case, we create a `cache` object that stores the previously returned values.

If we call the `addFunction` function again with the same argument, it first checks whether it has already gotten that value in its cache. If that's the case, the caches value will be returned, which saves on execution time. Else, if it's not cached, it will calculate the value and store it afterwards.

We call the `addFunction` function three times with the same value: on the first invocation, the value of the function when `num` is equal to `10` isn't cached yet. The condition of the if-statement `num in cache` returns `false`, and the else block gets executed: `Calculated! 20` gets logged, and the value of the result gets added to the cache object. `cache` now looks like `{ 10: 20 }`.

The second time, the `cache` object contains the value that gets returned for `10`. The condition of the if-statement `num in cache` returns `true`, and `'From cache! 20'` gets logged.

The third time, we pass `5 * 2` to the function which gets evaluated to `10`. The `cache` object contains the value that gets returned for `10`. The condition of the if-statement `num in cache` returns `true`, and `'From cache! 20'` gets logged.

</p>
</details>

---

###### 136. What is the output?

```javascript
const myLifeSummedUp = ['☕', '💻', '🍷', '🍫'];

for (let item in myLifeSummedUp) {
  console.log(item);
}

for (let item of myLifeSummedUp) {
  console.log(item);
}
```

- A: `0` `1` `2` `3` and `"☕"` `"💻"` `"🍷"` `"🍫"`
- B: `"☕"` `"💻"` `"🍷"` `"🍫"` and `"☕"` `"💻"` `"🍷"` `"🍫"`
- C: `"☕"` `"💻"` `"🍷"` `"🍫"` and `0` `1` `2` `3`
- D: `0` `1` `2` `3` and `{0: "☕", 1: "💻", 2: "🍷", 3: "🍫"}`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

With a _for-in_ loop, we can iterate over **enumerable** properties. In an array, the enumerable properties are the "keys" of array elements, which are actually their indexes. You could see an array as:

`{0: "☕", 1: "💻", 2: "🍷", 3: "🍫"}`

Where the keys are the enumerable properties. `0` `1` `2` `3` get logged.

With a _for-of_ loop, we can iterate over **iterables**. An array is an iterable. When we iterate over the array, the variable "item" is equal to the element it's currently iterating over, `"☕"` `"💻"` `"🍷"` `"🍫"` get logged.

</p>
</details>

---

###### 137. What is the output?

```javascript
const list = [1 + 2, 1 * 2, 1 / 2];
console.log(list);
```

- A: `["1 + 2", "1 * 2", "1 / 2"]`
- B: `["12", 2, 0.5]`
- C: `[3, 2, 0.5]`
- D: `[1, 1, 1]`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Array elements can hold any value. Numbers, strings, objects, other arrays, null, boolean values, undefined, and other expressions such as dates, functions, and calculations.

The element will be equal to the returned value. `1 + 2` returns `3`, `1 * 2` returns `2`, and `1 / 2` returns `0.5`.

</p>
</details>

---

###### 138. What is the output?

```javascript
function sayHi(name) {
  return `Hi there, ${name}`;
}

console.log(sayHi());
```

- A: `Hi there,`
- B: `Hi there, undefined`
- C: `Hi there, null`
- D: `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

By default, arguments have the value of `undefined`, unless a value has been passed to the function. In this case, we didn't pass a value for the `name` argument. `name` is equal to `undefined` which gets logged.

In ES6, we can overwrite this default `undefined` value with default parameters. For example:

`function sayHi(name = "Lydia") { ... }`

In this case, if we didn't pass a value or if we passed `undefined`, `name` would always be equal to the string `Lydia`

</p>
</details>

---

###### 139. What is the output?

```javascript
var status = '😎';

setTimeout(() => {
  const status = '😍';

  const data = {
    status: '🥑',
    getStatus() {
      return this.status;
    },
  };

  console.log(data.getStatus());
  console.log(data.getStatus.call(this));
}, 0);
```

- A: `"🥑"` and `"😍"`
- B: `"🥑"` and `"😎"`
- C: `"😍"` and `"😎"`
- D: `"😎"` and `"😎"`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

The value of the `this` keyword is dependent on where you use it. In a **method**, like the `getStatus` method, the `this` keyword refers to _the object that the method belongs to_. The method belongs to the `data` object, so `this` refers to the `data` object. When we log `this.status`, the `status` property on the `data` object gets logged, which is `"🥑"`.

With the `call` method, we can change the object to which the `this` keyword refers. In **functions**, the `this` keyword refers to the _the object that the function belongs to_. We declared the `setTimeout` function on the _global object_, so within the `setTimeout` function, the `this` keyword refers to the _global object_. On the global object, there is a variable called _status_ with the value of `"😎"`. When logging `this.status`, `"😎"` gets logged.

</p>
</details>

---

###### 140. What is the output?

```javascript
const person = {
  name: 'Lydia',
  age: 21,
};

let city = person.city;
city = 'Amsterdam';

console.log(person);
```

- A: `{ name: "Lydia", age: 21 }`
- B: `{ name: "Lydia", age: 21, city: "Amsterdam" }`
- C: `{ name: "Lydia", age: 21, city: undefined }`
- D: `"Amsterdam"`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

We set the variable `city` equal to the value of the property called `city` on the `person` object. There is no property on this object called `city`, so the variable `city` has the value of `undefined`.

Note that we are _not_ referencing the `person` object itself! We simply set the variable `city` equal to the current value of the `city` property on the `person` object.

Then, we set `city` equal to the string `"Amsterdam"`. This doesn't change the person object: there is no reference to that object.

When logging the `person` object, the unmodified object gets returned.

</p>
</details>

---

###### 141. What is the output?

```javascript
function checkAge(age) {
  if (age < 18) {
    const message = "Sorry, you're too young.";
  } else {
    const message = "Yay! You're old enough!";
  }

  return message;
}

console.log(checkAge(21));
```

- A: `"Sorry, you're too young."`
- B: `"Yay! You're old enough!"`
- C: `ReferenceError`
- D: `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Variables with the `const` and `let` keyword are _block-scoped_. A block is anything between curly brackets (`{ }`). In this case, the curly brackets of the if/else statements. You cannot reference a variable outside of the block it's declared in, a ReferenceError gets thrown.

</p>
</details>

---

###### 142. What kind of information would get logged?

```javascript
fetch('https://www.website.com/api/user/1')
  .then(res => res.json())
  .then(res => console.log(res));
```

- A: The result of the `fetch` method.
- B: The result of the second invocation of the `fetch` method.
- C: The result of the callback in the previous `.then()`.
- D: It would always be undefined.

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The value of `res` in the second `.then` is equal to the returned value of the previous `.then`. You can keep chaining `.then`s like this, where the value is passed to the next handler.

</p>
</details>

---

###### 143. Which option is a way to set `hasName` equal to `true`, provided you cannot pass `true` as an argument?

```javascript
function getName(name) {
  const hasName = //
}
```

- A: `!!name`
- B: `name`
- C: `new Boolean(name)`
- D: `name.length`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

With `!!name`, we determine whether the value of `name` is truthy or falsy. If name is truthy, which we want to test for, `!name` returns `false`. `!false` (which is what `!!name` practically is) returns `true`.

By setting `hasName` equal to `name`, you set `hasName` equal to whatever value you passed to the `getName` function, not the boolean value `true`.

`new Boolean(true)` returns an object wrapper, not the boolean value itself.

`name.length` returns the length of the passed argument, not whether it's `true`.

</p>
</details>

---

###### 144. What's the output?

```javascript
function sum(num1, num2 = num1) {
  console.log(num1 + num2);
}

sum(10);
```

- A: `NaN`
- B: `20`
- C: `ReferenceError`
- D: `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

You can set a default parameter's value equal to another parameter of the function, as long as they've been defined _before_ the default parameter. We pass the value `10` to the `sum` function. If the `sum` function only receives 1 argument, it means that the value for `num2` is not passed, and the value of `num1` is equal to the passed value `10` in this case. The default value of `num2` is the value of `num1`, which is `10`. `num1 + num2` returns `20`.

If you're trying to set a default parameter's value equal to a parameter which is defined _after_ (to the right), the parameter's value hasn't been initialized yet, which will throw an error.

</p>
</details>

---

###### 145. What's the output?

```javascript
// module.js
export default () => 'Hello world';
export const name = 'Lydia';

// index.js
import * as data from './module';

console.log(data);
```

- A: `{ default: function default(), name: "Lydia" }`
- B: `{ default: function default() }`
- C: `{ default: "Hello world", name: "Lydia" }`
- D: Global object of `module.js`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

With the `import * as name` syntax, we import _all exports_ from the `module.js` file into the `index.js` file as a new object called `data` is created. In the `module.js` file, there are two exports: the default export, and a named export. The default export is a function which returns the string `"Hello World"`, and the named export is a variable called `name` which has the value of the string `"Lydia"`.

The `data` object has a `default` property for the default export, other properties have the names of the named exports and their corresponding values.

</p>
</details>

---

###### 146. What's the output?

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
}

const member = new Person('John');
console.log(typeof member);
```

- A: `"class"`
- B: `"function"`
- C: `"object"`
- D: `"string"`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Classes are syntactical sugar for function constructors. The equivalent of the `Person` class as a function constructor would be:

```javascript
function Person() {
  this.name = name;
}
```

Calling a function constructor with `new` results in the creation of an instance of `Person`, `typeof` keyword returns `"object"` for an instance. `typeof member` returns `"object"`.

</p>
</details>

---

###### 147. What's the output?

```javascript
let newList = [1, 2, 3].push(4);

console.log(newList.push(5));
```

- A: `[1, 2, 3, 4, 5]`
- B: `[1, 2, 3, 5]`
- C: `[1, 2, 3, 4]`
- D: `Error`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The `.push` method returns the _new length_ of the array, not the array itself! By setting `newList` equal to `[1, 2, 3].push(4)`, we set `newList` equal to the new length of the array: `4`.

Then, we try to use the `.push` method on `newList`. Since `newList` is the numerical value `4`, we cannot use the `.push` method: a TypeError is thrown.

</p>
</details>

---

###### 148. What's the output?

```javascript
function giveLydiaPizza() {
  return 'Here is pizza!';
}

const giveLydiaChocolate = () =>
  "Here's chocolate... now go hit the gym already.";

console.log(giveLydiaPizza.prototype);
console.log(giveLydiaChocolate.prototype);
```

- A: `{ constructor: ...}` `{ constructor: ...}`
- B: `{}` `{ constructor: ...}`
- C: `{ constructor: ...}` `{}`
- D: `{ constructor: ...}` `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

Regular functions, such as the `giveLydiaPizza` function, have a `prototype` property, which is an object (prototype object) with a `constructor` property. Arrow functions however, such as the `giveLydiaChocolate` function, do not have this `prototype` property. `undefined` gets returned when trying to access the `prototype` property using `giveLydiaChocolate.prototype`.

</p>
</details>

---

###### 149. What's the output?

```javascript
const person = {
  name: 'Lydia',
  age: 21,
};

for (const [x, y] of Object.entries(person)) {
  console.log(x, y);
}
```

- A: `name` `Lydia` and `age` `21`
- B: `["name", "Lydia"]` and `["age", 21]`
- C: `["name", "age"]` and `undefined`
- D: `Error`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

`Object.entries(person)` returns an array of nested arrays, containing the keys and objects:

`[ [ 'name', 'Lydia' ], [ 'age', 21 ] ]`

Using the `for-of` loop, we can iterate over each element in the array, the subarrays in this case. We can destructure the subarrays instantly in the for-of loop, using `const [x, y]`. `x` is equal to the first element in the subarray, `y` is equal to the second element in the subarray.

The first subarray is `[ "name", "Lydia" ]`, with `x` equal to `"name"`, and `y` equal to `"Lydia"`, which get logged.
The second subarray is `[ "age", 21 ]`, with `x` equal to `"age"`, and `y` equal to `21`, which get logged.

</p>
</details>

---

###### 150. What's the output?

```javascript
function getItems(fruitList, ...args, favoriteFruit) {
  return [...fruitList, ...args, favoriteFruit]
}

getItems(["banana", "apple"], "pear", "orange")
```

- A: `["banana", "apple", "pear", "orange"]`
- B: `[["banana", "apple"], "pear", "orange"]`
- C: `["banana", "apple", ["pear"], "orange"]`
- D: `SyntaxError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

`...args` is a rest parameter. The rest parameter's value is an array containing all remaining arguments, **and can only be the last parameter**! In this example, the rest parameter was the second parameter. This is not possible, and will throw a syntax error.

```javascript
function getItems(fruitList, favoriteFruit, ...args) {
  return [...fruitList, ...args, favoriteFruit];
}

getItems(['banana', 'apple'], 'pear', 'orange');
```

The above example works. This returns the array `[ 'banana', 'apple', 'orange', 'pear' ]`

</p>
</details>

---

###### 151. What's the output?

```javascript
function nums(a, b) {
  if (a > b) console.log('a is bigger');
  else console.log('b is bigger');
  return
  a + b;
}

console.log(nums(4, 2));
console.log(nums(1, 2));
```

- A: `a is bigger`, `6` and `b is bigger`, `3`
- B: `a is bigger`, `undefined` and `b is bigger`, `undefined`
- C: `undefined` and `undefined`
- D: `SyntaxError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

In JavaScript, we don't _have_ to write the semicolon (`;`) explicitly, however the JavaScript engine still adds them after statements. This is called **Automatic Semicolon Insertion**. A statement can for example be variables, or keywords like `throw`, `return`, `break`, etc.

Here, we wrote a `return` statement, and another value `a + b` on a _new line_. However, since it's a new line, the engine doesn't know that it's actually the value that we wanted to return. Instead, it automatically added a semicolon after `return`. You could see this as:

```javascript
return;
a + b;
```

This means that `a + b` is never reached, since a function stops running after the `return` keyword. If no value gets returned, like here, the function returns `undefined`. Note that there is no automatic insertion after `if/else` statements!

</p>
</details>

---

###### 152. What's the output?

```javascript
class Person {
  constructor() {
    this.name = 'Lydia';
  }
}

Person = class AnotherPerson {
  constructor() {
    this.name = 'Sarah';
  }
};

const member = new Person();
console.log(member.name);
```

- A: `"Lydia"`
- B: `"Sarah"`
- C: `Error: cannot redeclare Person`
- D: `SyntaxError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

We can set classes equal to other classes/function constructors. In this case, we set `Person` equal to `AnotherPerson`. The name on this constructor is `Sarah`, so the name property on the new `Person` instance `member` is `"Sarah"`.

</p>
</details>

---

###### 153. What's the output?

```javascript
const info = {
  [Symbol('a')]: 'b',
};

console.log(info);
console.log(Object.keys(info));
```

- A: `{Symbol('a'): 'b'}` and `["{Symbol('a')"]`
- B: `{}` and `[]`
- C: `{ a: "b" }` and `["a"]`
- D: `{Symbol('a'): 'b'}` and `[]`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

A Symbol is not _enumerable_. The Object.keys method returns all _enumerable_ key properties on an object. The Symbol won't be visible, and an empty array is returned. When logging the entire object, all properties will be visible, even non-enumerable ones.

This is one of the many qualities of a symbol: besides representing an entirely unique value (which prevents accidental name collision on objects, for example when working with 2 libraries that want to add properties to the same object), you can also "hide" properties on objects this way (although not entirely. You can still access symbols using the `Object.getOwnPropertySymbols()` method).

</p>
</details>

---

###### 154. What's the output?

```javascript
const getList = ([x, ...y]) => [x, y]
const getUser = user => { name: user.name, age: user.age }

const list = [1, 2, 3, 4]
const user = { name: "Lydia", age: 21 }

console.log(getList(list))
console.log(getUser(user))
```

- A: `[1, [2, 3, 4]]` and `undefined`
- B: `[1, [2, 3, 4]]` and `{ name: "Lydia", age: 21 }`
- C: `[1, 2, 3, 4]` and `{ name: "Lydia", age: 21 }`
- D: `Error` and `{ name: "Lydia", age: 21 }`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The `getList` function receives an array as its argument. Between the parentheses of the `getList` function, we destructure this array right away. You could see this as:

`[x, ...y] = [1, 2, 3, 4]`

With the rest parameter `...y`, we put all "remaining" arguments in an array. The remaining arguments are `2`, `3` and `4` in this case. The value of `y` is an array, containing all the rest parameters. The value of `x` is equal to `1` in this case, so when we log `[x, y]`, `[1, [2, 3, 4]]` gets logged.

The `getUser` function receives an object. With arrow functions, we don't _have_ to write curly brackets if we just return one value. However, if you want to return an _object_ from an arrow function, you have to write it between parentheses, otherwise no value gets returned! The following function would have returned an object:

`const getUser = user => ({ name: user.name, age: user.age })`

Since no value gets returned in this case, the function returns `undefined`.

</p>
</details>

---

###### 155. What's the output?

```javascript
const name = 'Lydia';

console.log(name());
```

- A: `SyntaxError`
- B: `ReferenceError`
- C: `TypeError`
- D: `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The variable `name` holds the value of a string, which is not a function, thus cannot invoke.

TypeErrors get thrown when a value is not of the expected type. JavaScript expected `name` to be a function since we're trying to invoke it. It was a string however, so a TypeError gets thrown: name is not a function!

SyntaxErrors get thrown when you've written something that isn't valid JavaScript, for example when you've written the word `return` as `retrun`.
ReferenceErrors get thrown when JavaScript isn't able to find a reference to a value that you're trying to access.

</p>
</details>

---

###### 156. What's the value of output?

```javascript
const output = `${[] && 'Im'}possible!
You should${'' && `n't`} see a therapist after so much JavaScript lol`;
```

- A: `possible! You should see a therapist after so much JavaScript lol`
- B: `Impossible! You should see a therapist after so much JavaScript lol`
- C: `possible! You shouldn't see a therapist after so much JavaScript lol`
- D: `Impossible! You shouldn't see a therapist after so much JavaScript lol`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

`[]` is a truthy value. With the `&&` operator, the right-hand value will be returned if the left-hand value is a truthy value. In this case, the left-hand value `[]` is a truthy value, so `"Im'` gets returned.

`""` is a falsy value. If the left-hand value is falsy, nothing gets returned. `n't` doesn't get returned.

</p>
</details>

---

###### 157. What's the value of output?

```javascript
const one = false || {} || null;
const two = null || false || '';
const three = [] || 0 || true;

console.log(one, two, three);
```

- A: `false` `null` `[]`
- B: `null` `""` `true`
- C: `{}` `""` `[]`
- D: `null` `null` `true`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

With the `||` operator, we can return the first truthy operand. If all values are falsy, the last operand gets returned.

`(false || {} || null)`: the empty object `{}` is a truthy value. This is the first (and only) truthy value, which gets returned. `one` is equal to `{}`.

`(null || false || "")`: all operands are falsy values. This means that the last operand, `""` gets returned. `two` is equal to `""`.

`([] || 0 || "")`: the empty array`[]` is a truthy value. This is the first truthy value, which gets returned. `three` is equal to `[]`.

</p>
</details>

---

###### 158. What's the value of output?

```javascript
const myPromise = () => Promise.resolve('I have resolved!');

function firstFunction() {
  myPromise().then(res => console.log(res));
  console.log('second');
}

async function secondFunction() {
  console.log(await myPromise());
  console.log('second');
}

firstFunction();
secondFunction();
```

- A: `I have resolved!`, `second` and `I have resolved!`, `second`
- B: `second`, `I have resolved!` and `second`, `I have resolved!`
- C: `I have resolved!`, `second` and `second`, `I have resolved!`
- D: `second`, `I have resolved!` and `I have resolved!`, `second`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

With a promise, we basically say _I want to execute this function, but I'll put it aside for now while it's running since this might take a while. Only when a certain value is resolved (or rejected), and when the call stack is empty, I want to use this value._

We can get this value with both `.then` and the `await` keyword in an `async` function. Although we can get a promise's value with both `.then` and `await`, they work a bit differently.

In the `firstFunction`, we (sort of) put the myPromise function aside while it was running, but continued running the other code, which is `console.log('second')` in this case. Then, the function resolved with the string `I have resolved`, which then got logged after it saw that the callstack was empty.

With the await keyword in `secondFunction`, we literally pause the execution of an async function until the value has been resolved before moving to the next line.

This means that it waited for the `myPromise` to resolve with the value `I have resolved`, and only once that happened, we moved to the next line: `second` got logged.

</p>
</details>

---

###### 159. What's the value of output?

```javascript
const set = new Set();

set.add(1);
set.add('Lydia');
set.add({ name: 'Lydia' });

for (let item of set) {
  console.log(item + 2);
}
```

- A: `3`, `NaN`, `NaN`
- B: `3`, `7`, `NaN`
- C: `3`, `Lydia2`, `[object Object]2`
- D: `"12"`, `Lydia2`, `[object Object]2`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The `+` operator is not only used for adding numerical values, but we can also use it to concatenate strings. Whenever the JavaScript engine sees that one or more values are not a number, it coerces the number into a string.

The first one is `1`, which is a numerical value. `1 + 2` returns the number 3.

However, the second one is a string `"Lydia"`. `"Lydia"` is a string and `2` is a number: `2` gets coerced into a string. `"Lydia"` and `"2"` get concatenated, which results in the string `"Lydia2"`.

`{ name: "Lydia" }` is an object. Neither a number nor an object is a string, so it stringifies both. Whenever we stringify a regular object, it becomes `"[object Object]"`. `"[object Object]"` concatenated with `"2"` becomes `"[object Object]2"`.

</p>
</details>

---

###### 160. What's its value?

```javascript
Promise.resolve(5);
```

- A: `5`
- B: `Promise {<pending>: 5}`
- C: `Promise {<fulfilled>: 5}`
- D: `Error`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

We can pass any type of value we want to `Promise.resolve`, either a promise or a non-promise. The method itself returns a promise with the resolved value (`<fulfilled>`). If you pass a regular function, it'll be a resolved promise with a regular value. If you pass a promise, it'll be a resolved promise with the resolved value of that passed promise.

In this case, we just passed the numerical value `5`. It returns a resolved promise with the value `5`.

</p>
</details>

---

###### 161. What's its value?

```javascript
function compareMembers(person1, person2 = person) {
  if (person1 !== person2) {
    console.log('Not the same!');
  } else {
    console.log('They are the same!');
  }
}

const person = { name: 'Lydia' };

compareMembers(person);
```

- A: `Not the same!`
- B: `They are the same!`
- C: `ReferenceError`
- D: `SyntaxError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Objects are passed by reference. When we check objects for strict equality (`===`), we're comparing their references.

We set the default value for `person2` equal to the `person` object, and passed the `person` object as the value for `person1`.

This means that both values have a reference to the same spot in memory, thus they are equal.

The code block in the `else` statement gets run, and `They are the same!` gets logged.

</p>
</details>

---

###### 162. What's its value?

```javascript
const colorConfig = {
  red: true,
  blue: false,
  green: true,
  black: true,
  yellow: false,
};

const colors = ['pink', 'red', 'blue'];

console.log(colorConfig.colors[1]);
```

- A: `true`
- B: `false`
- C: `undefined`
- D: `TypeError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

In JavaScript, we have two ways to access properties on an object: bracket notation, or dot notation. In this example, we use dot notation (`colorConfig.colors`) instead of bracket notation (`colorConfig["colors"]`).

With dot notation, JavaScript tries to find the property on the object with that exact name. In this example, JavaScript tries to find a property called `colors` on the `colorConfig` object. There is no property called `colors`, so this returns `undefined`. Then, we try to access the value of the first element by using `[1]`. We cannot do this on a value that's `undefined`, so it throws a `TypeError`: `Cannot read property '1' of undefined`.

JavaScript interprets (or unboxes) statements. When we use bracket notation, it sees the first opening bracket `[` and keeps going until it finds the closing bracket `]`. Only then, it will evaluate the statement. If we would've used `colorConfig[colors[1]]`, it would have returned the value of the `red` property on the `colorConfig` object.

</p>
</details>

---

###### 163. What's its value?

```javascript
console.log('❤️' === '❤️');
```

- A: `true`
- B: `false`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

Under the hood, emojis are unicodes. The unicodes for the heart emoji is `"U+2764 U+FE0F"`. These are always the same for the same emojis, so we're comparing two equal strings to each other, which returns true.

</p>
</details>

---

###### 164. Which of these methods modifies the original array?

```javascript
const emojis = ['✨', '🥑', '😍'];

emojis.map(x => x + '✨');
emojis.filter(x => x !== '🥑');
emojis.find(x => x !== '🥑');
emojis.reduce((acc, cur) => acc + '✨');
emojis.slice(1, 2, '✨');
emojis.splice(1, 2, '✨');
```

- A: `All of them`
- B: `map` `reduce` `slice` `splice`
- C: `map` `slice` `splice`
- D: `splice`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

With `splice` method, we modify the original array by deleting, replacing or adding elements. In this case, we removed 2 items from index 1 (we removed `'🥑'` and `'😍'`) and added the ✨ emoji instead.

`map`, `filter` and `slice` return a new array, `find` returns an element, and `reduce` returns a reduced value.

</p>
</details>

---

###### 165. What's the output?

```javascript
const food = ['🍕', '🍫', '🥑', '🍔'];
const info = { favoriteFood: food[0] };

info.favoriteFood = '🍝';

console.log(food);
```

- A: `['🍕', '🍫', '🥑', '🍔']`
- B: `['🍝', '🍫', '🥑', '🍔']`
- C: `['🍝', '🍕', '🍫', '🥑', '🍔']`
- D: `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

We set the value of the `favoriteFood` property on the `info` object equal to the string with the pizza emoji, `'🍕'`. A string is a primitive data type. In JavaScript, primitive data types don't interact by reference.

In JavaScript, primitive data types (everything that's not an object) interact by _value_. In this case, we set the value of the `favoriteFood` property on the `info` object equal to the value of the first element in the `food` array, the string with the pizza emoji in this case (`'🍕'`). A string is a primitive data type, and interact by value (see my [blogpost](https://www.theavocoder.com/complete-javascript/2018/12/21/by-value-vs-by-reference) if you're interested in learning more)

Then, we change the value of the `favoriteFood` property on the `info` object. The `food` array hasn't changed, since the value of `favoriteFood` was merely a _copy_ of the value of the first element in the array, and doesn't have a reference to the same spot in memory as the element on `food[0]`. When we log food, it's still the original array, `['🍕', '🍫', '🥑', '🍔']`.

</p>
</details>

---

###### 166. What does this method do?

```javascript
JSON.parse();
```

- A: Parses JSON to a JavaScript value
- B: Parses a JavaScript object to JSON
- C: Parses any JavaScript value to JSON
- D: Parses JSON to a JavaScript object only

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

With the `JSON.parse()` method, we can parse JSON string to a JavaScript value.

```javascript
// Stringifying a number into valid JSON, then parsing the JSON string to a JavaScript value:
const jsonNumber = JSON.stringify(4); // '4'
JSON.parse(jsonNumber); // 4

// Stringifying an array value into valid JSON, then parsing the JSON string to a JavaScript value:
const jsonArray = JSON.stringify([1, 2, 3]); // '[1, 2, 3]'
JSON.parse(jsonArray); // [1, 2, 3]

// Stringifying an object  into valid JSON, then parsing the JSON string to a JavaScript value:
const jsonArray = JSON.stringify({ name: 'Lydia' }); // '{"name":"Lydia"}'
JSON.parse(jsonArray); // { name: 'Lydia' }
```

</p>
</details>

---

###### 167. What's the output?

```javascript
let name = 'Lydia';

function getName() {
  console.log(name);
  let name = 'Sarah';
}

getName();
```

- A: Lydia
- B: Sarah
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

Each function has its own _execution context_ (or _scope_). The `getName` function first looks within its own context (scope) to see if it contains the variable `name` we're trying to access. In this case, the `getName` function contains its own `name` variable: we declare the variable `name` with the `let` keyword, and with the value of `'Sarah'`.

Variables with the `let` keyword (and `const`) are hoisted, but unlike `var`, don't get <i>initialized</i>. They are not accessible before the line we declare (initialize) them. This is called the "temporal dead zone". When we try to access the variables before they are declared, JavaScript throws a `ReferenceError`.

If we wouldn't have declared the `name` variable within the `getName` function, the javascript engine would've looked down the _scope chain_. The outer scope has a variable called `name` with the value of `Lydia`. In that case, it would've logged `Lydia`.

```javascript
let name = 'Lydia';

function getName() {
  console.log(name);
}

getName(); // Lydia
```

</p>
</details>

---

###### 168. What's the output?

```javascript
function* generatorOne() {
  yield ['a', 'b', 'c'];
}

function* generatorTwo() {
  yield* ['a', 'b', 'c'];
}

const one = generatorOne();
const two = generatorTwo();

console.log(one.next().value);
console.log(two.next().value);
```

- A: `a` and `a`
- B: `a` and `undefined`
- C: `['a', 'b', 'c']` and `a`
- D: `a` and `['a', 'b', 'c']`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

With the `yield` keyword, we `yield` values in a generator function. With the `yield*` keyword, we can yield values from another generator function, or iterable object (for example an array).

In `generatorOne`, we yield the entire array `['a', 'b', 'c']` using the `yield` keyword. The value of `value` property on the object returned by the `next` method on `one` (`one.next().value`) is equal to the entire array `['a', 'b', 'c']`.

```javascript
console.log(one.next().value); // ['a', 'b', 'c']
console.log(one.next().value); // undefined
```

In `generatorTwo`, we use the `yield*` keyword. This means that the first yielded value of `two`, is equal to the first yielded value in the iterator. The iterator is the array `['a', 'b', 'c']`. The first yielded value is `a`, so the first time we call `two.next().value`, `a` is returned.

```javascript
console.log(two.next().value); // 'a'
console.log(two.next().value); // 'b'
console.log(two.next().value); // 'c'
console.log(two.next().value); // undefined
```

</p>
</details>

---

###### 169. What's the output?

```javascript
console.log(`${(x => x)('I love')} to program`);
```

- A: `I love to program`
- B: `undefined to program`
- C: `${(x => x)('I love') to program`
- D: `TypeError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

Expressions within template literals are evaluated first. This means that the string will contain the returned value of the expression, the immediately invoked function `(x => x)('I love')` in this case. We pass the value `'I love'` as an argument to the `x => x` arrow function. `x` is equal to `'I love'`, which gets returned. This results in `I love to program`.

</p>
</details>

---

###### 170. What will happen?

```javascript
let config = {
  alert: setInterval(() => {
    console.log('Alert!');
  }, 1000),
};

config = null;
```

- A: The `setInterval` callback won't be invoked
- B: The `setInterval` callback gets invoked once
- C: The `setInterval` callback will still be called every second
- D: We never invoked `config.alert()`, config is `null`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Normally when we set objects equal to `null`, those objects get _garbage collected_ as there is no reference anymore to that object. However, since the callback function within `setInterval` is an arrow function (thus bound to the `config` object), the callback function still holds a reference to the `config` object.
As long as there is a reference, the object won't get garbage collected.
Since this is an interval, setting `config` to `null` or `delete`-ing `config.alert` won't garbage-collect the interval, so the interval will still be called.
It should be cleared with `clearInterval(config.alert)` to remove it from memory.
Since it was not cleared, the `setInterval` callback function will still get invoked every 1000ms (1s).

</p>
</details>

---

###### 171. Which method(s) will return the value `'Hello world!'`?

```javascript
const myMap = new Map();
const myFunc = () => 'greeting';

myMap.set(myFunc, 'Hello world!');

//1
myMap.get('greeting');
//2
myMap.get(myFunc);
//3
myMap.get(() => 'greeting');
```

- A: 1
- B: 2
- C: 2 and 3
- D: All of them

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

When adding a key/value pair using the `set` method, the key will be the value of the first argument passed to the `set` function, and the value will be the second argument passed to the `set` function. The key is the _function_ `() => 'greeting'` in this case, and the value `'Hello world'`. `myMap` is now `{ () => 'greeting' => 'Hello world!' }`.

1 is wrong, since the key is not `'greeting'` but `() => 'greeting'`.
3 is wrong, since we're creating a new function by passing it as a parameter to the `get` method. Object interact by _reference_. Functions are objects, which is why two functions are never strictly equal, even if they are identical: they have a reference to a different spot in memory.

</p>
</details>

---

###### 172. What's the output?

```javascript
const person = {
  name: 'Lydia',
  age: 21,
};

const changeAge = (x = { ...person }) => (x.age += 1);
const changeAgeAndName = (x = { ...person }) => {
  x.age += 1;
  x.name = 'Sarah';
};

changeAge(person);
changeAgeAndName();

console.log(person);
```

- A: `{name: "Sarah", age: 22}`
- B: `{name: "Sarah", age: 23}`
- C: `{name: "Lydia", age: 22}`
- D: `{name: "Lydia", age: 23}`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Both the `changeAge` and `changeAgeAndName` functions have a default parameter, namely a _newly_ created object `{ ...person }`. This object has copies of all the key/values in the `person` object.

First, we invoke the `changeAge` function and pass the `person` object as its argument. This function increases the value of the `age` property by 1. `person` is now `{ name: "Lydia", age: 22 }`.

Then, we invoke the `changeAgeAndName` function, however we don't pass a parameter. Instead, the value of `x` is equal to a _new_ object: `{ ...person }`. Since it's a new object, it doesn't affect the values of the properties on the `person` object. `person` is still equal to `{ name: "Lydia", age: 22 }`.

</p>
</details>

---

###### 173. Which of the following options will return `6`?

```javascript
function sumValues(x, y, z) {
  return x + y + z;
}
```

- A: `sumValues([...1, 2, 3])`
- B: `sumValues([...[1, 2, 3]])`
- C: `sumValues(...[1, 2, 3])`
- D: `sumValues([1, 2, 3])`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

With the spread operator `...`, we can _spread_ iterables to individual elements. The `sumValues` function receives three arguments: `x`, `y` and `z`. `...[1, 2, 3]` will result in `1, 2, 3`, which we pass to the `sumValues` function.

</p>
</details>

---

###### 174. What's the output?

```javascript
let num = 1;
const list = ['🥳', '🤠', '🥰', '🤪'];

console.log(list[(num += 1)]);
```

- A: `🤠`
- B: `🥰`
- C: `SyntaxError`
- D: `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

With the `+=` operand, we're incrementing the value of `num` by `1`. `num` had the initial value `1`, so `1 + 1` is `2`. The item on the second index in the `list` array is 🥰, `console.log(list[2])` prints 🥰.

</p>
</details>

---

###### 175. What's the output?

```javascript
const person = {
  firstName: 'Lydia',
  lastName: 'Hallie',
  pet: {
    name: 'Mara',
    breed: 'Dutch Tulip Hound',
  },
  getFullName() {
    return `${this.firstName} ${this.lastName}`;
  },
};

console.log(person.pet?.name);
console.log(person.pet?.family?.name);
console.log(person.getFullName?.());
console.log(member.getLastName?.());
```

- A: `undefined` `undefined` `undefined` `undefined`
- B: `Mara` `undefined` `Lydia Hallie` `ReferenceError`
- C: `Mara` `null` `Lydia Hallie` `null`
- D: `null` `ReferenceError` `null` `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

With the optional chaining operator `?.`, we no longer have to explicitly check whether the deeper nested values are valid or not. If we're trying to access a property on an `undefined` or `null` value (_nullish_), the expression short-circuits and returns `undefined`.

`person.pet?.name`: `person` has a property named `pet`: `person.pet` is not nullish. It has a property called `name`, and returns `Mara`.
`person.pet?.family?.name`: `person` has a property named `pet`: `person.pet` is not nullish. `pet` does _not_ have a property called `family`, `person.pet.family` is nullish. The expression returns `undefined`.
`person.getFullName?.()`: `person` has a property named `getFullName`: `person.getFullName()` is not nullish and can get invoked, which returns `Lydia Hallie`.
`member.getLastName?.()`: `member` is not defined: `member.getLastName()` is nullish. The expression returns `undefined`.

</p>
</details>

---

###### 176. What's the output?

```javascript
const groceries = ['banana', 'apple', 'peanuts'];

if (groceries.indexOf('banana')) {
  console.log('We have to buy bananas!');
} else {
  console.log(`We don't have to buy bananas!`);
}
```

- A: We have to buy bananas!
- B: We don't have to buy bananas
- C: `undefined`
- D: `1`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

We passed the condition `groceries.indexOf("banana")` to the if-statement. `groceries.indexOf("banana")` returns `0`, which is a falsy value. Since the condition in the if-statement is falsy, the code in the `else` block runs, and `We don't have to buy bananas!` gets logged.

</p>
</details>

---

###### 177. What's the output?

```javascript
const config = {
  languages: [],
  set language(lang) {
    return this.languages.push(lang);
  },
};

console.log(config.language);
```

- A: `function language(lang) { this.languages.push(lang }`
- B: `0`
- C: `[]`
- D: `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The `language` method is a `setter`. Setters don't hold an actual value, their purpose is to _modify_ properties. When calling a `setter` method, `undefined` gets returned.

</p>
</details>

---

###### 178. What's the output?

```javascript
const name = 'Lydia Hallie';

console.log(!typeof name === 'object');
console.log(!typeof name === 'string');
```

- A: `false` `true`
- B: `true` `false`
- C: `false` `false`
- D: `true` `true`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

`typeof name` returns `"string"`. The string `"string"` is a truthy value, so `!typeof name` returns the boolean value `false`. `false === "object"` and `false === "string"` both return`false`.

(If we wanted to check whether the type was (un)equal to a certain type, we should've written `!==` instead of `!typeof`)

</p>
</details>

---

###### 179. What's the output?

```javascript
const add = x => y => z => {
  console.log(x, y, z);
  return x + y + z;
};

add(4)(5)(6);
```

- A: `4` `5` `6`
- B: `6` `5` `4`
- C: `4` `function` `function`
- D: `undefined` `undefined` `6`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The `add` function returns an arrow function, which returns an arrow function, which returns an arrow function (still with me?). The first function receives an argument `x` with the value of `4`. We invoke the second function, which receives an argument `y` with the value `5`. Then we invoke the third function, which receives an argument `z` with the value `6`. When we're trying to access the value `x`, `y` and `z` within the last arrow function, the JS engine goes up the scope chain in order to find the values for `x` and `y` accordingly. This returns `4` `5` `6`.

</p>
</details>

---

###### 180. What's the output?

```javascript
async function* range(start, end) {
  for (let i = start; i <= end; i++) {
    yield Promise.resolve(i);
  }
}

(async () => {
  const gen = range(1, 3);
  for await (const item of gen) {
    console.log(item);
  }
})();
```

- A: `Promise {1}` `Promise {2}` `Promise {3}`
- B: `Promise {<pending>}` `Promise {<pending>}` `Promise {<pending>}`
- C: `1` `2` `3`
- D: `undefined` `undefined` `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The generator function `range` returns an async object with promises for each item in the range we pass: `Promise{1}`, `Promise{2}`, `Promise{3}`. We set the variable `gen` equal to the async object, after which we loop over it using a `for await ... of` loop. We set the variable `item` equal to the returned Promise values: first `Promise{1}`, then `Promise{2}`, then `Promise{3}`. Since we're _awaiting_ the value of `item`, the resolved promsie, the resolved _values_ of the promises get returned: `1`, `2`, then `3`.

</p>
</details>

---

###### 181. What's the output?

```javascript
const myFunc = ({ x, y, z }) => {
  console.log(x, y, z);
};

myFunc(1, 2, 3);
```

- A: `1` `2` `3`
- B: `{1: 1}` `{2: 2}` `{3: 3}`
- C: `{ 1: undefined }` `undefined` `undefined`
- D: `undefined` `undefined` `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

`myFunc` expects an object with properties `x`, `y` and `z` as its argument. Since we're only passing three separate numeric values (1, 2, 3) instead of one object with properties `x`, `y` and `z` ({x: 1, y: 2, z: 3}), `x`, `y` and `z` have their default value of `undefined`.

</p>
</details>

---

###### 182. What's the output?

```javascript
function getFine(speed, amount) {
  const formattedSpeed = new Intl.NumberFormat('en-US', {
    style: 'unit',
    unit: 'mile-per-hour'
  }).format(speed);

  const formattedAmount = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD'
  }).format(amount);

  return `The driver drove ${formattedSpeed} and has to pay ${formattedAmount}`;
}

console.log(getFine(130, 300))
```

- A: The driver drove 130 and has to pay 300
- B: The driver drove 130 mph and has to pay \$300.00
- C: The driver drove undefined and has to pay undefined
- D: The driver drove 130.00 and has to pay 300.00

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

With the `Intl.NumberFormat` method, we can format numeric values to any locale. We format the numeric value `130` to the `en-US` locale as a `unit` in `mile-per-hour`, which results in `130 mph`. The numeric value `300` to the `en-US` locale as a `currency` in `USD` results in `$300.00`.

</p>
</details>

---

###### 183. What's the output?

```javascript
const spookyItems = ['👻', '🎃', '🕸'];
({ item: spookyItems[3] } = { item: '💀' });

console.log(spookyItems);
```

- A: `["👻", "🎃", "🕸"]`
- B: `["👻", "🎃", "🕸", "💀"]`
- C: `["👻", "🎃", "🕸", { item: "💀" }]`
- D: `["👻", "🎃", "🕸", "[object Object]"]`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

By destructuring objects, we can unpack values from the right-hand object, and assign the unpacked value to the value of the same property name on the left-hand object. In this case, we're assigning the value "💀" to `spookyItems[3]`. This means that we're modifying the `spookyItems` array, we're adding the "💀" to it. When logging `spookyItems`, `["👻", "🎃", "🕸", "💀"]` gets logged.

</p>
</details>

---

###### 184. What's the output?

```javascript
const name = 'Lydia Hallie';
const age = 21;

console.log(Number.isNaN(name));
console.log(Number.isNaN(age));

console.log(isNaN(name));
console.log(isNaN(age));
```

- A: `true` `false` `true` `false`
- B: `true` `false` `false` `false`
- C: `false` `false` `true` `false`
- D: `false` `true` `false` `true`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

With the `Number.isNaN` method, you can check if the value you pass is a _numeric value_ and equal to `NaN`. `name` is not a numeric value, so `Number.isNaN(name)` returns `false`. `age` is a numeric value, but is not equal to `NaN`, so `Number.isNaN(age)` returns `false`.

With the `isNaN` method, you can check if the value you pass is not a number. `name` is not a number, so `isNaN(name)` returns true. `age` is a number, so `isNaN(age)` returns `false`.

</p>
</details>

---

###### 185. What's the output?

```javascript
const randomValue = 21;

function getInfo() {
  console.log(typeof randomValue);
  const randomValue = 'Lydia Hallie';
}

getInfo();
```

- A: `"number"`
- B: `"string"`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

Variables declared with the `const` keyword are not referencable before their initialization: this is called the _temporal dead zone_. In the `getInfo` function, the variable `randomValue` is scoped in the functional scope of `getInfo`. On the line where we want to log the value of `typeof randomValue`, the variable `randomValue` isn't initialized yet: a `ReferenceError` gets thrown! The engine didn't go down the scope chain since we declared the variable `randomValue` in the `getInfo` function.

</p>
</details>

---

###### 186. What's the output?

```javascript
const myPromise = Promise.resolve('Woah some cool data');

(async () => {
  try {
    console.log(await myPromise);
  } catch {
    throw new Error(`Oops didn't work`);
  } finally {
    console.log('Oh finally!');
  }
})();
```

- A: `Woah some cool data`
- B: `Oh finally!`
- C: `Woah some cool data` `Oh finally!`
- D: `Oops didn't work` `Oh finally!`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

In the `try` block, we're logging the awaited value of the `myPromise` variable: `"Woah some cool data"`. Since no errors were thrown in the `try` block, the code in the `catch` block doesn't run. The code in the `finally` block _always_ runs, `"Oh finally!"` gets logged.

</p>
</details>

---

###### 187. What's the output?

```javascript
const emojis = ['🥑', ['✨', '✨', ['🍕', '🍕']]];

console.log(emojis.flat(1));
```

- A: `['🥑', ['✨', '✨', ['🍕', '🍕']]]`
- B: `['🥑', '✨', '✨', ['🍕', '🍕']]`
- C: `['🥑', ['✨', '✨', '🍕', '🍕']]`
- D: `['🥑', '✨', '✨', '🍕', '🍕']`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

With the `flat` method, we can create a new, flattened array. The depth of the flattened array depends on the value that we pass. In this case, we passed the value `1` (which we didn't have to, that's the default value), meaning that only the arrays on the first depth will be concatenated. `['🥑']` and `['✨', '✨', ['🍕', '🍕']]` in this case. Concatenating these two arrays results in `['🥑', '✨', '✨', ['🍕', '🍕']]`.

</p>
</details>

---

###### 188. What's the output?

```javascript
class Counter {
  constructor() {
    this.count = 0;
  }

  increment() {
    this.count++;
  }
}

const counterOne = new Counter();
counterOne.increment();
counterOne.increment();

const counterTwo = counterOne;
counterTwo.increment();

console.log(counterOne.count);
```

- A: `0`
- B: `1`
- C: `2`
- D: `3`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

`counterOne` is an instance of the `Counter` class. The counter class contains a `count` property on its constructor, and an `increment` method. First, we invoked the `increment` method twice by calling `counterOne.increment()`. Currently, `counterOne.count` is `2`.

<img src="../img/KxLlTm9.png" width="400">

Then, we create a new variable `counterTwo`, and set it equal to `counterOne`. Since objects interact by reference, we're just creating a new reference to the same spot in memory that `counterOne` points to. Since it has the same spot in memory, any changes made to the object that `counterTwo` has a reference to, also apply to `counterOne`. Currently, `counterTwo.count` is `2`.

We invoke the `counterTwo.increment()`, which sets the `count` to `3`. Then, we log the count on `counterOne`, which logs `3`.

<img src="../img/BNBHXmc.png" width="400">

</p>
</details>

---

###### 189. What's the output?

```javascript
const myPromise = Promise.resolve(Promise.resolve('Promise!'));

function funcOne() {
  myPromise.then(res => res).then(res => console.log(res));
  setTimeout(() => console.log('Timeout!'), 0);
  console.log('Last line!');
}

async function funcTwo() {
  const res = await myPromise;
  console.log(await res);
  setTimeout(() => console.log('Timeout!'), 0);
  console.log('Last line!');
}

funcOne();
funcTwo();
```

- A: `Promise! Last line! Promise! Last line! Last line! Promise!`
- B: `Last line! Timeout! Promise! Last line! Timeout! Promise!`
- C: `Promise! Last line! Last line! Promise! Timeout! Timeout!`
- D: `Last line! Promise! Promise! Last line! Timeout! Timeout!`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

First, we invoke `funcOne`. On the first line of `funcOne`, we call the `myPromise` promise, which is an _asynchronous_ operation. While the engine is busy completing the promise, it keeps on running the function `funcOne`. The next line is the _asynchronous_ `setTimeout` function, from which the callback is sent to the Web API. (see my article on the event loop <a href="https://dev.to/lydiahallie/javascript-visualized-event-loop-3dif">here</a>.)

Both the promise and the timeout are asynchronous operations, the function keeps on running while it's busy completing the promise and handling the `setTimeout` callback. This means that `Last line!` gets logged first, since this is not an asynchonous operation. This is the last line of `funcOne`, the promise resolved, and `Promise!` gets logged. However, since we're invoking `funcTwo()`, the call stack isn't empty, and the callback of the `setTimeout` function cannot get added to the callstack yet.

In `funcTwo` we're, first _awaiting_ the myPromise promise. With the `await` keyword, we pause the execution of the function until the promise has resolved (or rejected). Then, we log the awaited value of `res` (since the promise itself returns a promise). This logs `Promise!`.

The next line is the _asynchronous_ `setTimeout` function, from which the callback is sent to the Web API.

We get to the last line of `funcTwo`, which logs `Last line!` to the console. Now, since `funcTwo` popped off the call stack, the call stack is empty. The callbacks waiting in the queue (`() => console.log("Timeout!")` from `funcOne`, and `() => console.log("Timeout!")` from `funcTwo`) get added to the call stack one by one. The first callback logs `Timeout!`, and gets popped off the stack. Then, the second callback logs `Timeout!`, and gets popped off the stack. This logs `Last line! Promise! Promise! Last line! Timeout! Timeout!`

</p>
</details>

---

###### 190. How can we invoke `sum` in `sum.js` from `index.js?`

```javascript
// sum.js
export default function sum(x) {
  return x + x;
}

// index.js
import * as sum from './sum';
```

- A: `sum(4)`
- B: `sum.sum(4)`
- C: `sum.default(4)`
- D: Default aren't imported with `*`, only named exports

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

With the asterisk `*`, we import all exported values from that file, both default and named. If we had the following file:

```javascript
// info.js
export const name = 'Lydia';
export const age = 21;
export default 'I love JavaScript';

// index.js
import * as info from './info';
console.log(info);
```

The following would get logged:

```javascript
{
  default: "I love JavaScript",
  name: "Lydia",
  age: 21
}
```

For the `sum` example, it means that the imported value `sum` looks like this:

```javascript
{ default: function sum(x) { return x + x } }
```

We can invoke this function, by calling `sum.default`

</p>
</details>

---

###### 191. What's the output?

```javascript
const handler = {
  set: () => console.log('Added a new property!'),
  get: () => console.log('Accessed a property!'),
};

const person = new Proxy({}, handler);

person.name = 'Lydia';
person.name;
```

- A: `Added a new property!`
- B: `Accessed a property!`
- C: `Added a new property!` `Accessed a property!`
- D: Nothing gets logged

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

With a Proxy object, we can add custom behavior to an object that we pass to it as the second argument. In this case, we pass the `handler` object which contained to properties: `set` and `get`. `set` gets invoked whenever we _set_ property values, `get` gets invoked whenever we _get_ (access) property values.

The first argument is an empty object `{}`, which is the value of `person`. To this object, the custom behavior specified in the `handler` object gets added. If we add a property to the `person` object, `set` will get invoked. If we access a property on the `person` object, `get` gets invoked.

First, we added a new property `name` to the proxy object (`person.name = "Lydia"`). `set` gets invoked, and logs `"Added a new property!"`.

Then, we access a property value on the proxy object, the `get` property on the handler object got invoked. `"Accessed a property!"` gets logged.

</p>
</details>

---

###### 192. Which of the following will modify the `person` object?

```javascript
const person = { name: 'Lydia Hallie' };

Object.seal(person);
```

- A: `person.name = "Evan Bacon"`
- B: `person.age = 21`
- C: `delete person.name`
- D: `Object.assign(person, { age: 21 })`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

With `Object.seal` we can prevent new properies from being _added_, or existing properties to be _removed_.

However, you can still modify the value of existing properties.

</p>
</details>

---

###### 193. Which of the following will modify the `person` object?

```javascript
const person = {
  name: 'Lydia Hallie',
  address: {
    street: '100 Main St',
  },
};

Object.freeze(person);
```

- A: `person.name = "Evan Bacon"`
- B: `delete person.address`
- C: `person.address.street = "101 Main St"`
- D: `person.pet = { name: "Mara" }`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The `Object.freeze` method _freezes_ an object. No properties can be added, modified, or removed.

However, it only _shallowly_ freezes the object, meaning that only _direct_ properties on the object are frozen. If the property is another object, like `address` in this case, the properties on that object aren't frozen, and can be modified.

</p>
</details>

---

###### 194. What's the output?

```javascript
const add = x => x + x;

function myFunc(num = 2, value = add(num)) {
  console.log(num, value);
}

myFunc();
myFunc(3);
```

- A: `2` `4` and `3` `6`
- B: `2` `NaN` and `3` `NaN`
- C: `2` `Error` and `3` `6`
- D: `2` `4` and `3` `Error`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

First, we invoked `myFunc()` without passing any arguments. Since we didn't pass arguments, `num` and `value` got their default values: num is `2`, and `value` the returned value of the function `add`. To the `add` function, we pass `num` as an argument, which had the value of `2`. `add` returns `4`, which is the value of `value`.

Then, we invoked `myFunc(3)` and passed the value `3` as the value for the argument `num`. We didn't pass an argument for `value`. Since we didn't pass a value for the `value` argument, it got the default value: the returned value of the `add` function. To `add`, we pass `num`, which has the value of `3`. `add` returns `6`, which is the value of `value`.

</p>
</details>

---

###### 195. What's the output?

```javascript
class Counter {
  #number = 10

  increment() {
    this.#number++
  }

  getNum() {
    return this.#number
  }
}

const counter = new Counter()
counter.increment()

console.log(counter.#number)
```

- A: `10`
- B: `11`
- C: `undefined`
- D: `SyntaxError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

In ES2020, we can add private variables in classes by using the `#`. We cannot access these variables outside of the class. When we try to log `counter.#number`, a SyntaxError gets thrown: we cannot acccess it outside the `Counter` class!

</p>
</details>

---

###### 196. What's missing?

```javascript
const teams = [
  { name: 'Team 1', members: ['Paul', 'Lisa'] },
  { name: 'Team 2', members: ['Laura', 'Tim'] },
];

function* getMembers(members) {
  for (let i = 0; i < members.length; i++) {
    yield members[i];
  }
}

function* getTeams(teams) {
  for (let i = 0; i < teams.length; i++) {
    // ✨ SOMETHING IS MISSING HERE ✨
  }
}

const obj = getTeams(teams);
obj.next(); // { value: "Paul", done: false }
obj.next(); // { value: "Lisa", done: false }
```

- A: `yield getMembers(teams[i].members)`
- B: `yield* getMembers(teams[i].members)`
- C: `return getMembers(teams[i].members)`
- D: `return yield getMembers(teams[i].members)`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

In order to iterate over the `members` in each element in the `teams` array, we need to pass `teams[i].members` to the `getMembers` generator function. The generator function returns a generator object. In order to iterate over each element in this generator object, we need to use `yield*`.

If we would've written `yield`, `return yield`, or `return`, the entire generator function would've gotten returned the first time we called the `next` method.

</p>
</details>

---

###### 197. What's the output?

```javascript
const person = {
  name: 'Lydia Hallie',
  hobbies: ['coding'],
};

function addHobby(hobby, hobbies = person.hobbies) {
  hobbies.push(hobby);
  return hobbies;
}

addHobby('running', []);
addHobby('dancing');
addHobby('baking', person.hobbies);

console.log(person.hobbies);
```

- A: `["coding"]`
- B: `["coding", "dancing"]`
- C: `["coding", "dancing", "baking"]`
- D: `["coding", "running", "dancing", "baking"]`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The `addHobby` function receives two arguments, `hobby` and `hobbies` with the default value of the `hobbies` array on the `person` object.

First, we invoke the `addHobby` function, and pass `"running"` as the value for `hobby` and an empty array as the value for `hobbies`. Since we pass an empty array as the value for `y`, `"running"` gets added to this empty array.

Then, we invoke the `addHobby` function, and pass `"dancing"` as the value for `hobby`. We didn't pass a value for `hobbies`, so it gets the default value, the `hobbies` property on the `person` object. We push the hobby `dancing` to the `person.hobbies` array.

Last, we invoke the `addHobby` function, and pass `"baking"` as the value for `hobby`, and the `person.hobbies` array as the value for `hobbies`. We push the hobby `baking` to the `person.hobbies` array.

After pushing `dancing` and `baking`, the value of `person.hobbies` is `["coding", "dancing", "baking"]`

</p>
</details>

---

###### 198. What's the output?

```javascript
class Bird {
  constructor() {
    console.log("I'm a bird. 🦢");
  }
}

class Flamingo extends Bird {
  constructor() {
    console.log("I'm pink. 🌸");
    super();
  }
}

const pet = new Flamingo();
```

- A: `I'm pink. 🌸`
- B: `I'm pink. 🌸` `I'm a bird. 🦢`
- C: `I'm a bird. 🦢` `I'm pink. 🌸`
- D: Nothing, we didn't call any method

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

We create the variable `pet` which is an instance of the `Flamingo` class. When we instantiate this instance, the `constructor` on `Flamingo` gets called. First, `"I'm pink. 🌸"` gets logged, after which we call `super()`. `super()` calls the constructor of the parent class, `Bird`. The constructor in `Bird` gets called, and logs `"I'm a bird. 🦢"`.

</p>
</details>

---

###### 199. Which of the options result(s) in an error?

```javascript
const emojis = ['🎄', '🎅🏼', '🎁', '⭐'];

/* 1 */ emojis.push('🦌');
/* 2 */ emojis.splice(0, 2);
/* 3 */ emojis = [...emojis, '🥂'];
/* 4 */ emojis.length = 0;
```

- A: 1
- B: 1 and 2
- C: 3 and 4
- D: 3

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The `const` keyword simply means we cannot _redeclare_ the value of that variable, it's _read-only_. However, the value itself isn't immutable. The properties on the `emojis` array can be modified, for example by pushing new values, splicing them, or setting the length of the array to 0.

</p>
</details>

---

###### 200. What do we need to add to the `person` object to get `["Lydia Hallie", 21]` as the output of `[...person]`?

```javascript
const person = {
  name: "Lydia Hallie",
  age: 21
}

[...person] // ["Lydia Hallie", 21]
```

- A: Nothing, object are iterable by default
- B: `*[Symbol.iterator]() { for (let x in this) yield* this[x] }`
- C: `*[Symbol.iterator]() { yield* Object.values(this) }`
- D: `*[Symbol.iterator]() { for (let x in this) yield this }`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Objects aren't iterable by default. An iterable is an iterable if the iterator protocol is present. We can add this manually by adding the iterator symbol `[Symbol.iterator]`, which has to return a generator object, for example by making it a generator function `*[Symbol.iterator]() {}`. This generator function has to yield the `Object.values` of the `person` object if we want it to return the array `["Lydia Hallie", 21]`: `yield* Object.values(this)`.

</p>
</details>

---

###### 201. What's the output?

```javascript
let count = 0;
const nums = [0, 1, 2, 3];

nums.forEach(num => {
	if (num) count += 1
})

console.log(count)
```

- A: 1
- B: 2
- C: 3
- D: 4

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The `if` condition within the `forEach` loop checks whether the value of `num` is truthy or falsy. Since the first number in the `nums` array is `0`, a falsy value, the `if` statement's code block won't be executed. `count` only gets incremented for the other 3 numbers in the `nums` array, `1`, `2` and `3`. Since `count` gets incremented by `1` 3 times, the value of `count` is `3`.

</p>
</details>

---

###### 202. What's the output?

```javascript
function getFruit(fruits) {
	console.log(fruits?.[1]?.[1])
}

getFruit([['🍊', '🍌'], ['🍍']])
getFruit()
getFruit([['🍍'], ['🍊', '🍌']])
```

- A: `null`, `undefined`, 🍌
- B: `[]`, `null`, 🍌
- C: `[]`, `[]`, 🍌
- D: `undefined`, `undefined`, 🍌

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The `?` allows us to optionally access deeper nested properties within objects. We're trying to log the item on index `1` within the subarray that's on index `1` of the `fruits` array. If the subarray on index `1` in the `fruits` array doesn't exist, it'll simply return `undefined`. If the subarray on index `1` in the `fruits` array exists, but this subarray doesn't have an item on its `1` index, it'll also return `undefined`.

First, we're trying to log the second item in the `['🍍']` subarray of `[['🍊', '🍌'], ['🍍']]`. This subarray only contains one item, which means there is no item on index `1`, and returns `undefined`.

Then, we're invoking the `getFruits` function without passing a value as an argument, which means that `fruits` has a value of `undefined` by default. Since we're conditionally chaining the item on index `1` of`fruits`, it returns `undefined` since this item on index `1` does not exist.

Lastly, we're trying to log the second item in the `['🍊', '🍌']` subarray of `['🍍'], ['🍊', '🍌']`. The item on index `1` within this subarray is `🍌`, which gets logged.

</p>
</details>

---

###### 203. What's the output?

```javascript
console.log('I want pizza'[0]);
```

- A: `"""`
- B: `"I"`
- C: `SyntaxError`
- D: `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

In order to get an character on a specific index in a string, you can use bracket notation. The first character in the string has index 0, and so on. In this case we want to get the element which index is 0, the character `"I'`, which gets logged.

Note that this method is not supported in IE7 and below. In that case, use `.charAt()`

</p>
</details>
