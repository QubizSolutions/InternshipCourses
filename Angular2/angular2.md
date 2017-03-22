# Introduction to Angular 2

Angular 2 is the next version of Google’s massively popular MV* framework for building complex applications in the browser (and beyond).

Angular 2 comes with almost everything you need to build a complicated frontend web or mobile apps, from powerful templates to fast rendering, data management, HTTP services, form handling, and so much more.

## Angular basics

 Angular applications are made up of components. A component is the combination of an HTML template and a component class that controls a portion of the screen. Here is an example of a component that displays a simple string:

 ```TYPESCRIPT
import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `<h1>Hello {{name}}</h1>`
})
export class AppComponent { name = 'Angular'; }
 ```

 Every component begins with an **@Component** decorator function that takes a **metadata** object. The metadata object describes how the HTML template and component class work together.

 The **selector** property tells Angular to display the component inside a custom ```<my-app>``` tag in the **index.html**.

 ```HTML
<my-app>Loading AppComponent content here ...</my-app>
 ```

 The template property defines a message inside an ```<h1>``` header. The message starts with **"Hello"** and ends with **{{name}}**, which is an Angular interpolation binding expression. At runtime, Angular replaces {{name}} with the value of the component's name property. Interpolation binding is one of many Angular features you'll discover in this course.

 ## In this course we will cover:

 [1. High level overview](#high-level-overview)

 [2. Modules](#modules)

 [3. Components](#components)

 [4. Directives](#directives)

 [5. Services](#services)

 [6. Routing](#routing)

 [7. References](#references)

 ## <a name="high-level-overview"></a>1. High level overview

 [HighLevelArchitecture]: https://github.com/QubizSolutions/InternshipCourses/blob/master/Angular2/Content/high_level_architecture.png "Angular 2 high level architecture"

![alt text][HighLevelArchitecture]

* **Modules** - main building blocks that contain routes, components, services, etc
  * There can be multiple modules within an application based on different functionality areas

* **Components** - contain templates, data and logic, froming part of a DOM tree

* **Directives** - attach behaviour, extend or transform a particular element and its children

* **Services** - data layer, logic that is not component related, ex: API requests, calculations

* **Routing** - renders a component based on the URL state, drives navigation

 ## <a name="modules"></a>2. Modules

***Angular modules consolidate components, directives and pipes into cohesive blocks of functionality... Modules can also add services***

Angular applications are modular and every of them has at least one module class, which is called the **root module**(AppModule)

While the root module may be the only module in a small application, most apps have many more feature based modules as well

Root module example: 
```TYPESCRIPT
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { DataService } from './data.service';
import { AppComponent } from './app.component';

@NgModule({
  imports:      [ BrowserModule ],
  providers:    [ DataService ],
  declarations: [ AppComponent ],
  exports:      [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

Every angular module is a class with a mandatory ```@NgModule``` decorator - **decorators** allow developers to configure classes as particular elements by setting metadata on them

The most important propertises of the ```@NgModule``` decorator are:
* ```imports``` - specifies a list of modules whose exported directives/pipes should be available to templates in this module
* ```exports``` - specifies a list of angular primitives that can be used within the template of any component that is part of an Angular module that imports this module
* ```declarations``` - the view classes that belong to the module. Theese can only be **components**, **directives** and **pipes**
* ```providers``` - a set of injectable objects that are available in the injector of this module
* ```bootstrap``` - the main application view, called the root component, that hosts all other app views. Only the root module should set this bootstrap property

 ## <a name="components"></a>3. Components

In Angular 2 any element of a web application can be a component.

Components are the main of building elements and logic on the page. 

Component example: 

app.component.ts
```TYPESCRIPT
import { Component } from '@angular/core';
import { Person } from './person.interface';

@Component({
  selector: 'app-component',
  styleUrls: ['app.component.css'],
  templateUrl: 'app.component.html',
})
export class AppComponent {
  name: string = 'Tony';
  personDetail: Person = {
    firstName: 'Tony',
    lastName: 'Stark',
    age: 44
  }
  
  constructor() {  }
  
  sayMyName() {
    console.log('My name is', this.name)
  }
}
```

app.component.html
```html
<div>
    Hello my name is {{name}}.
    <person-detail [person]="personDetail"></person-detail>
    <button (click)="sayMyName()">Say my name</button>
    <input [(ngModel)]="personDetail.firstName">
</div>
```

A component is a class with the ```@Component``` decorator. The main properties of the decorator are:
* **selector** - it tells Angular to  create and insert an instance of this component where it finds a ```<app-component>``` tag in parent HTML. For example, if an app's HTML contains ```<app-component></app-component>```, then Angular inserts an instance of the ```AppComponent``` view between those tags.
* **templateUrl** - url to an external file containing a template for the view
* **styleUrls** - list of urls to stylesheets to be applied to this component's view

### **Data binding**
[DataBinding]: https://github.com/QubizSolutions/InternshipCourses/blob/master/Angular2/Content/data_binding.png "Data binding"


Data binding is the synchronization of data between the model and view components

![alt text][DataBinding]

There are four forms of data binding:

* **interpolation** - ```{{name}}``` - displays the component's ```name``` property in between the tags where it is used
* **property binding** - ```[person]="personDetail"``` - passes the value of the ```personDetail``` property from the parent component to the ```person``` property of the child component
* **event binding** - ```(click)="sayMyName()"``` - calls the component's sayMyName method when the user click's the button
* **two-way data binding** - ```[(ngModel)]="personDetail.firstName"``` - combines the property and the event binding using the ```ngModel``` directive
  * a data property value flows to the input box from the component as with property binding
  * the user's changes also flow back to the component, resetting the property to the latest value, as with event binding

### **Lifecycle Hooks**

[LifecycleHooks]: https://github.com/QubizSolutions/InternshipCourses/blob/master/Angular2/Content/lifecycle-hooks.png "Lifecycle Hooks"

Angular calls lifecycle hook methods on directives and components as it creates, changes, and destroys them

![alt text][LifecycleHooks]

* **ngOnChanges()** - Respond when Angular (re)sets data-bound input properties. The method receives a SimpleChanges object of current and previous property values. Called before ```ngOnInit()``` and whenever one or more data-bound input properties change

* **ngOnInit()** - Initialize the directive/component after Angular first displays the data-bound properties and sets the directive/component's input properties. Called once, after the first ```ngOnChanges()```

* **ngDoCheck()** - Detect and act upon changes that Angular can't or won't detect on its own. Called during every change detection run, immediately after ```ngOnChanges()``` and ```ngOnInit()```

* **ngAfterContentInit()** - Respond after Angular projects external content into the component's view. Called once after the first ```ngDoCheck()```

* **ngAfterContentChecked()** - Respond after Angular checks the content projected into the component. Called after the ```ngAfterContentInit()``` and every subsequent ```ngDoCheck()```

* **ngAfterViewInit()** - Respond after Angular initializes the component's views and child views. Called once after the first ```ngAfterContentChecked()```

* **ngAfterViewChecked()** - Respond after Angular checks the component's views and child views. Called after the ```ngAfterViewInit``` and every subsequent ```ngAfterContentChecked()```

* **ngOnDestroy()** - Cleanup just before Angular destroys the directive/component. Unsubscribe Observables and detach event handlers to avoid memory leaks. Called just before Angular destroys the directive/component


```TYPESCRIPT
import {
  OnChanges, SimpleChange,
  OnInit,
  DoCheck,
  AfterContentInit,
  AfterContentChecked,
  AfterViewInit,
  AfterViewChecked,
  OnDestroy
} from 'angular2/core';

@Component {
  selector: 'my-component',
  template: ''
}
export class MyComponent implements
              OnChanges, OnInit, DoCheck,
              AfterContentInit,AfterContentChecked,
              AfterViewInit, AfterViewChecked,
              OnDestroy {

  ngOnInit() {
    // Properties resolved
  }
  ngOnDestroy() {
    // Fin.
  }
  ngDoCheck() {
    // Custom change detection
  }
  ngOnChanges(changes) {
    // Bindings changed
  }
  ngAfterContentInit() {
    // Component content has been initialized
  }
  ngAfterContentChecked() {
    // Component content has been Checked
  }
  ngAfterViewInit() {
    // Component views are initialized
  }
  ngAfterViewChecked() {
    // Component views have been checked
  }

}

```

 ## <a name="directives"></a>4. Directives

A directive is a class with a ```@Directive``` decorator

Angular has three kinds of directives: 
* **component** - it's *directive with a template*, the ```@Component``` decorator which extends the ```@Directive``` decorator with template-oriented features
* **structural** - changes the DOM by adding, replacing and removing elements
* **attribute** - changes the appearence or behavior of a DOM element

### **Structural directives**

* **NgFor** - its a repeater that can be used to display a list of items
```HTML
<ul>
  <li *ngFor="let person of persons">
    {{ person.name }}
  </li>
</ul>
```

* **NgIf** - it removes or recreates a part of DOM tree depending on an expression evaluation

```HTML
<p class="alert alert-success" *ngIf="persons.length > 2">Currently there are more than 2 names!</p>
<p class="alert alert-danger" *ngIf="persons.length <= 2">Currently there are less than 2 names left!</p>
```

### **Attribute directives**
The attribute directive changes the appearance or behavior of a DOM element. 
These directives look like regular HTML attributes in templates. 

```TYPESCRIPT
import { Directive, ElementRef, Input } from '@angular/core';

@Directive({ 
  selector: '[myHighlight]' 
})
export class HighlightDirective {
    constructor(el: ElementRef) {
       el.nativeElement.style.backgroundColor = 'yellow';
    }
}
```

```HTML
<p myHighlight>Highlight me!</p>
```

```@Directive``` requires a selector to identify the HTML in the template that is associated with the directive. The selector for an attribute is the attribute name in square brackets. Here, the directive's selector is ```[myHighlight]```. 
Angular locates all elements in the template that have an attribute named ```myHighlight```

 ## <a name="services"></a>5. Services

In Angular 2 a service is typically a class with a well defined purpose.

Examples: 
* logging service
* calculation service
* data service
* configuration service
* etc

Services are fundamental to Angular applications. The biggest consumers of the services are components.

Components should only contain UI related logic (properties, models, methods for data binding), anything else needs to be placed in services

Example of a simple service: 

```TYPESCRIPT
export class LoggerService {
  log(msg: any)   { console.log(msg); }
  error(msg: any) { console.error(msg); }
  warn(msg: any)  { console.warn(msg); }
}
```

Use of the LoggerService in a component
```TYPESCRIPT
import { Component } from '@angular/core';
import { Person } from './person.interface';
import { LoggerService } from './logger.service'

@Component({
  selector: 'app-component',
  styleUrls: ['app.component.css'],
  templateUrl: 'app.component.html',
})
export class AppComponent {
  name: string = 'Tony';
  loggerService: LoggerService;
  
  constructor() {  
    this.loggerService = new LoggerService();
  }
  
  sayMyName() {
    this.loggerService.log('My name is: ' + this.name);
  }
}
```

### **Dependency injection**

It's a coding pattern in which a class receives its dependencies from external sources rather than creating them itself.

```TYPESCRIPT
import { Injectable } from '@angular/core';

@Injectable()
export class DataService {
  getData() { 
      return DATA; 
    }
}
```

The ```@Injectable()``` decorator lets Angular know that a class can be used with the dependency injector. Generally speaking, an injector reports an error when trying to instantiate a class that is not marked as ```@Injectable()```

Registering services (providers) in an NgModule

```TYPESCRIPT
@NgModule({
  imports: [
    BrowserModule
  ],
  declarations: [
    AppComponent,
    /* . . . */
  ],
  providers: [
    DataService,
  ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }
```

Injecting the service into a component

```TYPESCRIPT
import { Component } from '@angular/core';
import { DataService } from './data.service'

@Component({
  selector: 'app-component',
  styleUrls: ['app.component.css'],
  templateUrl: 'app.component.html',
})
export class AppComponent {
  
  constructor(private dataService: DataService) {  }
  
  getData() {
    let data = this.dataService.getData();
  }
}
```
### **HTTP with observables**

Making HTTP requests is a vital operation in the life of most front-end applications.

HTTP calls in Angular 2 by default return **observables** through RxJS

Using **observable** streams gives us the benefit of greater flexibility when it comes to handling the responses coming from HTTP requests


In order to use **HTTP**, it needs to be included into the module

```TYPESCRIPT
...
import { HttpModule } from '@angular/http';

@NgModule({
  ...
  imports: [ HttpModule ],
  ...
})
class AppModule { }
```

Using http in a service

```TYPESCRIPT
import { Injectable } from '@angular/core';
import { Http, Response } from '@angular/http';
import { Observable } from 'rxjs/Rx';
import { HttpUtilityService } from '../common/helpers/http-utility.service';
import { Person } from './person.interface';

@Injectable()
export class DataService {
    private url = 'api/People';  // URL to web API
    constructor(private http: Http) { }
    
    getPeople(): Observable<Person[]> {
        return this.http.get(`${this.url}/GetObjectConfigs`)
            .map((response: Response)=> response.json());
    }
```

Using the service in a component
```TYPESCRIPT
import { Component } from '@angular/core';
import { DataService } from './data.service'
import { Person } from './person.interface';

@Component({
  selector: 'app-component',
  styleUrls: ['app.component.css'],
  templateUrl: 'app.component.html',
})
export class AppComponent {
  people: Person[] = [];
  constructor(private dataService: DataService) {  }
  
  getData() {
    this.dataService.getPeople().subscribe((data: Person[])=> this.people = data)
  }
}
```

 ## <a name="routing"></a>6. Routing

The Angular Router enables navigation from one view to the next as users perform application tasks.

Routing is used to separate different parts of an application, generally by using the URL to denote the location

Most routing applications should add a ```<base>``` element to the **index.html** as the first child in the ```<head>``` tag to tell the router how to compose navigation urls

```HTML
<base href="/">
```

A routed Angular app has one singleton **Router** service
When the URL in the browser changes, the router looks for the correspinging **Route** from which it can find the componet to display

Route definition

```TYPESCRIPT
import { ModuleWithProviders } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';

import { HomeComponent } from './home.component';
import { PeopleComponent } from './people.component';
import { PersonComponent } from './person.component';

const appRoutes: Routes = [
    {
        path: '',
        redirectTo: '/home',
        pathMatch: 'full',
    },
    {
        path: 'home',
        component: HomeComponent
    },
    {
        path: 'people',
        component: PeopleComponent
    },
    {
        path: 'person/:id',
        component: PersonComponent
    }
];

export const Routing: ModuleWithProviders = RouterModule.forRoot(appRoutes, { useHash: true });
```

Given the configuration, when the browser URL for this application becomes /home, the router matches that URL to the route path /home and displays the HomeComponent after a **RouterOutlet** that is placed in the host view's HTML.

```HTML
<router-outlet></router-outlet>
```

The navigation to a specific view can be done by typing the URL into the browser's address bar, or by using **router links**

```HTML
<h1>Angular Router</h1>
  <nav>
    <a [routerLink]="['/home']" [routerLinkActive]="['link-active']">Home</a>
    <a [routerLink]="['/people']" [routerLinkActive]="['link-active']">People</a>
    <a [routerLink]="['/person', {id: selectedPerson.id}]" [routerLinkActive]="['link-active']">Person</a>
  </nav>
  <router-outlet></router-outlet>
```

Navigation can also be done from typescript trough the **Router**

```TYPESCRIPT
import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';

@Component({
    ...
})
export class HomeComponent {
    ...

     constructor(private router: Router) { }

    goToPerson(id: number) {
        this.router.navigate(['/person', id]);
    }

    goToDashboard() {
        this.router.navigate(['/dashboard']);
    }
}
```

Reading route parameters

```TYPESCRIPT
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
    ...
})
export class HomeComponent implements OnInit {
    ...

    constructor(private route: ActivatedRoute) { }

    ngOnInit() {
        this.route.params.subscribe(params => {
            let id = params['id'];
        });
    }
}
```

 ## <a name="references"></a>7. References

* https://angular.io/docs/ts/latest/guide/
* http://www.tutorialspoint.com/angular2/
* https://angular-2-training-book.rangle.io

