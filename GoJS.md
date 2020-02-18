## 一、简单的创建图形和节点等

```typescript
ngOnInit() {
    const diagram = new go.Diagram('myDiagramDiv'); // GraphObject对象
    // diagram.model = new go.GraphLinksModel(
    //   [{ key: 'hello' }, { key: 'world' }],
    //   [{ from: 'hello', to: 'world' }]);

    // 新建一个node(节点)
    const node = new go.Node(go.Panel.Auto);

    // 新建一个shape(图形)
    const shape = new go.Shape();
    shape.figure = 'RoundedRectangle'; // 样式：圆角
    shape.fill = 'lightBlue'; // 样式：颜色
    node.add(shape); // 把图形添加到节点

    // 新建textBlock(文本块)
    const textBlock = new go.TextBlock();
    textBlock.text = 'hello';
    textBlock.margin = 5;
    textBlock.scale = 2;
    node.add(textBlock);

    diagram.add(node); // 节点添加到GraphObject
 }
```

## 二、使用go.GraphObject.make

代码一：

```typescript
import * as go from 'gojs';
import { Component, OnInit } from '@angular/core';
const $ = go.GraphObject.make;
@Component({
  selector: 'app-gojs-com',
  template: `
    <div id="myDiagramDiv" style="border: solid 1px pink; width: 500px; height: 250px;"></div>
  `,
  styles: []
})
export class GojsComComponent implements OnInit {
  ngOnInit() {
    const diagram = new go.Diagram('myDiagramDiv');
    diagram.add(
      $(go.Node, 'Auto',
        $(go.Shape, {
          figure: 'RoundedRectangle', fill: $(go.Brush,
            { 0.0: 'blue', 1.0: 'lightblue' })
        }),
        $(go.TextBlock, { text: 'hello!', margin: 10 })
      )
    );
  }
}
```

代码二：

```typescript
const diagram = new go.Diagram('myDiagramDiv');
    const node1 = $(go.Node, 'Auto',
      $(go.Shape, {
        figure: 'RoundedRectangle', fill: $(go.Brush,
          { 0.0: 'blue', 1.0: 'lightblue' })
      }),
      $(go.TextBlock, { text: 'hello!', margin: 10 })
    );
    diagram.add(node1);

    const node2 = $(go.Node, 'Auto',
      $(go.Shape, { figure: 'RoundedRectangle', fill: 'pink' }),
      $(go.TextBlock, { text: 'World', margin: 10 })
    );
    diagram.add(node2);

    diagram.add(
      $(go.Link, { fromNode: node1, toNode: node2 },
        $(go.Shape))
    );
```

## 三、Using a Model and Templates

```typescript
    const diagram = new go.Diagram('myDiagramDiv');

    // 新建一个节点样式
    diagram.nodeTemplate = $(go.Node, 'Auto',
      $(go.Shape, { figure: 'RoundedRectangle', fill: 'white' }),
      $(go.TextBlock, { text: 'hello', margin: 5 })
    );

    const nodeDateArray = [
      { key: 'AAA' },
      { key: 'BBB' }
    ];
    const linkDAteArray = [
      { from: 'AAA', to: 'BBB' }
    ];

    diagram.model = new go.GraphLinksModel(nodeDateArray, linkDAteArray);
```

添加数据绑定之后：

```typescript
    const diagram = new go.Diagram('myDiagramDiv');

    // 新建一个节点样式
    diagram.nodeTemplate = $(go.Node, 'Auto',
      $(go.Shape,
        { figure: 'RoundedRectangle', fill: 'white' },
        new go.Binding('fill', 'color')),
      $(go.TextBlock, { text: 'hello', margin: 5 },
        new go.Binding('text', 'key'))
    );

    const nodeDateArray = [
      { key: 'AAA', color: 'lightblue' },
      { key: 'BBB', color: 'pink' }
    ];
    const linkDAteArray = [
      { from: 'AAA', to: 'BBB' }
    ];

    diagram.model = new go.GraphLinksModel(nodeDateArray, linkDAteArray);
```

通过json字符串加载数据：

```typescript
    const diagram = new go.Diagram('myDiagramDiv');
    // const a = {
    //   "class": "GraphLinksModel",
    //   "nodeDataArray": [
    //     {
    //       "key": "Alpha",
    //       "color": "lightblue",
    //       "Ioc": {
    //         "class": "go.Point",
    //         "x": 0,
    //         "y": 0
    //       }
    //     },
    //     {
    //       "key": "Beta",
    //       "color": "pink",
    //       "Ioc": {
    //         "class": "go.Point",
    //         "x": 100,
    //         "y": 50
    //       }
    //     }
    //   ],
    //   "linkDataArray": [
    //     {
    //       "from": "Alpha",
    //       "to": "Beta",
    //       "color": "blue",
    //       "thick": 2
    //     }
    //   ]
    // };
    diagram.nodeTemplate = $(go.Node, 'Auto',
      new go.Binding('location', 'Ioc'),
      $(go.Shape, 'RoundedRectangle',
        { fill: 'white' },
        new go.Binding('fill', 'color')
      ),
      $(go.TextBlock, { margin: 5 },
        new go.Binding('text', 'key')
      )
    );

    diagram.linkTemplate = $(go.Link,
      $(go.Shape,
        new go.Binding('stroke', 'color'),
        new go.Binding('strokeWidth', 'thick')),
      $(go.Shape,
        { toArrow: 'OpenTriangle', fill: null },
        new go.Binding('stroke', 'color'),
        new go.Binding('strokeWidth', 'thick')
      )
    );

    const nodeDateArray = [
      { key: 'Alpha', color: 'lightblue', Ioc: new go.Point(0, 0) },
      { key: 'Beta', color: 'pink', Ioc: new go.Point(100, 50) }
    ];

    const linkDateArray = [
      { from: 'Alpha', to: 'Beta', color: 'blue', thick: 2 }
    ];

    diagram.model = new go.GraphLinksModel(nodeDateArray, linkDateArray);
    // diagram.model = go.Model.fromJson(a);
    console.log(diagram.model.toJson());
  }
```

