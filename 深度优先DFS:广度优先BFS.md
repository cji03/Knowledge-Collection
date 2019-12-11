### 深度优先DFS算法

从一棵树顶往下搜索，尽可能的找到最深处，如果没有更深的节点，返回上一节点走岔路继续向下，没有岔路返回上一层；这么一路优先深度搜索至全部搜索完。

```javascript
let deepTraversal1 = (node, nodeList = []) => {
  if (node !== null) {
    nodeList.push(node)
    let children = node.children
    for (let i = 0; i < children.length; i++) {
      deepTraversal1(children[i], nodeList)
    }
  }
  return nodeList
}
let deepTraversal2 = (node) => {
  let nodes = []
  if (node !== null) {
    nodes.push(node)
    let children = node.children
    for (let i = 0; i < children.length; i++) {
      nodes = nodes.concat(deepTraversal2(children[i]))
    }
  }
  return nodes
}
```

### 广度优先BFS算法

从一棵树顶点向下搜索，依次搜索它的所有相邻子节点（同层节点），搜索完之后再分别从这些相邻节点出发搜索他们的相邻子节点，直至所有节点搜索完。

```javascript
let widthTraversal2 = (node) => {
  let nodes = []
  let stack = []
  if (node) {
    stack.push(node)
    while (stack.length) {
      let item = stack.shift()
      let children = item.children
      nodes.push(item
      for (let i = 0; i < children.length; i++) {
        stack.push(children[i])
      }
    }
  }
  return nodes
}
```
