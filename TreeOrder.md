```
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None


def preOrderRecur(root):
    if root:
        print(root.val)
        preOrder(root.left)
        preOrder(root.right)

def preOrder(root):
    stack = []
    while root or stack:
        # 一直遍历左子树
        while root:
            print(root.val)
            stack.append(root)
            root = root.left
        # 没有左子节点，就弹出它的父节点，遍历它的右子节点
        root = stack.pop()
        root = root.right

def inOrderRecur(root):
    if root:
        inOrder(root.left)
        print(root.val)
        inOrder(root.right)

def inOrder(root):
    stack = []
    while root or stack:
        while root:
            stack.append(root)
            root = root.left
        # 每次从栈弹元素，说明当前节点不存在，就打印父节点（该节点是父节点的左子节点）
        root = stack.pop()
        print(root.val)
        root = root.right

def postOrderRecur(root):
    if root:
        postOrderRecur(root.left)
        postOrderRecur(root.right)
        print(root.val)

def postOrder(root):
    # 两个栈：栈2保存栈1的弹出顺序
    stack1 = [root]
    stack2 = []
    while len(stack1) > 0:
        node = stack1.pop()
        stack2.append(node)
        if node.left:
            stack1.append(node.left)
        if node.right:
            stack1.append(node.right)
    while len(stack2) > 0:
        print(stack2.pop().val)


root = TreeNode(10)
root.left = TreeNode(6)
root.right = TreeNode(15)
root.left.left = TreeNode(5)
root.left.right = TreeNode(7)
root.right.left = TreeNode(14)
root.right.right = TreeNode(16)

postOrderRecur(root)
```
