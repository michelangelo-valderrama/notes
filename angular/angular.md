
**Interpolation binding syntax:**
```html
<h1>{{ title }}</h1>
```
```ts
title = 'Tour of Heroes'
```

**Event binding:**
```html
<button type="button" (click)="fn()"></button>
```
```ts
fn() {
    return 'value...'
}
```

**Property binding:**
```html
<app-my-component [property]="myProperty"></app-my-component>
```
```ts
myProperty = "property..."
```