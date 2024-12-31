# Angular

## High Level Goals

By the end of this lesson, you will be familiar with the following:

- Angular
- Angular CLI
- Components
- Event And data Binding

## Angular

Angular is a platform and framework made by Google for building single-page client applications using HTML and TypeScript. Angular is written in TypeScript and is used to develop applications For web, mobile web, native mobile and native desktop.

### Installing And Setting Up An Angular Project

To install Angular and manage angular apps use the Angular [CLI](https://cli.angular.io/).

#### Installing Angular CLI

```cmd
npm install -g @angular/cli
```

#### Creating And Running A New Project

The first command is used to generate a new applications, during that process you will asked few questions to determine how the application will be.

```cmd
ng new my-app

cd my-app

ng serve
```

### Angular File Structure

Here is a quick guide that explains some of the files that gets generated when using `ng new app-name`. Assuming that the app uses CSS and generated with routing.

For more information about read the documentation about the [file-structure](https://angular.io/guide/file-structure).

- `src/index.html`: it's the main html page that holds the div (app-root) that angular gets rendered in.
- `src/styles.css`: it's the main css file that holds the global styles.
- `src/main.ts`: The main entry point for your application.
- `src/app/app.modules.ts`: Defines the root module that tells Angular how to assemble the application.
- `src/app/app-routing.module.ts`: The main file for routing.
- `src/app/app.component.ts`: Defines the logic for the application's root component `AppComponent`
- `src/app/app.component.html`: Defines the HTML template associated with the root `AppComponent`.
- `src/app/app.component.css`: Defines the base CSS stylesheet for the root `AppComponent`.

### Angular Components

The main component for Angular is the `AppComponent` and we could modify the it by changing it's related `.ts`, `.html`, and `.css` files.

in `src/app/app.component.ts` there is a component decorator that has three properties:

- selector: it defines the html tag name to reference the application
- templateUrl: it defines the path for the html file that is connected to the component.
- stylesUrls: it defines the path for the the css files that are connected to the component.

```js
import { Component } from "@angular/core";

@Component({
  selector: "app-root",
  templateUrl: "./app.component.html",
  styleUrls: ["./app.component.css"],
})
export class AppComponent {
  // the class holds the logic for the application
}
```

### Generating Components

To generate a new component using angular cli use the following command, when generating the component angular will create a folder with the three used files ( ts, html, css) inside the app directory and import the component to use it in `src/app/app.modules.ts`.

```cmd
ng generate component home
```

it could also be ran as

```cmd
ng g c home
```

home.component.ts

```js
import { Component, OnInit } from "@angular/core";

@Component({
  // use the selector as a tag name in another component's html file to render the component inside
  selector: "app-home",
  templateUrl: "./home.component.html",
  styleUrls: ["./home.component.css"],
})
export class HomeComponent implements OnInit {
  // class constructor
  constructor() {}

  // a life cycle method that runs when the component is initialized
  ngOnInit(): void {}
}
```

app.component.html

```html
<!-- the line below will be replaced with the home component -->
<app-home></app-home>
```

### Passing Properties

app.component.ts

```js
import { Component } from "@angular/core";

@Component({
  selector: "app-root",
  templateUrl: "./app.component.html",
  styleUrls: ["./app.component.css"],
})
export class AppComponent {
  name: string = "John Doe";
}
```

app.component.html

```html
<!-- the attribute must exist in the home component, [name] is an attribute in home component -->
<!-- the value for the attribute must exist in the app component, "name" is not a string it is an attribute -->
<app-home [name]="name"></app-home>
```

```js
// import Input to be able to accept the passed property
import { Component, OnInit, Input } from "@angular/core";

@Component({
  selector: "app-home",
  templateUrl: "./home.component.html",
  styleUrls: ["./home.component.css"],
})
export class HomeComponent implements OnInit {
  // this class is expecting a property (name) to be passed
  @Input() name: String = "";

  constructor() {}

  // a method ran when the component is initialized
  ngOnInit(): void {}
}
```

### Directives And Data Binding

Angular supports two types of data binding:

**Event binding**: makes the application respond to input by updating the application data.

**Property binding**: interpolate values that are computed from the application data into the HTML.

```js
import { Component, OnInit } from "@angular/core";

@Component({
  selector: "app-home",
  templateUrl: "./home.component.html",
  styleUrls: ["./home.component.css"],
})
export class HomeComponent implements OnInit {
  name: string = "John";
  age: number = 21;
  todos: string[] = ["eat", "study", "sleep"];
  email: string = "";

  constructor() {}

  ngOnInit(): void {}

  showTodo(todo: string): void {
    console.log(`TODO: ${todo}`);
  }
}
```

home.component.html

```html
<!-- iterate over an array using ngFor directive -->
<ul *ngFor="let todo of todos; let i = index">
  <li>{{i}}. {{todo}}</li>
  <button (click)="showTodo(todo)">Click me</button>
</ul>
```

app.modules.ts

```js
import { NgModule } from "@angular/core";
import { BrowserModule } from "@angular/platform-browser";
// import FormsModule to be able to use the ngModel directive
import { FormsModule } from "@angular/forms";

import { AppRoutingModule } from "./app-routing.module";
import { AppComponent } from "./app.component";
import { HomeComponent } from "./home/home.component";

@NgModule({
  declarations: [AppComponent, HomeComponent],
  // add FormsModule to imports
  imports: [BrowserModule, AppRoutingModule, FormsModule],
  providers: [],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

home.component.html

```html
<!-- ngModel will bind the input value with the email attribute -->
<input type="text " [(ngModel)]="email" placeholder="email" />
<!-- when the email attribute changes it will update the email value in the html -->
<p>The email is: {{email}}</p>
```

### Practice

This practice will test your autonomous learning abilities so make sure to rely on documentation as much as possible.

1. Learn about conditional rendering using `*ngIf`, `ng-template`.
2. Learn about style binding `[style], [ngStyle]`.
3. Learn about class binding `[class], [ngClass]`.
4. Learn about Routing, adding routes in `app-routing.module.ts`, `routerLink` and `router-outlet`.
5. Learn about about Output and EventEmitter.
6. Learn about Angular's life cycle.
7. Create a full CRUD todo list app using angular (frontend only) by using what you have learnt in the lesson and read, use whatever tools you find fit to achieve that goal, as a general guideline make sure to use routing, dynamic styling/rendering and reuseable components at least (`TodosComponent` and `TodoComponent`).
8. Learn about Services (generating service, creating an http service using `HttpClientModule`).
9. Convert the application into a fullstack app by using what you learnt about creating an http service, you may use the database of your choosing.
