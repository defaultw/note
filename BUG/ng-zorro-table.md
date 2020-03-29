#### 1.发现日期

2020年3月29日 22 : 26 : 33

#### 2.问题描述

对zorro的table组件的`[nZData]`使用`push`,`splice`增加或删除内容的时候未生效。

```typescript
add() {
  lists.forEach(item => {
    this.listOfData.push(item);
  });
}

// 删除
delete(i) {
  this.listOfData.splice(i, 1);
}
```

#### 3.问题原因

`push()` 和 `splice()`这俩函数是直接在原始数组上进行操作的，会改变原数组，但是不会改变数组的引用。在angular的设计中，`onChanges()` 监听的是引用的变化。

#### 4.如何发现

使用`push`修改数据源界面未生效。

#### 5.如何修复

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'nz-demo-table-basic',
  template: `
    <nz-table #basicTable [nzData]="listOfData">
      <thead>
        <tr>
          <th>Name</th>
          <th>Age</th>
          <th>Address</th>
        </tr>
      </thead>
      <tbody>
        <tr *ngFor="let data of basicTable.data">
          <td>{{ data.name }}</td>
          <td>{{ data.age }}</td>
          <td>{{ data.address }}</td>
        </tr>
      </tbody>
    </nz-table>
    <input type="button" value="add" (click)="add()">
    <input type="button" value="delete" (click)="delete(1)">
  `
})
export class NzDemoTableBasicComponent {
  listOfData = [];

  add() {

    const lists = [
      {
        key: '1',
        name: 'John Brown',
        age: 32,
        address: 'New York No. 1 Lake Park'
      },
      {
        key: '2',
        name: 'Jim Green',
        age: 42,
        address: 'London No. 1 Lake Park'
      },
      {
        key: '3',
        name: 'Joe Black',
        age: 32,
        address: 'Sidney No. 1 Lake Park'
      }
    ];
    // 新增
    lists.forEach(item => {
      // 此处有两种写法，可以使用push，也可以直接使用[...this.listOfData, item]来添加元素
      // this.listOfData.push(item);
      this.listOfData = [...this.listOfData, item];
    });
  }

  // 删除
  delete(i) {
    // 此处删除有两种写法，可以使用splice,可以使用this.listOfData.filter
    // this.listOfData.splice(i, 1);
    // this.listOfData = [...this.listOfData];
    // 这边传入的i为可以的值，如果与表格内容的key相等则删除（语句解释为：当i与key不相等时，则在新创建的数组中添加该元素）
    this.listOfData = this.listOfData.filter(d => d.key !== i);
  }
  
}
```

#### 6.总结

按照 [Angular 的设计](https://angular.io/guide/lifecycle-hooks#onchanges)，当需要对 `nzData` 中的数据进行增删时需要使用以下操作，使用 `push` 或者 `splice` 修改 `nzData` 的数据不会生效

```typescript
// 增加数据
this.dataSet = [ ...this.dataSet, {
  key    : `${this.i}`,
  name   : `Edward King ${this.i}`,
  age    : '32',
  address: `London, Park Lane no. ${this.i}`
}];
// 删除数据
this.dataSet = this.dataSet.filter(d => d.key !== i);
```

其中，删除的语句`filter()` 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。 