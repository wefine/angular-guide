# Codedamn-Tut

Followed codedamn angular 4 tutorial.

## 01. get start
```bash
ng new codedamn-tut
cd codedamn-tut
ng set --global packageManager=yarn
yarn install
```

## 02. add header and directive

Add a component
```bash
ng g component header
```

add a directive
```bash
ng g directive blue-color
```

modify `blue-color.directive.ts`:
```typescript
import {Directive, ElementRef} from '@angular/core';

@Directive({
  selector: '[blueColored]'
})
export class BlueColorDirective {

  constructor(element: ElementRef) {
    element.nativeElement.style.color = "blue";
  }

}
```

modify `app.component.html` to add header.
```html
<div style="text-align:center">
  <app-header></app-header>
</div>
```

modify `header.component.html`:
```html
<p blueColored>
  header works!
</p>

```

## 03. HostListener

```typescript
import {Directive, ElementRef, HostListener} from '@angular/core';

@Directive({
  selector: '[blueColored]'
})
export class BlueColorDirective {

  constructor(element: ElementRef) {
    element.nativeElement.style.color = "blue";
  }

  @HostListener("mouseover")
  mouseover() {
    console.log("mouseover")
  }

  @HostListener("document:click", ['$event'])
  click(event) {
    console.log("clicked ", event)
  }
}

```

## 04. ngif

### ng-template
```html
<button (click)="toggleDiv()">hide|show</button>

<div *ngIf="visible; then odd else even">
  Div Show
</div>

<ng-template #odd>Odd number of click!</ng-template>
<ng-template #even>Even number of click!</ng-template>

```
当`ngif`使用了`ng-template`后，`ngif`所在元素所包含的全部内容均无意义了。

### local variable
```html
<div *ngIf="language.frontend; let frontendLanguages " >
  {{ frontendLanguages.join(",") }}
</div>

``` 

## 05. ngFor
ngFor有几个内置的变量，如index, first, last, odd, even等关于序号的变量。

```html

<ul *ngFor="let item of language.frontend; let even = even; let first=first;">
  <li>{{ item }}</li>
  <li *ngIf="first">{{ item }}</li>
  <li *ngIf="even">{{ item }}</li>
</ul>

```

## 06. data bind
### common
单向数据绑定，即组件中的属性数据绑定到页面中展示。

```html
<div>
  <li>result = {{ result }}</li>
  <li>1 + 1 = <input type="text" value="{{ result }}"></li>
  <li>1 + 1 = <input type="text" [value]="result"></li>
  <li>1 + 1 = <input type="text" [value]="result" (keyup)="changeResult($event)"></li>
  <li>1 + 1 = <input type="text" bind-value=" result " on-keyup="changeResult($event)"></li>
</div>

```
### ngModel
使用`[(ngModel)]`来简化数据双向绑定。首先在`AppModule`中引入：
```typescript
import { NgModule } from '@angular/core';

import { FormsModule } from '@angular/forms';

@NgModule({
  declarations: [
  ],
  imports: [
    FormsModule
  ],
  providers: [],
  bootstrap: []
})
export class AppModule {
}

```
具体使用方式：
```html
  <li>1 + 1 = <input type="text" [(ngModel)]="result"></li>

```
## 07. router 路由
### 基本配置
在`AppModule`头中引入 `RouterModule, Routes`；定义路由对象； 配置`RouterModule.forRoot(appRoutes)`。
```typescript

import { RouterModule, Routes } from '@angular/router';

const appRoutes: Routes = [
  {path: 'home', component: HomeComponent},
  {path: 'header', component: HeaderComponent},
  {path: '', redirectTo: '/header', pathMatch: 'full'},
  {path: '**', component: PageNotFoundComponent}
];

@NgModule({
  imports: [
    RouterModule.forRoot(
      appRoutes,
      {enableTracing: true} // <-- 仅用于调试
    )
  ]
})
export class AppModule {
}

```
### 简单使用
使用 `router-outlet` 来使路由在指定位置显示。
```html
<router-outlet></router-outlet>
```

### 跳转链接与激活状态

```html
<div>
  <a routerLink="/home" routerLinkActive="active" [routerLinkActiveOptions]="{exact:true}">Home</a>
  <a routerLink="/header" routerLinkActive="active">Header</a>
</div>
```
## 08. ngif
## 09. ngif
## 10. ngif
