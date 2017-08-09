
### Example 1

- What will the following code return?
- Where does the _closure_ occur?

```
function introduction() {
  var phrase1 = "My Name is ";
  var phrase2 = "Mr. Roboto"
  
  function displayIntroduction() { 
    console.log(phrase1+phrase2);    
  }
  displayIntroduction();    
}

introduction();
```
#### Answer:
- `"My Name is Mr. Roboto"`
- The `displayIntroduction()` function is a _closure_. It is a function object returned by the `introduction()` first class function. 

### Example 2
Source: [https://www.reddit.com/r/javaScriptStudyGroup/comments/48aaz1/week_7_focus_closures/d0otqbf/](https://www.reddit.com/r/javaScriptStudyGroup/comments/48aaz1/week_7_focus_closures/d0otqbf/)

**Closures** are created by a function object and the _free_ variables inside that function (or, more specifically, what those variables reference).

A **_free_/non-local_ variable** is a variable that was not instantiated inside a function. For example, it was neither locally declared nor passed as parameter (i.e. assigned via LHS, implied LHS, or RHS).

#### Example 2.a
- List the _free_ variables.
- List the _declared variables.
- What will `totalOfSums` return?

```
function plus(a, b) {
  var sum = a + b;

  totalOfSums += sum;
  console.log('The total of all sums you have calculated is: ' + totalOfSums);

  return sum;
}
```
#### Answer
- Free: `totalOfSums` 
- Declared: `sum`,`a`,`b` 
- `undefined`

#### Example 2.b
- What will the `plus(1,2)` return?
- Where is the _closure_?

```
function sums() {
  var totalOfSums = 0;

  return function(a, b) {
    var sum = a + b;

    totalOfSums += sum;
    console.log('The total of all sums you have calculated is: ' + totalOfSums);

    return sum;
  };
}

var plus = sums();
plus(1,2);

```

#### Answer
- `"The total of all sums you have calculated is: 3"`
- The _closure_ is created when we instantiate the `plus` object.
- The `return function()` expression is an **IIFE**

#### Why?
See Example 3. :)

### Example 3
Source: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)

> A _closure_ is the combination of a function and the lexical environment within which that function was declared. This environment consists of any local variables that were in-scope at the time that the closure was created. 

- What is the output of `myFunc()`?

```
function makeFunc() {
  var name = 'Mozilla';
  function displayName() {
    console.log(name);
  }
  return displayName;
}

var myFunc = makeFunc();
myFunc();
```

#### Answer
- `"Mozilla"`

#### Why?
> In this case, `myFunc` is a **reference** to the instance of the function `displayName` created when `makeFunc` is run.
> The instance of `displayName` maintains a reference to its lexical environment, within which the variable name exists. 
> For this reason, when `myFunc` is invoked, the **variable name remains available** for use and "Mozilla" is passed to alert.

### Example 4
Source: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)

- What is the output of `console.log(add5(2));`?
- What is the output of `console.log(add10(2));`?
- Where do _closures_ occur? 

```
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);

console.log(add5(2));
console.log(add10(2));
```

#### Answer
- `7`
- `12`
- `add5` and `add10` create _closures_.

#### Why??
> `makeAdder` is [essentially], a function factory — it creates functions which can add a specific value to their argument. 
> In the above example we use our function factory to create two new functions — one that adds 5 to its argument, and one that adds 10.
> [These new functions],`add5` and `add10`, are both closures. They share the same function body definition, but store different lexical environments. [In the lexical environment for] `add5`, `x` is 5, while in the lexical environment for `add10`, `x` is 10.


#### Example 5 

- Based on the following HTML, what will the javascript output?
- What change would you make to get the desired output?

```
  <button>Button 1</button>
  <button>Button 2</button>
  <button>Button 3</button>
  <button>Button 4</button>
```

```
var nodes = document.getElementsByTagName('button');
for (var i = 0; i < nodes.length; i++) {
   nodes[i].addEventListener('click', function() {
      console.log('You clicked element #' + i);
   });
}
```
- "You clicked element #4"
- You could add an _IIFE_ function, or another function, to the previous example:
```
var nodes = document.getElementsByTagName('button');
for (var i = 0; i < nodes.length; i++) {
   nodes[i].addEventListener('click', (function(i) {
      // IIFE GOES HERE
      return function() {
         console.log('You clicked element #' + i);
      }
   })(i));
}
```

#### Why??
The _terminating condition_ of the loop is when i is **greater than 3** (based on the node placement in the array). The output of **4** is the value of the `i` after the loop terminates.

The loop originally did _not_ capture its own copy of `i`.  The way scope works, the event is closed over the _same shared global scope_, which has, in fact, only one `i` in it. As such, we get the same value each time a button is clicked. 

An _IIFE_ creates its **own scope** as part of an _inner function_ object. Note that, the syntax `(i))` at the close of the `addEventListener` function executes the `return function()` expression immediately, and passes `i` as a value. 
