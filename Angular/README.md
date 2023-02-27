<h1 align="center"> Angular </h1>

### `Client Side Framework - Single Page application`

### commands

```node
npm i -g @angular/cli               to install angular
ng new App_name                     to create a new angular app
ng serve -o                         to run the application
ng g c component_name               to generate a component
ng g class folderName/className     to generate a class
```

### folders & files

- - e2e => for testing
- - src => app place
- main.js => All code
- vendor.js => All libraries and compiler
- style.js => control the styles
- polyfills.js => close the gap between browsers
- runtime.js => from where calling starts

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

## Arrays

### \*ngFor

```javascript
// in component
ages = [10, 20, 30];

//in template
<div *ngFor ="let item of ages">
  age = {{item}}
</div>
```
