### 一、angular
####   &ensp;1.angular常用命令
#####  &ensp;&ensp;安装脚手架 npm i -g  @angular/cli
#####  &ensp;&ensp;创建新项目 ng new project-name
#####  &ensp;&ensp;运行新项目 ng serve
#####  &ensp;&ensp;创建新组件 ng g component component-name or dirname/component-name
#####  &ensp;&ensp;创建新服务 ng g service service-name or dirname/service-name
<!--### 二、angular常用指令-->
####   &ensp;2.angular常用指令
#####  &ensp;&ensp;*ngIf if条件的渲染
#####  &ensp;&ensp;*ngFor 循环数据渲染
`<li *ngFor="let item of list; let i = index"><li>`
#####  &ensp;&ensp;*ngSwitch switch条件渲染
####   &ensp;3.angular常用事件
#####  &ensp;&ensp;(click) 点击事件
#####  &ensp;&ensp;(mousedown) 鼠标按下事件
#####  &ensp;&ensp;(keydown) 键盘按下事件

####   &ensp;4.双向绑定[(model)]
```
import {FormsModule} from '@angular/forms';
@NgModule{
    imports:[FormsModule]
}

<input [(model)]="name" />
```
#### &ensp;5.引入并注册服务
#####  &ensp;&ensp;使用 ng g service service-name or dirname/service-name 创建服务
```
ng g service services/storage

//app.module.ts
import {StorageService} form './services/storage.service';
@NgModule{
    providers:[StorageService]
}

//storage.service

import { Injectable } from "@angular/core";

@Injectable({
  providedIn: "root"
})
export class StorageService {
  constructor() {}
  get() {
    return "this is a service";
  }
}

接下来我们可以在别的组件中引入StorageService服务

//home.components.ts
import { StorageService } from "../../services/storage.service";

export class HomeComponent implements OnInit{
    constructor(public storage: StorageService){
        console.log(this.storage.get())
    }
}
```
#### &ensp;6.父子组件传参 Input,ViewChild,Output EventEmmiter
##### &ensp;&ensp;Input 父组件向子组件传参
```
//parent component

  <app-child [msg]="msg"></app-child>
  
//child component
  import {Component,OnInit,Input} from '@angular/core';
  export class ChildComponent implements OnInit{
     @Input() msg:string='';
     constructor(){
         console.log(this.msg)    
      }
  }
  ```
 #####  &ensp;&ensp;ViewChild 父组件获取子组件的方法和数据
 ```
 //parent component
   
   <app-child #myChild></app-child>
   
   import {Component,OnInit,ViewChild} from '@angular/core';
   
   export class ParentComponent implements OnInit{
       @ViewChild("myChild") myChild:any    *angular7
       @ViewChild("myChild",{static:true}) myChild:any    *angular8 要传入2个参数
       
       run(){
           console.log(this.myChild.msg)
           this.myChild.run();
       }
   }
 ```
 ##### &ensp;&ensp;Output EventEmmiter 父组件获取子组件的方法和数据
 
 ```
 //child component
 
 <button (click)="childRun()">ChildRun</button>
 
 import {Component,OnInit,OutPut,EventEmmiter} from '@angular/core';
 export class ChildComponent implements OnInit{
     @Output() outer = new EventEmmiter();
     childRun(){
         this.outer.emit('我是子组件中的Run方法')
     }
 }
 
 //parent component
 
 <app-child (outer)="parentRun($event)"></app-child>
 
  export class ParentComponent implements OnInit{
    
     parentRun(e){
        alert(e);
     }
 }
 ```
 #### &ensp;7.angular中的生命周期
<!--##### &ensp;&ensp;Input 父组件向子组件传参-->