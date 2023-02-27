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

  #### 1 - One way data binding

  recieve data from component to template or reverse

      - string interpolation ex: <h1>{{value}}</h1>   =>  component to template
      - event binding ex: click    => template to component

  #### 2 - Two way data binding

### starting

### `main.ts => app module => app component`

<hr/>

### data bind

```javascript
<h1>{{ value }}</h1> // to set dynamic property
```

### property bind

    ```javascript
      <input type="text" [value] = "obj.name"/>     // to set dynamic property
    ```
