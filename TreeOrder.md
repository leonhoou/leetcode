## 二叉树

先序遍历（递归，非递归），中序遍历（递归，非递归），后序遍历（递归，非递归）

```
#include <iostream>
#include <stack>
#include <queue>
using namespace std;

struct Node {
    Node* left;
    Node* right;
    int val;
    Node(): left(NULL), right(NULL), val(-1) {}
    Node(int val): left(NULL), right(NULL), val(val) {}
};

// 广度优先遍历
void breadthOrder(Node* root) {
    queue<Node*> q;
    q.push(root);
    while(!q.empty()) {
        root = q.front(); q.pop();
        cout << root->val << " ";
        if(root->left != NULL) {
            q.push(root->left);
        }
        if(root->right != NULL) {
            q.push(root->right);
        }
    }
}

void preOrderRecur(Node* root) {
    if(root != NULL) {
        cout << root->val << " ";
        // 栈里面存的是root
        preOrderRecur(root->left);
        preOrderRecur(root->right);
    }
}

// 关键在于每次压栈root
void preOrder(Node* root) {
    stack<Node*> st;
    while(root != NULL || !st.empty()) {
        while(root != NULL) {
            cout << root->val << " ";
            st.push(root);
            root = root->left;
        }
        root = st.top(); st.pop();
        root = root->right;
    }
}

void inOrderRecur(Node* root) {
    if(root != NULL) {
        inOrderRecur(root->left);
        // 栈里面存的是root
        cout << root->val << " ";
        inOrderRecur(root->right);
    }
}

// 关键还是在于压栈root
void inOrder(Node* root) {
    stack<Node*> st;
    while(root != NULL || !st.empty()) {
        while(root != NULL) {
            st.push(root);
            root = root->left;
        }
        root = st.top(); st.pop();
        cout << root->val << " ";
        root = root->right;
    }
}

void postOrderRecur(Node* root) {
    if(root != NULL) {
        postOrderRecur(root->left);
        postOrderRecur(root->right);
        cout << root->val << " ";
    }
}

void postOrder(Node* root) {
    Node* leastNode = NULL;
    stack<Node*> st;
    while(root != NULL || !st.empty()) {
        // -- 这里是遍历左子节点
        while(root != NULL) {
            st.push(root);
            root = root->left;
        }
        // 关键在什么？
        // 在于访问根节点的时候，会先去遍历他的左子节点，遍历完之后，
        // 会返回到根节点，再去遍历它的右子节点，遍历完右子节点后，
        // 会返回到根节点，而从右子节点返回时，就不应该再去遍历他的右子节点了
        // -- 这里是返回到根节点
        root = st.top();
        // -- 这里是遍历其右子节点，并且不是从右子节点返回的话才处理右子节点
        if(root->right != NULL && root->right != leastNode) {
            root = root->right;
        }
        // 如果右节点为空，就弹栈并输出根节点，并使当前处理节点为NULL
        else {
            cout << root->val << " ";
            st.pop();
            leastNode = root;
            root = NULL;
        }
    }
}

void postOrderDoubleStack(Node* root) {
    stack<Node*> st1;
    // 保存st1的弹出顺序
    stack<Node*> st2;
    st1.push(root);
    while(!st1.empty()) {
        root = st1.top(); st1.pop();
        st2.push(root);
        if(root->left != NULL)
            st1.push(root->left);
        if(root->right != NULL)
            st1.push(root->right);
    }
    while(!st2.empty()) {
        cout << st2.top()->val << " ";
        st2.pop();
    }
}

int main() {
//    广度优先遍历：1 2 3 4 5 6 7 8
//    先序遍历递归：1 2 4 5 8 3 6 7
//    先序遍历非递归：1 2 4 5 8 3 6 7
//    中序遍历递归：4 2 8 5 1 6 3 7
//    中序遍历非递归：4 2 8 5 1 6 3 7
//    后序遍历递归：4 8 5 2 6 7 3 1
//    后序遍历非递归：4 8 5 2 6 7 3 1
//    双栈后序遍历非递归：4 8 5 2 6 7 3 1
//    Program ended with exit code: 0
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->left->right->left = new Node(8);
    root->right->left = new Node(6);
    root->right->right = new Node(7);
    cout << "广度优先遍历："; breadthOrder(root); cout << endl;
    cout << "先序遍历递归："; preOrderRecur(root); cout << endl;
    cout << "先序遍历非递归："; preOrder(root); cout << endl;
    cout << "中序遍历递归："; inOrderRecur(root); cout << endl;
    cout << "中序遍历非递归："; inOrder(root); cout << endl;
    cout << "后序遍历递归："; postOrderRecur(root); cout << endl;
    cout << "后序遍历非递归："; postOrder(root); cout << endl;
    cout << "双栈后序遍历非递归："; postOrderDoubleStack(root); cout << endl;
}


```

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
