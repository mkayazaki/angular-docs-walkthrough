# Angular official documentation

## Getting Started
### What is angular ?
Angular is a **development platform** built on **typescript** that allows developers to create single page application. It includes:
* A Component based framework.
* A Collection of official libraries for routing, forms, http requests...
* Provides all the developers tools for developing, testing, building the app.

### Essentials
#### Components
The building blocks of angular application are **Components**.\
 A single component includes: 
* Typescript class.
* HTML template.
* CSS styles.

The typescript class contains the `@Component()` decorator. It specifies:
* A CSS selector that can be used in HTML templates.
* An HTML template that shows how the component should be rendered.
* An optional CSS styles.

The following is a minimal Angular component.
```ts
import { Component } from '@angular/core';

@Component({
  selector: 'hello-world',
  template: `
    <h2>Hello World</h2>
    <p>This is my first component!</p>
  `
})
export class HelloWorldComponent {}
```

To use this component we simply write in a template:
```html
<hello-world></hello-world>
```
Angular components provides strong encapsulation that makes the code readable and easier to test.

#### Templates
As we saw earlier each component has a specific template.
For our previous example, we have defined the template inline, but we could define it on an another file and provide the file path.  

##### Interpolation
We can insert dynamic value in the template of our component using the double curly braces.

`hello-world-interpolation.component.ts`
```ts
import { Component } from '@angular/core';

@Component ({
  selector: 'hello-world-interpolation',
  templateUrl: './hello-world-interpolation.component.html'
})
export class HelloWorldInterpolationComponent {
    message = 'Hello, World!';
}
```
`hello-world-interpolation.component.html`
```html
<p>{{ message }}</p>
```

The result in the DOM will be:
```html
<p>Hello, World!</p>
```

The double curly braces instructs angular that it should evaluate the content with in them. This way we can use variables declared in the ts file, on our HTML template.

##### Property Bindings
We can also use **property bindings** to bind an HTML attribute or property to a variable declared in our component typescript class.

`hello-world-property-binding.component.ts`
```ts
import { Component } from '@angular/core';
 
@Component ({
  selector: 'hello-world-property-binding',
  templateUrl: './hello-world-property-binding.component.html'
})
export class HelloWorldPropertyBindingComponent {
  fontColor = 'blue';
}
```

`hello-world-property-binding.component.html`
```html
<p
  [style.color]="fontColor">
  You can set my color in the component!
</p>
```
The color of the text will be blue!
As you can see we have used **brackets** around the property to indicate to angular that we are binding this property to a value in the component class. We could have also used curly braces and string interpolation.  

`hello-world-property-binding.component.html`
```html
<p
  style.color="{{ fontColor }}">
  You can set my color in the component!
</p>
```
But the latter is less idiomatic ;).

##### Event Bindings
We can declare events listeners that will be called when a specific event event is triggered such as keystrokes, mouse movements, clicks and touches...

`hello-world-event-binding.component.html`
```html
<button
  (click)="onClick()">
  Trigger alert message
</button>
```

`hello-world-event-binding.component.ts`
```ts
import { Component } from '@angular/core';
 
@Component ({
  selector: 'hello-world-event-binding',
  templateUrl: './hello-world-event-binding.component.html'
})
export class HelloWorldEventBindingComponent {
  onClick() {
    alert("You clicked");
  }
 
}
```

When the user clicks on the button, an alert will pop with the message "You clicked".  
To attach an event listener we can specify the name of the event we want in parentheses.

##### Directives
The two most popular directives in angular are `*ngIf` and `*ngFor`. These two directives allows to dynamically modify the DOM structure.

We can conditionally render a specific part of the template using the `*ngIf` directive.

`hello-world-directive-ng-if.component.ts`
```ts
import { Component } from '@angular/core';
 
@Component ({
  selector: 'hello-world-directive-ng-if',
  templateUrl: './hello-world-directive-ng-if.component.html'
})
export class HelloWorldDirectiveNgIfComponent {
  isVisible = false;
}
```

`hello-world-directive-ng-if.component.html`
```html
<p *ngIf="isVisible">This text won't be shown</p>
```

The text won't be show because isVisible is false. We can also provide a template to show when the condition is not met. To create a reusable template inside our HTML we can use the `ng-template` selector without forgetting to set an `#id`.

`hello-world-directive-ng-if.component.html`
```html

<ng-template #textShown>
  This text will be shown
</ng-template>

<p *ngIf="isVisible; else #textShown">This text won't be shown</p>
```

#### Dependency Injection
Dependency injection allows us to declare the dependencies of our typescript class without worrying about instantiation.

```ts
import { Injectable } from '@angular/core';

@Injectable({providedIn: 'root'})
export class UserService {
  add(user: User) {
    // ...
  }
}
```

```ts
import { Component } from '@angular/core';
import { UserService } from '../logger.service';

@Component({
  selector: 'hello-world-di',
  templateUrl: './hello-world-di.component.html'
})
export class HelloWorldDependencyInjectionComponent  {
  user = { name: "user " }

  constructor(private userService: UserService) { }

  addUser() {
    userService.add(user)
  }
}
```

#### Angular CLI
Angular provides a power CLI tool that allows to do numerous tasks much easier. Some examples are:
* ng build
* ng serve
* ng generate
* ng test
* ng e2e2

#### Angular First party libraries
Unlike react, Angular comes with official libraries to handle routing, forms, HTTP client, animation and much more!

## Conclusion
Angular is a component based development platform. Each component is defined by a typescript class, HTML template and CSS styles. The essential features of angular are:
* Components
* Interpolation
* Property bindings
* Event bindings
* Directives
* Templates
* Dependency Injection
* Angular CLI
* First party libraries for routing, forms, HTTP and much more....
