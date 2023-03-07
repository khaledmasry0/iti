<h1 align="center"> Angular </h1>

### `Client Side Framework - Single Page application`

[cheatsheet](https://angular.io/guide/cheatsheet)

### commands

```node
npm i -g @angular/cli               to install angular
ng new App_name                     to create a new angular app
ng serve -o                         to run the application
ng g c component_name               to generate a component    // --skipTests
ng g class folderName/className     to generate a class
ng g d directive_name               to generate a directive
ng g p pipe_name                    to generate a pipe
ng g s service_name                 to generate a service
ng g g service_name                 to generate a guard
```

### folders & files

- - e2e => for testing
- - src => app place
- main.js => All code
- vendor.js => All libraries and compiler
- style.js => control the styles
- polyfills.js => close the gap between browsers
- runtime.js => from where calling starts

- #### primeNG : UI library

- #### Data Binding:

  #### `expession embadded in template and be evaluated bind between template and component class`

### - starting

### `main.ts => app module => app component`

## - Random Info

- if any changes happens to `angular.json` we should reRun the application
- event `keyup.enter` = on press Enter

<hr/>

### 1 - One way data binding

recieve data from component to template or reverse

- string interpolation ex: `<h1>{{value}}</h1>` => component to template
- event binding ex: click => template to component

### data bind

```javascript
<h1>{{ value }}</h1> // to set dynamic Value
```

### property bind

```javascript
<input type="text" [value] = "obj.name"/>           // to set dynamic Dom property
  =
<input type="text" [attr.value] = "obj.name"/>     // to set dynamic html property
// there are some differences between dom and html properties but in most cases they are the same
```

### event bind

```javascript
show(e){
  console.log(e.target.value)
}
//using circular brackets to bind events & without (on)
<button (click) ="show($event)">save</button>
```

### Reference variable

```javascript
//  = useRef() in React
```

```javascript
<input #rf type="text"/>
<button (click) ="showInput(rf)">save</button>           // onclick ==> show that input holds the rf
```

<hr/>

### 2 - Two way data binding

### ngModel

```javascript
productname =""      // in component

<input type="text" [(ngModel)] ="productname"/>

  & in `app.module.ts`
  import {FormsModule} from @angular/forms ;
  // in imports
  push FormsModule
```

### =

```javascript
productname =""      // in component

changeproduct(value){      // in component
  this.prodcutname = value
}
<input type="text" #qw [value] ="productname"
(keyup)= "changeproduct(qw.value)"/>

```

<hr/>

### \*ngFor structure directive

```javascript
// in component
ages = [10, 20, 30];

//in template
<div *ngFor ="let item of ages;let i=index;let o=odd;let e=even; let f=first; let l =last"

// classes
[class.bg-success] = "condition"
[class.bg-success] = "o"   // odd items will take the class of success
[class.bg-danger] = "e"   // even items will take the class of dan  ger
  =
[ngClass] = "{'className': condition, 'bg-success': o, 'bg-danger': array.length > 5}"
//if that condition is true this item will take that class
// true => o(odd) || e(even) || ...etc

[class]="'bg-success'"          // all items will take this class


//Styles
[ngStyle]= "{'className': condition, 'bg-success': o, 'bg-danger': array.length > 5}"
>
  age = {{item}}
</div>
```

"--------------------------------------------------------------------------------------------------"

### \*ngIf structure directive

`control if the element will be exist in the dom or not`

```javascript
// in component
ages = [10, 20, 30];

//in template
//if true this div will be exist in Dom
<div *ngIf ="ages.lenth > 5"
[ngClass] = "{'className': condition, 'bg-danger': ages.length < 5}"
>
</div>
```

### [ngSwitch]

`control if the element will be exist in the dom or not`

```javascript
// in component
x = 2

//in template
<div [ngSwitch]= "x">
  <span *ngSwitchCase= "1">1 is selected</span>
  <span *ngSwitchCase= "2">2 is selected</span>
  <span *ngSwitchCase= "3">3 is selected</span>
</div>
// so span of 2 is which be exist
```

"--------------------------------------------------------------------------------------------------"

### make your own directive

```typescript
// ng g d directive_name => it'll make a class in directive_name.directive.ts

import { Directive, ElementRef, Input } from "@angular/core";

//inside the class
export class directive_name implements onInit {
  @Input() dcolor: string = "purlpe";
  constructor(public el: ElementRef) {}
  ngOnInit(): void {
    this.el.nativeElement.style.backgroundColor = this.dcolor;
  }
}

//inside the template
<div directive_name dcolor="red">
  {" "}
  // & if i don't use d color it will be purlpe by default
</div>;
```

<hr/>

### Pipe

#### `it's a format for: String || Number || Date`

```typescript
{{ValueName | currency : currencyCode : display : digitInfo : locale}}
{{ValueName | date : format : timezone : locale  }}

//Example
salary = 5000.4568          // in component
title = "KHALED"
ndate = new Date(1997 , 4 , 12)

<p>
  salary {{salary | currency : 'CAD' : 'symbol-narrow' : '4.3-3'}}  // $5,000.456

  {{title | lowercase}}        // khaled       // without any changes on the original value

  {{ndate | date}}          // May, 12 , 1997
  {{ndate | date : 'dd / MM / yyyyy'}}          // 12 / 05 / 1997
  {{ndate | date : 'dd / MMM / yyyyy'}}          // 12 / May / 1997
  {{ndate | date : 'MMM'}}          // May
  {{ndate | date : 'short'}}          // 5 / 12 / 97, 12:00 AM
</p>
```

```javascript
// in the pipe file
// pipe is watching the changes on reference by default
// to make it watch the values  => pure = false
```

<hr/>

## Routing

```typescript
// inside app-routing.module.ts
// suppose we have Home, Contact and About components

const routes: Routes = [
  { path: "home", component: HomeComponent } //if path is starts with home => load HomeComponent
  { path: "contact", component: ContactComponent }
  { path: "about", component: AboutComponent }

  //children
  { path: "about", component: AboutComponent,children: [
  { path: "detais1", component: AboutDetail1sComponent },
  { path: "detais2", component: AboutDetail2sComponent }
  ]}

  { path: "", redirectTo:"home", pathMatch:"full" } // has nothing => load HomeComponent & make path has /home
  { path: "**", component: NotfoundComponent }    // if path is has anything =>  load NotfoundComponent
  // path: "**" must be the last one in the array , because it is just a searhing loop

  { path: "department/details/:id", component: DepartmentDetails }                  // dynamic

  // guard
];
```

```typescript
// inside app-component.html
<router-outlet></router-outlet> // and that's it
```

### Navigation

```javascript

<a routerLink = "/home">home</a>       // adding the attr routerLink to navigate
<a routerLink = "/about">About</a>
<a [routerLink] = "['/contact']">Contact</a>   // or
<a [routerLink] = "['/department/details',item.id]">item</a>   // ====> = `/department/details${item.id}`

<li routerLinkActive="active"><a routerLink = "/home">home</a></li>   // in that path =>this li will have active class


// to navigate
// in constructor (router:Router)
this.router.navigateByUrl("/home")           // go to home component


// to get the id param from current Url
// in constructor (ac:ActivatedRoute)
// in ngOnInit
this.ac.params.subscribe(a=>{this.variableName = a})
```

<hr/>

## Reactive extension for js ==> rxjs

```typescript
// in componentName.serrvice.ts
import { Observable } from 'rxjs';

myfun(){
  return new Observable<number>(a => {
    setTimeout(()=>{
      a.next(10);                  // after 1 second send data to subscribe = 10
    },1000)

    setTimeout(()=>{
      a.next(30);                  // after 5 second send data to subscribe = 30
    },5000)

    setTimeout(()=>{
      a.complete();
    },6000)

    setTimeout(()=>{
      a.error("error");
    },9000)

})
```

```typescript
// in componentName.component.ts
constructor(public hs:serviceClass)

show(){
  this.hs.myfun().subscribe(data => {console.log(data)},                 //10................30
  err => {console.log(err)},
  () => {console.log("complete")}             // excute after complete
  )
}
```

## Form

### `template driven form`

```typescript
// in app.module.ts
import { FormsModule } from "@angular/forms";
// and push it to imports

// in component.html
<form #userform="ngForm" >

</form>
<button (click)="show(userform)"></button>

//in ts
show(userform){
  console.log(userform)
}
```

```typescript
// to make the form has control on input
// inside that form
<input type="text" name="id" ngModel>     //must has name & ngModel to make it form control type

{{userform.value|json}}          // will show the value of the input => inputName:value

<input type="text" name="id" ngModel #sid="ngModel">   // adding classes due to its status
// classed: ng-valid - ng-dirty - ng-touched - ng-invalid -...
{{sid.value}} - {{sid.dirty}} -{{sid.touched}}


//submit
<form (ngSubmit)="save">
<input type="submit" value="add" [disabled]="userform.invalid">
</form>

```

#### `ng2 validation // "library for form validation"`

### `Reactive form`

```typescript
//in app.component.ts
import {ReactiveFormsModule} from '@angular/forms';        // & push it to imports

//in tamplate
<form [formGroup]="stdform" (ngSubmit)="save()">
  <input type"text" name="id" formControlName="id">     // to bind and control
  <input type"text" name="fname" formControlName="fname">
  <input type"text" name="age" formControlName="age">
  <input type"text" name="email" formControlName="email">
</form>

{{stdform.value|json}}        //{"id":initialValue,"fname":initialValue,"age":initialValue,"email":initialValue}
```

```typescript
// in component.ts
import { FormControl, FormGroup } from "@angular/forms";

stdform = new formGroup({
  id: new FormControl(initialValue),
  fname: new FormControl(initialValue),
  age: new FormControl(initialValue),
  email: new FormControl(initialValue),
});

std:Student = new Student();
save(){
  this.std = this.stdform.value;
  console.log(this.std)
}
```
