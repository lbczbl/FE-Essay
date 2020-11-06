#### 前序遍历

##### 递归法  按照根节点、左子树、右子树的顺序，数组连接使用concat，且此函数并不改变数组本身

```javascript
var preorderTraversal = function(root) {
  if (!root) return []
  var result = []
  result.push(root.val)
  result = result.concat(preorderTraversal(root.left))
  result = result.concat(preorderTraversal(root.right))
  return result
}
```

##### 迭代法

迭代意在通过循环解决问题，建立一个栈，将根节点加入栈中，当栈不为空时：

1. 取出栈顶元素curr，访问curr
2. 若curr右子节点不为空，则将curr右子节点加入栈
3. 若curr左子节点不为空，则将curr左子节点加入栈

```javascript
var preorderTraversal = function(root) {
  if(!root) return []
  var result = [], stack = [root]
  while(stack.length !== 0) {
    var curr = stack.pop()
    if(curr.right) stack.push(curr.right)
    if(curr.left) stack.push(curr.left)
    result.push(curr.val)
  }
  return result
}
```

#### 中序遍历

##### 栈

```javascript
var inorderTraversal = function(root) {
  var res = []
  //栈
  var stack = []
  while( root || stack.length > 0) {
    //直至左节点为空，即没有左节点为止
    while(root) {
      stack.push(root)
      root = root.left
    }
    //出栈，存放根节点
    root = stack.pop()
    res.push(root.val)
    root = root.right
  }
  return res
};
```

##### 递归

```javascript
var inorderTraversal = function(root) {
  var res = []
  inorder(root, res)
  return res
}
function inorder(root, res) {
  if (!root) return
  inorder(root.left, res)
  res.push(root.val)
  inorder(root.right, res)
}
```

#### 后序遍历

```javascript
var postorderTraversal = function(root) {
  let res = []
  postorder(root, res)
  return res
}
function postorder(root, res) {
  if(!root) return
  postorder(root.left, res)
  postorder(root.right, res)
  res.push(root.val)
}
```

