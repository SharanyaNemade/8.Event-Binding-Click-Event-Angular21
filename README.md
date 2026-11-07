# Angular 21 Tutorial

# Event Binding in Angular

Event Binding in Angular is a feature that allows you to respond to user actions, such as button clicks, mouse movements, keyboard inputs, and form submissions.

It connects an HTML element's event to a method in the component's TypeScript file.

For example, when a user clicks a button, Angular can execute a function.

## 1. What is Event Binding in Angular?

Angular uses parentheses `()` to bind events.

Syntax:

HTMLWrap linesCopy codePreview

```html
<button (click)="functionName()">Click Me</button>
```

Here:

- `(click)` is the event.
- `functionName()` is the component method.
- When the button is clicked, Angular calls the method.

Example:

`app.component.html`

HTMLWrap linesCopy codePreview

```html
<button (click)="showMessage()">Click Me</button>
```

`app.component.ts`

typescript

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  standalone: true,
  templateUrl: './app.component.html'
})
export class AppComponent {

  showMessage() {
    alert('Hello Angular!');
  }

}
```

Output: When you click the button, an alert displays:

## Hello Angular\!

 Click Me Illustration of a button click event.

## 2. How to Handle Button Click Events

Angular provides the `(click)` event to handle button clicks.

Example:

HTMLWrap linesCopy codePreview

```html
<button (click)="handleClick()">
  Submit
</button>
```

TypeScript:

typescript

```typescript
export class AppComponent {

  handleClick() {
    console.log('Button clicked!');
  }

}
```

When the user clicks Submit, Angular executes `handleClick()`.

Other commonly used Angular events:

| Event | Description |
| --- | --- |
| `(click)` | Mouse click |
| `(dblclick)` | Double click |
| `(mouseover)` | Mouse enters element |
| `(mouseout)` | Mouse leaves element |
| `(keyup)` | Keyboard key released |
| `(keydown)` | Keyboard key pressed |
| `(input)` | Input value changes |
| `(change)` | Value changes |
| `(submit)` | Form submission |

## 3. Calling a Function on Button Click

You can call any component method from an HTML button using event binding.

HTML:

HTMLWrap linesCopy codePreview

```html
<button (click)="displayName()">
  Show Name
</button>

<h2>{{ name }}</h2>
```

TypeScript:

typescript

```typescript
export class AppComponent {

  name = '';

  displayName() {
    this.name = 'Welcome to Angular';
  }

}
```

How it works:

1. The user clicks the button.
2. Angular triggers the `displayName()` method.
3. The method updates the `name` property.
4. Angular updates the HTML automatically.

## 4. Calling a Function from Another Function

In Angular, you can call one component method from another method using `this`.

Example:

typescript

```typescript
export class AppComponent {

  firstFunction() {
    console.log('First Function Called');

    this.secondFunction();
  }

  secondFunction() {
    console.log('Second Function Called');
  }

}
```

HTML:

HTMLWrap linesCopy codePreview

```html
<button (click)="firstFunction()">
  Click Me
</button>
```

Output in console:

text

```text
First Function Called
Second Function Called
```

Explanation:

- The button calls `firstFunction()`.
- Inside `firstFunction()`, we call `this.secondFunction()`.
- Therefore, both functions execute.

## 5. Passing Parameters in Event Binding

You can pass parameters to component methods directly from HTML.

HTML:

HTMLWrap linesCopy codePreview

```html
<button (click)="showMessage('Hello')">
  Click Me
</button>
```

TypeScript:

typescript

```typescript
export class AppComponent {

  showMessage(message: string) {
    alert(message);
  }

}
```

You can also pass multiple parameters.

HTMLWrap linesCopy codePreview

```html
<button (click)="addNumbers(10, 20)">
  Add Numbers
</button>
```

typescript

```typescript
addNumbers(a: number, b: number) {
  console.log(a + b);
}
```

Output:

text

```text
30
```

### Passing the event object

Angular also allows you to access the original browser event using `$event`.

HTMLWrap linesCopy codePreview

```html
<button (click)="handleClick($event)">
  Click Me
</button>
```

typescript

```typescript
handleClick(event: MouseEvent) {
  console.log(event);
  console.log(event.target);
}
```

`$event` contains information about the event, such as the target element and mouse position.

## 6. Creating a Counter App Using Event Binding

Let's create a simple counter application using Angular event binding.

# Angular Counter App

Interactive example of increment and decrement events

Current Count# 0

\+ Increment

− Decrement

 Reset Counter Try clicking the buttons. The count cannot go below zero.

### Step 1: HTML Code

`app.component.html`

HTMLWrap linesCopy codePreview

```html
<h2>Counter App</h2>

<h1>{{ count }}</h1>

<button (click)="increment()">
  Increment
</button>

<button (click)="decrement()">
  Decrement
</button>

<button (click)="reset()">
  Reset
</button>
```

### Step 2: TypeScript Code

`app.component.ts`

typescript

```typescript
export class AppComponent {

  count: number = 0;

  increment() {
    this.count++;
  }

  decrement() {
    this.count--;
  }

  reset() {
    this.count = 0;
  }

}
```

### Step 3: Understanding the Code

- `count = 0` initializes the counter.
- `increment()` increases the counter by one.
- `decrement()` decreases the counter by one.
- `reset()` sets the counter back to zero.
- `{{ count }}` displays the updated value.

Angular automatically updates the view when the component property changes.

## 7. Calling One Function from Another Function

Let's understand this with a practical counter example.

Suppose we want to increment the counter and display a message whenever the button is clicked.

HTML:

HTMLWrap linesCopy codePreview

```html
<button (click)="increment()">
  Increment
</button>

<h2>{{ count }}</h2>
```

TypeScript:

typescript

```typescript
export class AppComponent {

  count = 0;

  increment() {
    this.count++;
    this.showMessage();
  }

  showMessage() {
    console.log('Counter Updated!');
  }

}
```

Execution flow:

Button Click

increment()

count++

showMessage()

Counter Updated\!

Remember: Use `this.functionName()` when calling another method of the same component class.

## 8. Preventing Negative Values in Counter

One common requirement is preventing the counter from going below zero.

There are two ways to achieve this.

Method 1: Using an if condition

typescript

```typescript
decrement() {

  if (this.count > 0) {
    this.count--;
  }

}
```

Here, the counter decreases only when its value is greater than zero.

Method 2: Using Math.max()

typescript

```typescript
decrement() {
  this.count = Math.max(0, this.count - 1);
}
```

`Math.max()` returns the greater value between zero and the calculated counter value.

For example:

| Current count | Result |
| --- | --- |
| 5 | 4 |
| 2 | 1 |
| 1 | 0 |
| 0 | 0 |

You can also disable the decrement button when the counter reaches zero.

HTMLWrap linesCopy codePreview

```html
<button
  (click)="decrement()"
  [disabled]="count === 0">
  Decrement
</button>
```

Notice that `[disabled]` is property binding, whereas `(click)` is event binding.

## 9. Common Mistakes Developers Make in Event Binding

Here are some common mistakes beginners should avoid.

### Mistake 1: Using curly braces instead of parentheses

Incorrect:

HTMLWrap linesCopy codePreview

```html
<button {click}="showMessage()">
  Click
</button>
```

Correct:

HTMLWrap linesCopy codePreview

```html
<button (click)="showMessage()">
  Click
</button>
```

### Mistake 2: Forgetting parentheses when calling a function

Incorrect:

HTMLWrap linesCopy codePreview

```html
<button (click)="showMessage">
  Click
</button>
```

Correct:

HTMLWrap linesCopy codePreview

```html
<button (click)="showMessage()">
  Click
</button>
```

### Mistake 3: Forgetting `this` when calling another method

Incorrect:

typescript

```typescript
increment() {
  count++;
  showMessage();
}
```

Correct:

typescript

```typescript
increment() {
  this.count++;
  this.showMessage();
}
```

### Mistake 4: Not initializing variables

Incorrect:

typescript

```typescript
count: number;
```

Better:

typescript

```typescript
count: number = 0;
```

### Mistake 5: Forgetting to pass parameters

Incorrect:

HTMLWrap linesCopy codePreview

```html
<button (click)="showMessage()">
  Click
</button>
```

typescript

```typescript
showMessage(message: string) {
  alert(message);
}
```

Correct:

HTMLWrap linesCopy codePreview

```html
<button (click)="showMessage('Hello Angular')">
  Click
</button>
```

### Mistake 6: Allowing negative counter values

Incorrect:

typescript

```typescript
decrement() {
  this.count--;
}
```

Correct:

typescript

```typescript
decrement() {
  if (this.count > 0) {
    this.count--;
  }
}
```

### Mistake 7: Confusing event binding with property binding

| Event binding | Property binding |
| --- | --- |
| Uses `()` | Uses `[]` |
| Responds to events | Updates element properties |
| `(click)` | `[disabled]` |
| `(input)` | `[value]` |

## 10. Practice Questions

Test your understanding of Angular event binding.

Angular Event Binding Quiz

0/4 answered

1. Which syntax is used for event binding in Angular?

\[click\]

(click)

{{click}}

{click}

2. How do you call another method inside a component method?

functionName()

this.functionName()

@functionName()

call.functionName()

3. How do you pass a parameter to an event handler?

(click)='show()'

(click)='show("Hello")'

\[click\]='show("Hello")'

{{show("Hello")}}

4. What is the correct way to prevent a counter from going below zero?

this.count++

this.count = -1

if (this.count \> 0) this.count--

this.count = 0 always

 Submit Answers

## 11. Quick Revision

| Concept | Syntax |
| --- | --- |
| Event binding | `(click)="method()"` |
| Call function | `(click)="showMessage()"` |
| Pass parameter | `(click)="showMessage(10)"` |
| Pass event | `(click)="handleClick($event)"` |
| Call another function | `this.secondFunction()` |
| Increment | `this.count++` |
| Decrement | `this.count--` |
| Prevent negative | `if (this.count > 0)` |
| Disable button | `[disabled]="count === 0"` |

Final takeaway: Angular event binding allows you to connect user actions in HTML with methods in TypeScript. Once you understand `(click)`, `$event`, passing parameters, and calling component methods, you can build interactive applications such as counters, forms, calculators, and dynamic user interfaces.
