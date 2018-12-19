# Angular Interview questions
###  Angular ��������
����� �������� ��� � Angular �������� � �� � ��������� ������ HTML, � � ��������� Shadow DOM, �������� ��������� ����� ���� �������������� �������� (ngIf, ngSwitch...)
� Angular ���� ������ ����� �������� ������:
<details>
<summary><b>[]</b> &nbsp;&mdash; �������� <b>��������</b> �������� HTML � <b>��������</b> Component <b>(������������)</b>
</summary>
 
 ������ �� ������� � ��������

```html
<input type="text" [value]="name" />
``` 

```html
<template [ngIf]="condition">������ ���</template>
``` 
```html
 <div [ngSwitch]="count">
            <ng-template *ngSwitchCase="1">{{count * 10}}</ng-template>
            <ng-template *ngSwitchCase="2">{{count * 100}}</ng-template>
            <ng-template ngSwitchDefault>{{count * 1000}}</ng-template>
        </div>
```

<br>
</details>

<details>
<summary><b>()</b> &nbsp;&mdash; �������� <b>�������</b> �������� HTML � <b>������</b> Component <b>(������������)</b></summary>
<div>
������ �� �������� � ������.<br> 
������ "()" ���������� ����� �������, � Angular ��� ���� ��� �������, ��� ����� ���������.

```html
<button (click)="addItem(text, price)">��������</button>
```  
���������� ���������� � ������� ����� ����� ������ $event 
<br>
```html
<button (click)="increase($event)">Click</button>
``` 

```javascript
increase($event) : void { 
        this.count++;
        console.log($event);
        }
```
<br>
</details>

<details>
<summary>
    <b>[()]</b> &nbsp;&mdash; <b>������������ </b> �������� <b>��������</b> �������� HTML � <b>��������</b> Component
</summary>
<div>
��������� � ���� ��� ����������, ������� � ��� �������.<br>
[(ngModel)]= � <b>�������</b> ��������� �� ����� ��������� �� ��������.<br>
������ <b>[()]</b> ���������� ����� � �����, ��� ����� ��������� ��������� (������ �������� ���� � �����).

```html

<input [(ngModel)]="name" placeholder="name">

<dx-load-indicator [(visible)]="loading" class="loading"></dx-load-indicator>

<dx-popup #popup title="Create Project" [(visible)]="popupVisible">Hi!</dx-popup>
```  

<br>
</details>

<details>
<summary>
    <b>{{}}</b> &nbsp;&mdash; <b>������������ �����</b>,  ��� ���������� <b>�����</b> �� ������� Component <b>��������� �����</b> ���  <b>����������</b>  HTML <b>(�����������)</b>
</summary>
<div>

```html
<h3>
  {{title}}
  <img src="{{titleImageUrl}}" style="height:30px">
</h3> 
<a href="img/{{username}}.jpg">Hello {{username}}!</a>
```  

 ���������, ������ ������� �������� ������ �� ����� ��������� ����� ������, ������� ����� �������������� � ��������������� ��������� typescript. <br>
ex: {{name}} , {{'name'}} ����� �������.  <br>
������ ����� �� ��������� ������� &nbsp;&mdash; �� ��'� ���������� ����������. <br>
�������, ����� �� ��������� ������� &nbsp;&mdash; �� �����, ���� Angular �������� ������, � ���� ���������� �� �����: 

```html
<p>The sum of 1 + 1 is not {{1 + 1 + getVal()}}</p>
```  


<br>
</details>


### Angular ��������� �����������, ������������, ����������
#### ����������� ��������� ngIf, ngFor, ngSwitch
�������� ��������� DOM � ������� ����������, ��������� ��� �������� ��������� hmtl.

<details>
<summary>
    <b>*ngIf</b> &nbsp;&mdash; ��������� ������� ���, ��������, ���������� ������� ��� ������������ �������
</summary>

```html
<p *ngIf="condition">������ ���</p>
<p *ngIf="!condition">���� ���</p>
<button (click)="toggle()">Toggle</button>
``` 

<br>
</details>

<details>
<summary>
    <b>ng-template</b> &nbsp;&mdash; ��������� �������� �������������� ���������
</summary>

 ������� � ������ Angular 4.0 ��������� ngIf ����������� ������ �������������. � ���������, �� ����� �������� �������������� ��������� � ������� ��������� ng-template. ���, ���������� ������ ����� ���������� ����������:

```html
<p *ngIf="condition;else unset"> ������ ��� </p>
<ng-template #unset><p>���� ���</p></ng-template>
<button (click)="toggle()">Toggle</button>
``` 

���� ����� ���������� ����� ���������� ������:

```html
<div *ngIf="condition; then thenBlock else elseBlock"></div>
<ng-template #thenBlock>Then template</ng-template>
<ng-template #elseBlock>Else template</ng-template>
<button (click)="toggle()">Toggle</button>
```

<br>
</details>


<details>
<summary>
    <b>*ngFor</b> &nbsp;&mdash; ��������� � �������� �������� �������
</summary>

```html
<ul>
    <li *ngFor="let item of items; let i = index">{{i+1}}.{{item}}</li>
</ul>
``` 

```javascript
items =["Apple iPhone 7", "Huawei Mate 9", "Samsung Galaxy S7", "Motorola Moto Z"];
``` 

<br>
</details>

<details>
<summary>
   <b>������ ���������</b> <b>'*'</b> &nbsp;&mdash; �������������� �����
</summary>
����� ��������, ��� ��� ������������� �������� ngFor � ngIf ����� ���� �������� ������ ���������. �� ����� ��� �� ����� ��� �������������� �����, ������� �������� ���������� ���������.

```html
<p *ngIf="condition">������ ���</p>
<ul>
    <li *ngFor="let item of items">{{item}}</li>
</ul>
``` 
�� ����� ����� ������������ ��������� ���:


```html
<template [ngIf]="condition">
    <p>������ ���</p>
</template>

<ul>
    <template ngFor let-item [ngForOf]="items">
        <li>{{item}}</li>
    </template>
</ul>
``` 


<br>
</details>

 <details>
<summary>
    <b>*ngSwitch</b> &nbsp;&mdash;  �������� � ������ ����������� switch..case � � ����������� �� �� ���������� ���������� �������� ��� ��� ���� ����.
</summary>

```html
<div [ngSwitch]="count">
            <ng-template *ngSwitchCase="1">{{count * 10}}</ng-template>
            <ng-template *ngSwitchCase="2">{{count * 100}}</ng-template>
            <ng-template ngSwitchDefault>{{count * 1000}}</ng-template>
</div>
``` 

<br>
</details>

#### ������������ ��������� ngModel, ngClass, ngStyle 
�������� ��������� ��� ������������� ��������

 
<details>
    <summary>
        <b>ngModel</b> &nbsp;&mdash; ������� ����������� ����'���� ����� ��� ������� �� ������ �����
 </summary>

 ������� ��������� ����� FormControl � ������� ���������� ������ � ����������� ��� ������ � ���������� �������� �����. <br>
  ������ FormControl ����������� �������� ������, � ����� �������� �� ��������� ����� �������� � �������������� � �������������.
- [angular.io/api/forms/FormControl](https://angular.io/api/forms/FormControl)

���� ��� ���� ������ ������� �������� ������ � ���� �����, <br>�� ����� ������������ � ���������������� ��������� **[...]** 

```html
<input name="title" [ngModel]="title" />
```
���� ��� ���� ����������� ��������� ��������� ������, <br>�� �� ����� ������������ ��������������� �������� **[(...)]** 

```html
<input name="title" [(ngModel)]="title" />
``` 

<br>
</details>

<details>
    <summary>
        <b>ngClass</b> &nbsp;&mdash; ����������� ��������� �������� �������� ���� "�� �������" 
    </summary>

������ �������� � DOM ����� ���������� ����� ������. <br>
������� ��������� ngClass:

```html
<some-element [ngClass]="'first second'">...</some-element>
<some-element [ngClass]="['first', 'second']">...</some-element>
<some-element [ngClass]="{'first': true, 'second': true, 'third': false}">...</some-element>
<some-element [ngClass]="stringExp|arrayExp|objExp">...</some-element>
<some-element [ngClass]="{'class1 class2 class3' : true}">...</some-element>
``` 

�� ����� ���������� ������, ������� �����, Set � ��������� ��������. ��� ���������� ������ ��������� ��������. ������ � ������� ����� ��������� ������������� ������, �� �� ������� ��, ��� ��� ��� ����������� ��� �������:

```html
<p [ngClass]="{segoePrintFont:condition}">Angular</p>
``` 
```html
<div [ngClass]="{
  'is-active': condition,
  'is-inactive': !condition,
  'is-focused': condition && anotherCondition,
}">
</div>
``` 
<br>
</details>

<details>
    <summary>
        <b>ngStyle</b> &nbsp;&mdash; ������ ����� ������ � ��������
    </summary>

������� ��������� ngStyle:

```html
<some [ngStyle]="{'font-style': styleExp}">...</some>
<some [ngStyle]="{'max-width.px': widthExp}">...</some>
<some [ngStyle]="objExp">...</some>

<div [style.display]="visibility==true?'block':'none'">
<p [style.fontSize]="'14px'" [style.fontFamily]="'Verdana'">Angular</p>
```

<br>
</details>
<hr>



<details>
    <summary>
        E��� �� ����� �������� � �� �������� ������ ��������?
    </summary>

<b>ngIf</b> ����������  

```html
<p *ngIf="condition">������ ���</p>
<p *ngIf="!condition">���� ���</p>
<button (click)="toggle()">Toggle</button>
```
 
<br>
</details>


<details>
    <summary>
        ����� ������ ����� �� ����� ��������, ��� �� ����������?
    </summary>


 <b>*ngFor</b> ����������  

```html
<ul>
    <li *ngFor="let item of items; let i = index">{{i+1}}.{{item}}</li>
</ul>
``` 
```javascript
items =["Apple iPhone 7", "Huawei Mate 9", "Samsung Galaxy S7", "Motorola Moto Z"];
``` 
<br>
</details>

<details>
    <summary>
         ���� ����� �������� *ngIf ��� *ngFor, �� �� �������� � �������� ����� div?
    </summary>

 <b>ng-content</b> ���������� 

```html
<ng-container *ngFor="let item of items; let i = index; trackBy: trackByFn">
  <li>...</li>
</ng-container>
``` 
����� ������������ <b>template</b>, ������ �� ������� ����������� ����������.
 <br/> (��.  " <b>������ ���������</b> <b>'*'</b> " )
<br/> ��������
```html
<li *ngFor="let item of items; let i = index; trackBy: trackByFn">...</li>
``` 

������

```html
<template ngFor let-item [ngForOf]="items" let-i="index" [ngForTrackBy]="trackByFn">
  <li>...</li>
</template>
```
 
<br>
</details>



<details>
    <summary>
        ��������� ����� �������� css ���� ������ �����
    </summary>


 <b>*ngFor</b> ����������  


```javascript
@Component({
   selector: 'body',
   template: 'app-element',
   // prefer decorators (see below)
   // host:     {'[class.someClass]':'someField'}
})
export class App implements OnInit {
  constructor(private cdRef:ChangeDetectorRef) {}

  someField: boolean = false;
  // alternatively also the host parameter in the @Component()` decorator can be used
  @HostBinding('class.someClass') someField: boolean = false;

  ngOnInit() {
    this.someField = true; // set class `someClass` on `<body>`
    //this.cdRef.detectChanges(); 
  }
}
``` 

```css
:host(.someClass) {
 background-color: red;
}
``` 
<br>
</details>





<hr/>

## ������� �� ������������� �� Angular  [![Angular-RU](https://img.shields.io/badge/Telegram_chat:-Angular_RU-216bc1.svg?style=flat)](https://t.me/angular_ru)

������� ������������ ��������������� ��� ����, ����� ���������� ������� ������������, ��������� �������, ������������ ��� ������ �� ����� Angular. ������� ��� ������������� �� ������ JavaScript ��� Web-����� ������ �������� � ������ ������, ������� ���� ����� �������� ������ �������� �� ���� ����:

**Fundamentals**:

- [Coding Interview University](https://github.com/jwasham/coding-interview-university)
- [Awesome Interviews](https://github.com/alex/what-happens-when)

**Frontend**: 

- [Front-end Job Interview Questions](https://github.com/h5bp/Front-end-Developer-Interview-Questions)
- [The Best Frontend JavaScript Interview Questions](https://performancejs.com/post/hde6d32/The-Best-Frontend-JavaScript-Interview-Questions-(Written-by-a-Frontend-Engineer))
- [Frontend Guidelines Questionnaire](https://github.com/bradfrost/frontend-guidelines-questionnaire)
- [���������� � �������� �� Front-end ������������](https://proglib.io/p/frontend-interview/)

**Angular**:

- [Angular Interview Questions by Google Developer Expert](https://github.com/Yonet/Angular-Interview-Questions)

##### �������� ���������

<details>
<summary>��� ����� Angular?</summary>
<div><br>
<img src="https://d2eip9sf3oo6c2.cloudfront.net/series/square_covers/000/000/033/thumb/egghead-angular-material-course-sq.png" align="left"><p><b>Angular</b>&nbsp;&mdash; ��� ��������� ��� ���������� ��������� �&nbsp;���������� ���-����������. ���� ���������� ������ ������������ ��&nbsp;���� &laquo;������� ������&raquo;, ��� ���������� ������������ �&nbsp;����� ������ ���������� ��&nbsp;������� ��������. ��� ������ ������� ������ ������� �������� ������, ���� ��������� ������������� �&nbsp;���������� �����������. �&nbsp;Angular ��&nbsp;��������� ��������� ���������� ������������, �&nbsp;�&nbsp;TypeScript �������� ��������� ������ ������, ��������� ����������� ���������. �&nbsp;Angular ������������ �������� ���������� ������������ ��&nbsp;�������. ��� ����� ���� ������������ �&nbsp;������ �&nbsp;�����, �&nbsp;����������� ��&nbsp;����, ��� ��� ����������.</p>
<hr>
  
<b>����� ����� ����� ��������</b>:
<ul>
  <li>��������� Google, Microsoft</li>
  <li>����������� ������������ (CLI)</li>
  <li>Typescript �� �������</li>
  <li>���������� ���������������� � RxJS</li>
  <li>������������ ��������� � Dependency Injection �� �������</li>
  <li>�������, ���������� �� ���������� HTML</li>
  <li>��������������� Shadow DOM �� ������� (���� ��� ��������) </li>
  <li>��������������� ��������� HTTP, WebSockets, Service Workers</li>
  <li>�� ����� ������ ������������� �����������. ������ ������� �������. jQuery ������� � D3 ����� ������������ �� ������</li>
  <li>����� ����������� ���������, ��� AngularJS (�� ������ React, Vue)</li>
  <li>������� ���������</li>
</ul>

<b>������</b>:

<ul>
  <li>���� ����� ��������� ��-�� Observable (RxJS) � Dependency Injeciton</li>
  <li>����� ��� �������� ������ � ������ ����� ������� ����� �� �������������� ����������� 
    (�� �� ����� �������, �� ���������, �� ������� AngularJS �� ����� ���)</li>
  <li>���� �� ���������� ������������� ������� enterprise-����������, �� � ���� ������, � ��� ��� ����������� �� ������� - ����� ��������� Mobx, Redux, MVVM, CQRS/CQS ��� ������ state-��������, ����� ����� �� ������� ���� ����</li>
  <li>Angular-Univesal ����� ����� ��������� ������</li>
  <li>������������ �������� ����������� ����������� ������������� �������</li>
</ul>

</div>
</details>

<details>
<summary>� ��� ������� ����� AngularJS � Angular?</summary>
<div>
  
<br><b>AngularJS</b> �������� �����������, ������� ����� ������ ��� � ���������� Single Page Application. �� �������� � 2009 ���� � � ������ ����������, ��� ���� ����� �������. <b>Angular</b> (Angular 2+) �� � ���� ������� ��������� �� ���� �����, �� ���� ������ ����������� �� ��������� � AngularJS 1.x, ������� ������ ������������������, ������� ��������, ����� ������� API, ����� ������ �������.

<b>��� ��������� � Angular</b>: <br>

<ul>
  <li>Angular ������������ �� ��������� ��������� � ����� ������ ������������������</li>  
  <li>Angular ����� ���������� ������� ��� ��������� �������������������</li>
  <li>AngularJS ����� ���������, ��� Angular</li>
  <li>AngularJS ���������� ����������� � $scope</li>
  <li>Angular ����� ����� �������� ����������� ��������� ����������</li>
  <li>� Angular ����� ��������� ����������� �������� (camelCase)</li>
  <li>Angular �������� �������� � �������� � ��������� DOM ���������</li>
  <li>������������� ���������� ������ ����� [property]</li>
  <li>������������ ���������� ������ ����� [(property)]</li>
  <li>����� �������� DI, ��������, ������� ����������</li>
</ul>

<b>�������� ������������ Angular</b>: <br>

<ul>
  <li>�������� ������������� Angular 2, 4, 5, ..</li>
  <li>TypeScript � ���������� ��������� �����</li>
  <li>���������� ���������� � �������� JIT � AOT (+ c��������� ����)</li>
  <li>���������� ��������</li>
</ul>

</div>
</details>

<details>
<summary>����� ������ ���� ��������� ��������� ����������� ������ Angular ���������� � ������?</summary>
<div>
  in progress..
</div>
</details>


<details>
<summary>��� ����� MVVM � � ��� ������� ����� MVC?</summary>
<div>
  in progress..
</div>
</details>

<br> 

 

##### Angular Template ���������

<details>
<summary>��� ����� ������������ � Angular?</summary>
<div><br>
  
�������� ������������ � ����������� ����������� ������������ � Angular ��� ���������� ������ ��������� ����� � �������� ����������. ��������:
  
  ```html
    <a href="img/{{username}}.jpg">Hello {{username}}!</a>
  ```

  
<br>
</div>

</details>


<details>
<summary>����� ������� ������������� �������� � Angular �� ������?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>� ��� ������� ����� ����������� � ���������� ����������, �������� ���������� ���������?</summary>
<div>
  in progress..
����������� ��������� ngIf, ngFor, ngSwitch
�������� ��������� DOM � ������� ����������, ��������� ��� �������� ��������� hmtl. 
<br/>
������������ ��������� ngModel, ngClass, ngStyle 
�������� ��������� ��� ������������� ��������
</div>
</details>



<details>
<summary>��� ���� ����� ��������� ng-template, ng-container, ng-content?</summary>
<div>
  <h4>1. ng-template</h4>
  
  `<template>` � ��� �������� ��� ����������� ������� ����������� ��������, ������� �� ������������ �� ����� ��������, �� ����� ���� ��������������� ��� ������ JavaScript. <br><br>
  Template ����� ����������� ���� ��� �������� ��������, ���������� ��� ������������ ������������� � ���������. ���� ������ � ������������ ���������� �������� `template` �� ����� �������� ��������, �� ������ ��� ������ ����� ��������� � ���������� �����������; ���� ���������� ��� ���� �� ������������. <br><br>
  
  `<ng-template>` - �������� �������������� ������������ �������� template, ������ ������� �������� � ��������� ������ Angular, ��� ���� ������� � ����� ������ ������������� �� ������������� �� �������� template ����������, ������� ����� ������� � ������ ����� ����������� �� ��� ��� ���� ��������. <br><br>

������:

```html
<div class="lessons-list" *ngIf="lessons else loading">
  ... 
</div>

<ng-template #loading>
    <div>Loading...</div>
</ng-template>
```

  <h4>2. ng-container</h4>
  
  `<ng-container>` - ��� ���������� ���������, ������� ����� �������������� ��� ����������� �����, �� �� ������������ � ������ DOM ��� ���� (node).

  �� ����� ���� ����������� ��������� (*ngIf, *ngFor, ..) �������� �������������� ������� ��� ����� ��������. � ����������, ������ ������� ���������������� � ����� �����������:
  
```html
<ng-template [ngIf]="lessons" [ngIfElse]="loading">
   <div class="lessons-list">
     ... 
   </div>
</div>

<ng-template #loading>
    <div>Loading...</div>
</ng-template>
```

�� ��� ������, ���� � ���� ��������� ��������� ����������� ��������?
(�������: � ���������, ��� ������ �������)

```html
<div class="lesson" *ngIf="lessons" *ngFor="let lesson of lessons">
  <div class="lesson-detail">
      {{lesson | json}}
  </div>
</div> 
```

```
Uncaught Error: Template parse errors:
Can't have multiple template bindings on one element. Use only one attribute 
named 'template' or prefixed with *
```

�� ����� ������� ���:

```html
<div *ngIf="lessons">
  <div class="lesson" *ngFor="let lesson of lessons">
    <div class="lesson-detail">
        {{lesson | json}}
    </div>
  </div> 
</div>
```

������, ����� �������� ������������� ��������� �������������� div, �� ����� ������ ����� ������������ ��������� ng-container:

```html
<ng-container *ngIf="lessons">
    <div class="lesson" *ngFor="let lesson of lessons">
        <div class="lesson-detail">
            {{lesson | json}}
        </div>
    </div>
</ng-container>
```

��� �� �����, ��������� ng-container ������������� ��� �������, � ������� �� ����� ������������ ����������� ���������, ��� ������������� ��������� �������������� �������.

��� ���� �������������� ��������, ���� ��� �� �� ������ ������������ ng-template ������ ng-container, �� ������������ �������� �� �� ������� ������������ ������ ����������� ����������� ��������.

�� ������ ������ ���� ���:

```html
<div class="mainwrap">
    <ng-container *ngIf="true">
        <h2>Title</h2>
        <div>Content</div>
    </ng-container>
</div>
```

���� ���:

```html
<div class="mainwrap">
    <ng-template [ngIf]="true">
        <h2>Title</h2>
        <div>Content</div>
    </ng-template>
</div>
```

�� ������, ��� ���������� ����� ���� � ����:

```html
<div class="mainwrap">
      <h2>Title</h2>
      <div>Content</div>
</div>
```

 <h4>3. ng-content</h4>
 
 `<ng-content>` - ��������� �������� ������������ ����������� html-��� � �������� ����������.
 
����� �� ����� ����, ������� ������� ��� ��� � ng-template, ng-container. ��� ��� ng-content ������ ������ ������������� �������� � ���� ���-����������. ���-���������� ������� �� ���������� ��������� ����������. �� ������ ������ � ���-����������� ��� � ���������������� �������� ����������������� ����������, ������� ��������� � ������� �������� ���-����������. ��� �������� ������ �������� � ������� �� ��������� �� ������� �����������, ����� ��� jQuery ��� Dojo. ������������ ���-��������� ����� ���� ����������� ��� ��������� ����, ������ ����� ������� ��������� �� HTML-��������. ���-���������� ���������� ����� ��� ��������������� ����������� ����������� ��������.

������� ���������� �������� �� ���������, ��� ����� ����������������� ��� ���������. �� ����� ������� ���, ����� �� ���� � ��������� �� ����� �������� �����-���� ��������� ������. ��� ����� ������� ����������� ���������. 

comment.component.ts:

```ts
@Component({
  selector: 'comment',
  template: `
    <h1>�����������: </h1>
    <p>{{data}}</p>
  `
})
export class CommentComponent {
  @Input() data: string = null;
}
```

app.component.html

```html
<div *ngFor="let message of comments">
  <comment [data]="message"></comment>
</div>
```

�� ����� ��������� � ������ �����. <br>
comment.component.ts:

```ts
@Component({
  selector: 'comment',
  template: `
    <h1>�����������: </h1>
    <ng-content></ng-content>
  `
})
export class CommentComponent { 
}
```

app.component.html

```html
<div *ngFor="let message of comments">
  <comment>
    <p>{{message}}</p>
  </comment>
</div>
```

�������, ��� ������� ����� ������������� ��������� �����, ���� ����� � ������. �� ������ ������ ������������� ������ ��� ������, ����� �� ��������� ������������ ������������ � ����� ������������ ������� ������ ����� ����������� (������ ���-�����������).

</div>
</details>

##### Angular development enviroments

<details>
<summary>��� ����� ��������� � ��� ������� �����������?</summary>
<div>
  in progress..
</div>
</details>


<details>
<summary>��� ����� ���������, ���������, ������, ������, ���� � Angular � ��� ���� ��� �����?</summary>
<div>
  in progress..
</div>
</details>


<details>
<summary>���������� �� �������� ���������� @NgModule, @Component, @Directive, @Injectable, @Pipe</summary>
<div>
  in progress..
</div>
</details>


<details>
<summary>��� ����� ������������ ���������� � ��� �� ����� ������������ � Angular?</summary>
<div>
  in progress..
</div>
</details>


<details>
<summary>��� ��������� �������� � �����������?</summary>
<div>
  in progress..
</div>
</details>


##### Angular render lifecycle and core environments

<details>
<summary>��������� �������� �������� (bootstrap) Angular-���������� � ��������?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>��� ���������� �������������� ����������� � Angular (������� components view)?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>����� ��������� ���� � �����������?</summary>
<div>
  in progress..
</div>
</details>


<details>
<summary>��� ����� Shadow DOM � ��� � ��� �������� � Angular?</summary>
<div>
  in progress..
</div>
</details>


<details>
<summary>��� ����� Data Binding � ����� �������� ��������� � ��� �� ������?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>��� �� ����������� ������������� � ������������� �������� ������?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>� ��� ������������ � ���������� Regular DOM (Angular) ����� Virtual DOM (React)?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>��� ����� ngZone?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>��� ��������� �������������, ���� ���� ������ ������ ����������� ��� '����'?</summary>
<br>

1. ��������� ����� `ApplicationRef.prototype.tick`, ������� �������� `change detection` �� ���� ������ �����������.

```typescript
import { Component, ApplicationRef, NgZone } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <h1>Hello, {{ name }}!</h1>
    `
})
export class AppComponent {

    public name: string = null;

    constructor(private app: ApplicationRef, private zone: NgZone) {
        this.zone.runOutsideAngular(() => {
            setTimeout(() => {
                this.name = window.prompt('What is your name?', 'Jake');
                this.app.tick();
            }, 5000);
        });
    }
    
}
```

2. ��������� ����� `NgZone.prototype.run`, ������� ����� �������� `change detection` �� ���� ������.

```typescript
import { Component, NgZone } from '@angular/core';
import { SomeService } from './some.service'

@Component({
    selector: 'app-root',
    template: `
        <h1>Hello, {{ name }}!</h1>
    `,
    providers: [SomeService]
})
export class AppComponent {

   public name: string = null;

   constructor(private zone: NgZone, private service: SomeService) {
       this.zone.runOutsideAngular(() => {
           this.service.getName().then((name: string) => {
               this.zone.run(() => this.name = name);
           });
       });
   }
   
}
```

����� `run` ��� ������� ��� �������� `tick`, � ���������� ��������� �������, ������� ����� ��������� ����� `tick`. �� ����:

```typescript
this.zone.run(() => this.name = name);

// ���������

this.name = name;
this.app.tick();
```

3. ��������� ����� `ChangeDetectorRef.prototype.detectChanges`, ������� �������� `change detection` �� ������� ���������� � ��������.

```typescript
import { Component, NgZone, ChangeDetectorRef } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <h1>Hello, {{ name }}!</h1>
    `
})
export class AppComponent {

   public name: string = null;

   constructor(private zone: NgZone, private ref: ChangeDetectorRef) {
       this.zone.runOutsideAngular(() => {
           this.name = window.prompt('What is your name?', 'Jake');
           this.ref.detectChanges();
       });
   }
   
}
```
</details>


<details>
<summary>��� ����� EventEmmiter � ��� ������������� �� �������?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>��� ����� Change Detection, ��� �������� Change Detection Mechanism?</summary>

<h4>1. Change Detection</h4>
  
Change Detection - ������� ������������� ������ � ��������������. � Angular ����� ���������� ����������������, ���� ��� ������������� `ngModel` ��� ���������� ������������� ����������, ������� �������� �������������� ������� ������ ����������������� ������.

<h4>2. Change Detection Mechanism </h4>

Change Detection Mechanism - ������������ ������ ������ � ������� �� ������������ �����, ������� � ��������� (���) ���������� �� ����������. � ���� � ���� ����� �������������� ������ ������. ����������� Angular ���������� ����� ������ � ������ �����������. ������ ��������� ��������� �� ��������, �� �������� �� ��������� �� ������������. ������������� ����� ��������� ������������� `$digest` �����. 

<br>
</details>

<details>
<summary>����� ���������� ��������� ����������� ���������?</summary>
<br>

����� ���� ��� ��������� - `Default` � `OnPush`. ���� ��� ���������� ���������� ������ ���������, �� `Zone` ��������� ��� ������ ���������� �� ����, ��� ��������� ���������. ����� �������� Angular, ��� �� ����� ��������� ������� ��������� ������������������ ����� ������������ ��������� ����������� ��������� `OnPush`. ��� ������� Angular, ��� ��� ��������� ������� ������ �� ������� ������ � ����� ������, ������� ���������� ��� ������ ��������� immutable. ��� ��� ��������� �� �������� �������� ����, ��� ������� ��������� ������� ������ �� ������� ��������. 

<br>

</details>

<details>
<summary>������� Change Detector'�� ����� ���� �� ���� ����������?</summary>
� ������� ���������� ���� ���� Change Detector, ��� Change Detector'� ����������� �� AbstractChangeDetector.
  
<br>
</details>

<details>
<summary>�������� ������� constructor �� ngOnInit?</summary>
<br>
  
����������� ��� �� ���� �������� ����� ������ ������, � �� Angular. �������� ������� � ���, ��� Angular �������� `ngOnInit`, ����� ����, ��� �������� ��������� ����������, �� ����, ��� ������, ��������� �������� �������� `@Input()` � ������ ���������, � ������������ �������� �������� � `ngOnInit`, �� �� ���������� ������ ������������, �� �������.

<br>
</details>

##### Angular data flow

<details>
<summary>��� ����� Dependency Injection?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>��� ����� Singleton Service � � ����� ����� ��� ���������� � Angular?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>��� ����� ���������� ���� ���������� ErrorHandler, Logging, Cache � Angular?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>��� ����� Observable?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>� ��� ������� ����� Observable � Promise?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>� ��� ������� ����� Observable � BehaviorSubject/Subject?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>� ��� ������� ����� switchMap, mergeMap, concatMap?</summary>
<div>
  in progress..
</div>
</details>



##### Angular with Backend integrations

<details>
<summary>������ ��������� ����� ����������������� API �������, ��� ��������� ��� ������������� ��������?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>��� ����� HTTP Interceptors?</summary>
<br>

Interceptor (�����������) - ������ ����������� ����� ��� �������, ������� �������� ������� / ������ �� ����, ��� ��� ����� ���������� / ���������� �� ������. ����� ������������ ������������, ���� ����� ����� �������������� ������������ ������ ���� �������� ����� ��������. �������� ����� ��� ���� �������� ������������� ����� ����������� `Bearer`:

 token.interceptor.ts
 
```typescript
import { Injectable } from '@angular/core';
import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent } from '@angular/common/http';
import { Observable } from 'rxjs/Observable';

@Injectable()
export class TokenInterceptor implements HttpInterceptor {

    public intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
        const token = localStorage.getItem('token') as string;

        if (token) {
            req = req.clone({
                setHeaders: {
                    'Authorization': `Bearer ${token}`
                }
            });
        }

        return next.handle(req);
    }
}
```

� ������������ ����������� ��� �������� � ����������� ������:

app.module.ts

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { HTTP_INTERCEPTORS } from '@angular/common/http';
import { AppComponent } from './app.component';
import { TokenInterceptor } from './token.interceptor';

@NgModule({
    imports: [
        BrowserModule
    ],
    declarations: [
        AppComponent
    ],
    bootstrap: [AppComponent],
    providers: [{
        provide: HTTP_INTERCEPTORS,
        useClass: TokenInterceptor,
        multi: true // <--- ����� ���� ��������������� ������ �������������
    }]
})
export class AppModule {}
```
<br>

</details>


<details>
<summary>��� ������������ Json Web Tokens ��� �������������� ��� ���������� �� Angular?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>��� �������������� ����� XSS � CSRF � Angular?</summary>
<div>
  in progress..
</div>
</details>

##### Angular routing

<details>
<summary>��� ����� ������� � ��� ��� ������� � Angular?</summary>
<div>
  in progress..
</div>
</details>


<details>
<summary>����� ��������� ���� � Angular Router?</summary>
<div>
  in progress..
</div>
</details>


<details>
<summary>��� ����� ������� �������� (Lazy-loading) � ��� ���� ��� ������������?</summary>
<div>
  in progress..
</div>
</details>


<details>
<summary>� ��� ������� ����� Routing � Navigation?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>��� ��������� ������ �� ���� ��� ������������ ����?</summary>
<div>
  in progress..
</div>
</details>


##### Angular Forms (also big ui enterprise)

<details>
<summary>��� ����� FormGroup � FormControl � ��� ���� ��� ������������?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>��� ����� ���������� ����� � Angular?</summary>
<div>
  in progress..
</div>
</details>


<details>
<summary>��� ��������� ��������� ��� ������� � ������� ����?</summary>
<div>
  in progress..
</div>
</details>


##### Build environments

<details>
<summary>� ��� ������� ����� Angular CLI � Webpack Development Environment?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>��� ����� JIT � AOT, � ��� �� ������� � ������ ����� ����������?</summary>
<div>
  in progress..
</div>
</details>

##### Test development

<details>
<summary>��� ����� Unit-������������, ��������������, e2e-������������ (End-to-End) � ��� ��� ����������� � Angular?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>��� ����� Karma, Jest, Jasmine (����� �� ���������� ��������� ��� ���������� �� Angular)?</summary>
<div>
  in progress..
</div>
</details>

<details>
<summary>��� �������������� ������� ��������� � ����������� ������� �����������?</summary>
<div>
  in progress..
</div>
</details>

