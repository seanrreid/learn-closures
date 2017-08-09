
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

#### Example 2.b
- What will the `totalOfSums` return?
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
```

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

