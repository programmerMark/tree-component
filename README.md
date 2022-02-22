### 使用 ztree.js 创建的树型组件

#### 安装

```
npm i @programmermark/ztree
```

#### 参数说明

> id: 节点 id，唯一标识

> pid: 父级节点 id，没有父节点时，该参数为 undefined

> checked: checkbox 是否选中

> open: 节点是否展开,

> clickSelf: 为 true 时，点击事件只会选中自身； 为 false 时，点击事件会选中自身和子节点

除此之外，节点还可以自定义属性。具体请参看代码中的 typescript 注释。

#### 代码示例

```javascript

import React, { useState } from "react";
import "./App.css";
import { Tree, ITreeNode } from "@programmermark/ztree";

function App() {
  const [treeData, setTreeData] = useState<ITreeNode[]>([
    {
      id: "10000",
      pId: undefined,
      name: "湖北省",
      checked: true,
      open: false,
    },
    {
      id: "10001",
      pId: "10000",
      name: "武汉市",
      checked: true,
      open: true,
      clickSelf: true /** 为true时，点击事件只会选中自身 */,
    },
    {
      id: "10010",
      pId: "10001",
      name: "汉口",
      checked: true,
      open: true,
    },
    {
      id: "10011",
      pId: "10001",
      name: "武昌",
      checked: true,
      open: true,
    },
    {
      id: "10012",
      pId: "10001",
      name: "汉阳",
      checked: true,
      open: true,
    },
    {
      id: "10002",
      pId: "10000",
      name: "孝感市",
      checked: true,
      open: true,
    },
    {
      id: "10020",
      pId: "10002",
      name: "云梦",
      checked: true,
      open: true,
    },
    {
      id: "10021",
      pId: "10002",
      name: "大悟",
      checked: true,
      open: true,
    },
    {
      id: "10022",
      pId: "10002",
      name: "应城",
      checked: true,
      open: true,
    },
  ]);

  const handleUpdateExpandNode = (id: string, open: boolean) => {
    setTreeData((treeData) => {
      const newTreeData = treeData.map((node) => {
        if (node.id === id) {
          // 更新当前节点的展开状态
          return {
            ...node,
            open,
          };
        }
        return node;
      });
      return newTreeData;
    });
  };

  const handleUpdateNodes = (ids: string[], checked: boolean) => {
    setTreeData((treeData) => {
      const newTreeData = treeData.map((node) => {
        if (ids.includes(node.id)) {
          // 更新当前节点的选中状态
          return {
            ...node,
            checked,
          };
        }
        return node;
      });
      return newTreeData;
    });
  };

  return (
    <div className="App">
      <Tree
        nodes={treeData}
        updateExpandNode={handleUpdateExpandNode}
        updateNodes={handleUpdateNodes}
      />
    </div>
  );
}

export default App;
```
