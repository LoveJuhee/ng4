# ng4 - Small Angular 4 Projects for Learning and Fun

## First App (`app1`)

__Download Node.js, if necessary__

I tried to upgrade to the latest version (7.7.4 with npm 4.1.2), but was then unable to install the Angular CLI (see below), so I downgraded to the LTS version (6.10.1 with npm 3.10.10). I was then able to install the CLI and create a new Angular app (see below). NOTE: I ran `$ npm cache clean` after each Node.js installation to make sure a package isn't loading anything from npm's cache. Not sure if that was necessary.

__Install CLI tool and create new app__

```
$ npm install -g @angular/cli
$ ng new app1 # 'app1' is the name of the new app
```

__Build and serve it__

```
$ ng serve
```

Visit http://localhost:4200 and you should see "app works!"

## CLI Deep Dive & Troubleshooting

If you want to dive deeper into the CLI and learn more about its usage, have a look at its official documentation: https://github.com/angular/angular-cli/wiki

You encountered issues during the installation of the CLI or setup of a new Angular project?

A lot of problems are solved by making sure you're using the latest version of NodeJS, npm and the CLI itself.

__Updating Node.js__

Go to http://nodejs.org and download the latest version. May be good/necessary to uninstall older versions first (Google it).

__Updating npm__

```
$ npm install -g npm
```
(`sudo` may be required on Mac/Linux)

__Updating the CLI__

```
$ npm uninstall -g angular-cli @angular/cli
$ npm cache clean
$ npm install -g @angular/cli
```

__Some common issues & solutions__

1. EADDR error (Address already in use). You might already have another ng serve process running - make sure to quit that or use `$ ng serve --port ANOTHERPORT` to serve your project on a new port

2. Changes not reflected in browser (App is not compiling). Check if the window running `$ ng serve` displays an error. If that's not the case, make sure you're using the latest CLI version and try restarting your CLI

## Install Bootstrap

From inside the `app1` folder:
```
$ npm i -S bootstrap
```

Edit the `.angular-cli.json` file to include Bootstrap:
``` javascript
"../node_modules/bootstrap/dist/css/bootstrap.min.css",
```

## How an Angular App Gets Loaded and Started

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655700?start=0)

## Creating a New Component

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655710?start=0)

## Understanding the Role of AppModule and Component Declaration

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655726?start=0)

## Using Custom Components

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655732?start=0)

## Creating Components with the CLI & Nesting Components

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655742?start=0)

Example: Generate `servers` component:
```
$ ng generate component servers
```
Same command using shorthand syntax:
```
$ ng g c servers
```

## Formatting With *Prettier*

While I've used Sublime and experimented with WebStorm and VS Code, I'm currently using Atom. To format code, I'm currently using the [prettier-atom package](https://atom.io/packages/prettier-atom). `Ctrl + Alt + F`

## Fully Understanding the Component Selector

You can select by element (e.g., `<app-servers></app-servers>`), attribute (e.g. `<div app-servers></div>`), or class (e.g., `<div class="app-servers"></div>`). You __can't__ select by id. Typically use elements with/for components.

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655772?start=0)

## Practice Making Components (`ass1`)

* Generated one with `$ ng g c SuccessAlert` and one by hand.
* Used `templateUrl` and `StyleUrls` with one and  `template` and `styles` (i.e., 'inline') with the other.
* Used applicable Bootstrap `alert` classes. See this [video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/practice/266/instructor-solution) for style-by-hand example.

## Data Binding

__Videos__

1. [String Interpolation](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655804?start=0) uses `{{ someString }}`
2. [Property Binding](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655806?start=0) uses `[someProperty]`
3. [Event Binding](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655820?start=0) uses `(someEvent)`
4. Combine 'Property' and 'Event' binding with `[(ngModel)]="someProperty"`

[Property Binding vs String Interpolation](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655814?start=0)

__Which Properties and Events can you bind to?__

Pretty much all of them. Use `console.log(foo)` to see something properties and events.

Example: Binging a method to a click event:
``` html
<button class="btn btn-primary" (click)="doSomething()">Do Something</button>
```

## Passing and Using Data with Event Binding

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655832?start=0)

## Two-Way Data Binding

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655868?start=0)

For Two-Way-Binding to work, you need to enable the `ngModel`  directive. This is done by adding the `FormsModule`  to the `imports[]`  array in the `AppModule`. You then also need to add the import from `@angular/forms`  in the `app.module.ts` file:
``` javascript
import { FormsModule } from '@angular/forms';
```

## Directives

Directives are instructions in the DOM (Components are a type of Directive with a template). Typically add directives with an Attribute selector (but can add with the other ways as well, if want/necessary).

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655898?start=0)

__ngIf Example__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655904?start=0)

``` javascript
<p *ngIf="serverCreated">Server was created, server name is {{ serverName }}</p>
```
The `*` is required because ngIf is a __Structural Directive__, which means it changes the structure of the DOM (in this case, it either adds the Element or it doesn't).

__ngIf else Example__

[Vide](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655984?start=0)

``` html
<p *ngIf="serverCreated; else noServer">Server was created, server name is {{ serverName }}</p>
<ng-template #noServer>
  <p>Server has not been created yet</p>
</ng-template>
```

The `noServer` is called a 'Local Reference.'

__ngStyle__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655914?start=0)

`ngStyle` is and __Attribute Directive__. Unlike Structural Directives, Attribute Directives don't *add* or *remove* elements. Instead, they *change* the element they are placed on.

__ngClass__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655924?start=0)

__ngFor__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655930?start=0)

## Course Project (`proj1`)

A recipe book / shopping list app. See [video clip](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6655594?start=14s).

__Intro Videos__

1. [Intro](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656000?start=0)
2. [Planning](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656004?start=0)
3. [Setup](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656008?start=0)

__Project Setup__

```
$ ng new proj1
$ cd proj1
$ ng serve
```

__Install Bootstrap__

```
$ npm i -S bootstrap
```

Edit `.angular-cli.json` to add `"../node_modules/bootstrap/dist/css/bootstrap.min.css",` line to `styles` array. Edit `app.component.html` to 'Hello World' Bootstrap.

```
$ ng serve
```

__Create Components__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656014?start=60)

1. Create `header` component manually (for practice).
2. Create all other components with the CLI:

```
$ ng g c recipes --spec false
$ ng g c recipes/recipe-list --spec false
$ ng g c recipes/recipe-list/recipe-item --spec false
$ ng g c recipes/recipe-detail --spec false
$ ng g c shopping-list --spec false
$ ng g c shopping-list/shopping-edit --spec false
```

__Place Components__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656016?start=0)

__Unix Command to Find and Remove Files__

I used this to remove files ending in .orig after using resolving merge conflict:
```
$ find . -type f -name '*.orig' -delete
```
1. [Source](http://unix.stackexchange.com/a/116390/224872) (StackExchange *Recursively delete all files with a given extension*)
2. [More about the `find` command]( https://www.cyberciti.biz/faq/howto-find-a-file-under-unix/) (CyberCiti.biz FAQ)

__Configure Navbar__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656020?start=0)

__Create Recipe Model__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656026?start=0)

__Design RecipeItem__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656030?start=0)

__Output List of Recipes With ngFor__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656034?start=0)

__Design RecipeDetail__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656036?start=0)

__Design ShoppingListComponent__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656038?start=0)

__Create Ingredient Model__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656040?start=0)

__Creating and Outputting the Shopping List__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656042?start=0)

__Design ShoppingEditComponent__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656046?start=0)

__Next Steps__

[Video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656048?start=0)

## Debugging Videos

1. [Angular Error Messages](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656252?start=0)
2. [Debugging Code in the Browser Using Sourcemaps](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656260?start=0)
3. [Using Augury to Dive into Angular Apps](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656262?start=0)

## Components & Databinding Deep Dive

* [Intro](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656058?start=0)
* [Splitting Apps into Components](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656060?start=0)
* [Property & Event Binding Overview](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656062?start=0)
* [Binding to Custom Properties](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656066?start=0) (good video to rewatch)
* [Assigning an Alias to Custom Properties](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656072?start=0)
* [Binding to Custom Events](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656076?start=0) (good video to rewatch)
* [Assigning an Alias to Custom Events](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656078?start=0)
* [Custom Property and Event Binding Summary](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656080?start=0)
* [Understanding View Encapsulation](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656082?start=0)
* [More on View Encapsulation](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656086?start=0)
* [Using Local References in Templates](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656092?start=0) (good video to rewatch)
* [Getting Access to the Template & DOM with @ViewChild](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656094?start=0) (good video to rewatch)
* [Projecting Content into Components with ng-content](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656100?start=0) (good video to rewatch)
* [Understanding the Component Lifecycle, such as ngOnInit](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656102?start=0) (good video to rewatch)
* [Seeing Lifecycle Hooks in Action](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656106?start=0) (good video to rewatch)
* [Lifecycle Hooks and Template Access](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656110?start=0) (good video to rewatch)
* [Getting Access to ng-content with @ContentChild](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656114?start=0) (good video to rewatch)
* [Wrap Up](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656116?start=0)

## Practicing Property & Event Binding and View Encapsulation (`ass4-cmps-dbnd`)

Great practice. See [video](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/practice/272/introduction) and [commits](https://github.com/chrisco/ng4/commits/master) for details (`$ git log --grep="Ass 4"`).

## Course Project, Continued (`proj1`)

__Videos__

* [Adding Navigation with Event Binding and ngIf](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656142?start=0)
* [Passing Recipe Data with Property Binding](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656142?start=0)
* [Passing Data with Event and Property Binding (Combined)](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656144?start=0)
* [Allowing the User to Add Ingredients to the Shopping List](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656156?start=0)

## Directives Deep Dive

__Videos__

* [Module Introduction](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656162?start=0)
* [ngFor and ngIf Recap](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656164?start=0)
* [ngClass and ngStyle Recap](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656166?start=0)
* [Creating a Basic Attribute Directive](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656170?start=0)
* [Using the Renderer to build a Better Attribute Directive](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656172?start=0)
```
$ ng g d better-highlight --spec false
```
* [More about the Renderer](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6730946?start=0)
* [Using HostListener to Listen to Host Events](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656176?start=0)
* [Using HostBinding to Bind to Host Properties](https://www.udemy.com/the-complete-guide-to-angular-2/learn/v4/t/lecture/6656178?start=0)
* [Binding to Directive Properties]()
* [What Happens behind the Scenes on Structural Directives]()
* [Building a Structural Directive]()
* [Understanding ngSwitch]()
