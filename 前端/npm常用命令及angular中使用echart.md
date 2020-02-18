## 一、npm常用命令

```shell
npm install xxx利用 npm 安装xxx模块到当前命令行所在目录
npm install -g xxx利用npm安装全局模块xxx

npm install xxx             安装但不写入package.json
npm install xxx –-save       安装并写入package.json的”dependencies”中
npm install xxx -–save-dev  安装并写入package.json的”devDependencies”中

npm uninstall xxx      删除xxx模块
npm uninstall -g xxx   删除全局模块xxx

ionic plugin list           列出所有已安装插件
ionic plugin remove xxx     根据插件名卸载
ionic plugin add xxx        添加地址可以是github的项目地址，也可以是一个文件夹路径
ionic –help                 查看帮助
```



## 二、angular2引入echart

#### 1.安装

```shell
npm install echarts -save
npm install ngx-echarts -save
```

#### 2.在angular.json中引入echarts.min.js

```json
"scripts": [
     ....
     "node_modules/echarts/dist/echarts.min.js"
 ]
```

#### 3.在module中导入ngx-echarts的模块

```typescript
import { NgxEchartsModule } from 'ngx-echarts';

import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppComponent } from './app.component';

// 这个是使用到echart的组件，在组件创建时自动导入
import { EchartDemoBComponent } from './echart-demo-b/echart-demo-b.component'; 

@NgModule({
  declarations: [AppComponent, EchartDemoBComponent],
  imports: [BrowserModule, NgxEchartsModule],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {}

```

#### 4.在html中编写echart图表代码

```html
<!-- 这里的class只是占位， demo-class 可以替换为任意的自定义的class -->
<div echarts [options]="chartOption" style="height: 400px" class="demo-chart"></div>
<div echarts [options]="option" style="height: 400px" class="demo-chart"></div>
```

#### 5.在component中配置echart的options(配置信息)

```typescript
import { EChartOption } from 'echarts';

import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-echart-demo-b',
  templateUrl: './echart-demo-b.component.html',
  styleUrls: ['./echart-demo-b.component.css']
})
export class EchartDemoBComponent implements OnInit {
  public chartOption: EChartOption;
  constructor() {
    this.chartOption = {
      xAxis: {
        type: 'category',
        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
      },
      yAxis: {
        type: 'value'
      },
      series: [
        {
          data: [820, 932, 901, 934, 1290, 1330, 1320],
          type: 'line'
        }
      ]
    };
  }
  ngOnInit() {}
}
```



> 报错：
>
> Unexpected module 'NgxEchartsModule' declared by the module 'AppModule'. Please add a @Pipe/@Directive/@Component annotation.：
>
> 强调一点，Component在declarations中的，Module在import中的，这样你就不会出错了。



## 三、echart使用

#### 1.实例注释(一)：柱状图

```typescript
option = {
  color: ['#3398DB'],
  tooltip: {  // 
    trigger: 'axis',
    axisPointer: {
      // 坐标轴指示器，坐标轴触发有效
      //（设置鼠标悬浮柱子后显示样式，shadow显示阴影覆盖柱子，line是线在柱子中间）
      type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'
    }
  },
  grid: { // 图显示的位置
    left: '3%',
    right: '4%',
    bottom: '3%',
    containLabel: true // 是否包含标签
  },
  xAxis: [
    {
      type: 'category', // 横轴显示类别
      data: ['一线执法', '日常值班', '专项备勤', '武装处突'],
      axisTick: {
        alignWithLabel: true // 横轴的标是否与柱子中间对齐，为true是对齐
      },
      axisLabel: {
        show: true, // 横轴类别是否显示
        textStyle: { // 横轴字体样式
          color: '#999999'
        }
      }
    }
  ],
  yAxis: [
    {
      type: 'value',
      axisLabel: {
        show: true,
        textStyle: {
          color: '#999999'
        }
      }
    }
  ],
  series: [
    {
      name: '直接访问',
      type: 'bar', // 图类型
      barWidth: '60%', // 柱子宽度
      data: [
        {
          value: 100,
          itemStyle: {
            color: '#60acfc' // 柱子颜色
          }
        },
        {
          value: 10,
          itemStyle: {
            color: '#32d3eb'
          }
        },
        {
          value: 210,
          itemStyle: {
            color: '#5bc49f'
          }
        },
        {
          value: 150,
          itemStyle: {
            color: '#feb64d'
          }
        }
      ],
      itemStyle: {
        normal: {
          label: {
            show: true, // 是否显示柱子对应的数据
            position: 'top', // 数据在中间显示
            formatter: '{c}' // 百分比显示，模板变量有 {a}、{b}、{c}、{d}，分别表示系列名，数
            // 据名，数据值，百分比。{d}数据会根据value值计算百分比
          }
        }
      }
    }
  ]
};
```

> 注意： 其中在柱子顶端显示对应数字也可以写做
>
> ```typescript
> series:[{ // echart3.0写法
>     label: {
>         normal: {
>             show: true,
>             position: 'inside',
>             formatter: '{c},({d}%)'//多值的嵌套
>         }
>     }
> }]
> ```

#### 4.实例注释(二)：饼图

### 勤务产品清库脚本

## 四、取JSON的属性

```typescript
public object: any = { ids: { id1: '1', id2: '2' }, name: 'wang' };

for (const key in this.object) {
    if (this.object.hasOwnProperty(key)) { // 防止对从对象原型继承的属性进行意外迭代
        console.log(key);  // 输出 ids name
    }
}
```



## 五、angular2常用

#### 1.文件路径

```json
+---e2e                              // 在e2e/下是端到端（End-to-End）测试。
|       
+---node_modules                     // package.json中列举的所有第三方模块都放在其中
|
 \---src                             // 代码源文件
|    |   favicon.ico                 // 图标 
|    |   index.html                  // 网站首页
|    |   main.ts                     // 这是应用的主要入口点  
|    |   polyfills.ts                // 标准化   
|    |   styles.css                  // 样式文件
|    |   test.ts                     // 测试入口
|    |   tsconfig.app.json           // TypeScript编译器对应用的配置文件
|    |   tsconfig.spec.json          // TypeScript编译器对测试的配置文件
|    |   typings.d.ts                // TypeScript用于标记对象类型文件
|    |   
|    +---app                         // app模块文件夹，类似与java的包
|    |       app.component.css       // app模块的样式文件
|    |       app.component.html      // app模块的HTML模版
|    |       app.component.spec.ts   // app模块的测试文件
|    |       app.component.ts        // app模块逻辑处理
|    |       app.module.ts           // app模块入口
|    |       
|    +---assets                      // 资源文件夹
|    |       .gitkeep                // 没什么卵用，git用的
|    |       
|    \---environments                // 环境配置
|            environment.prod.ts     
|            environment.ts          
|
|   .angular-cli.json                // Angular CLI的配置文件
|   .editorconfig                    // 编辑器看的一个简单配置文件 
|   .gitignore                       // git用的，与svn的ignore一个意思
|   karma.conf.js                    // Karma的单元测试配置
|   package.json                     // npm配置文件，其中列出了项目使用到的第三方依赖包
|   protractor.conf.js               // 给Protractor使用的端到端测试配置文件
|   README.md                        // 项目说明文件
|   tsconfig.json                    // TypeScript编译器的配置
|   tslint.json                      // 代码风格 
```

#### 2.angular-cli 添加新的构建

[资源链接]([https://my.oschina.net/bluesummer/blog/916706#1-2-angularjs-1-x-%E7%9A%84%E5%9B%B0%E5%A2%83](https://my.oschina.net/bluesummer/blog/916706#1-2-angularjs-1-x-的困境))

| 命令                                   | 简写                    | 说明     |
| -------------------------------------- | ----------------------- | -------- |
| ng generate class my-new-class         | ng g cl my-new-class    | 创建类   |
| ng generate component my-new-component | ng g c my-new-component | 创建组件 |
| ng generate directive my-new-directive | ng g d my-new-directive | 创建指令 |
| ng generate enum my-new-enum           | ng g e my-new-enum      | 创建枚举 |
| ng generate module my-new-module       | ng g m my-new-module    | 创建模块 |
| ng generate pipe my-new-pipe           | ng g p my-new-pipe      | 创建管道 |
| ng generate service my-new-service     | ng g s my-new-service   | 创建服务 |
