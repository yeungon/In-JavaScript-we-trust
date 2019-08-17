# js.edu.vn
In JS we trust



---

###### 1. What's the output?

```javascript
function a(x){
  x++;
  return function(){
  console.log(++x)
  }
}

a(1)();
a(1)();
a(1)();

let x = a(1);
x();
x();
x();
```

- A: `123` and `123`
- B: `333` and `345`
- C: `333` and `123`
- D: `123` and `333`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

This question reminds us about Closure in JS. Closure means we can create a `stateful function` and such function can access to variable outside of its scope. In a nutshell, a closure can have access to `global` variable (scope), `father function` scope and `its` scope.

We have here 333 and 345 because first we simply call the function a. It works like a normal function and we do not see something `stateful` here. In later case, we declare a variable `x` and it stores the value of function `a(1)`, that is why we get 3. 4. 5 rather than 3, 3, 3.

This kind of gottcha gives me the feeling of `static` variable in PHP world.
</p>
</details>

---
###### 2. What's the output?

```javascript
function Name(a, b){
  this.a = a;
  this.b = b;
}

const me = Name("Vuong", "Nguyen);

console.log(!(a.length - window.a.length));
```

- A: `undefined`
- B: `NaN`
- C: `true`
- D: `false`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

We get true when in the console. The tricky part is when we create an object from the constructor function Name but we DO NOT USE `new` keywork. That makes the variable `a` global one and get the value "Vuong". Remember that it is actually a property of the global object `window` (in the browser) or `global` in the nodejs. 

We then get `a.length` ~ 5 and `window.a.length` ~ 5 which return 0. !0 returns true.

Image what would happen when we create the instance `me` with the `new` keywork. What would happen?
</p>
</details>
