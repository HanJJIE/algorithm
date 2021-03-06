3.二叉查找树（Binary Search Tree）
=====

### 简介
- 二叉排序树（Binary Sort Tree），又称二叉查找树（Binary Search Tree），亦称二叉搜索树
- 二叉查找树或者是一棵空树，或者是具有下列性质的二叉查找树：
    1. 若左子树不空，则左子树上所有结点的值均小于它的根结点的值；
    2. 若右子树不空，则右子树上所有结点的值均大于它的根结点的值；
    3. 左、右子树也分别为二叉排序树；
    4. 没有键值相等的结点
    
### 实现
```java
public class BinarySearchTree<Key extends Comparable<Key>, Value> {

    private class Node {
        Key key;
        Value value;
        Node left, right;
        int nodeNumber;
        public Node(Key key, Value value, int nodeNumber) {
            this.key = key;
            this.value = value;
            this.nodeNumber = nodeNumber;
        }
    }

    //    根节点
    private Node root;

    /**
     * 返回二叉树节点个数
     * @return size
     */
    public int size() { return size(root); }

    /**
     * 以此节点为二叉树的节点个数
     * @param node 一颗二叉树根节点
     * @return size
     */
    private int size(Node node) {
        if (node == null) return 0;
        else return node.nodeNumber;
    }

    public boolean isEmpty() { return root == null; }

    /**
     * 添加节点
     * @param key 键
     * @param value 值
     */
    public void put(Key key, Value value) { root = put(root, key, value); }
    private Node put(Node node, Key key, Value value) {
//        根节点为空
        if (node == null) return new Node(key, value, 1);
//        与根节点进行比较
        int cmp = key.compareTo(node.key);
        if (cmp < 0) node.left = put(node.left, key, value);
        else if (cmp > 0) node.right = put(node.right, key, value);
        else node.value = value;
        node.nodeNumber = size(node.left) + size(node.right) + 1;
        return node;
    }

    /**
     * 获取节点值
     * @param key 键
     * @return value
     */
    public Value get(Key key) { return get(root, key); }
    private Value get(Node node, Key key) {
        if (node == null) return null;
        int cmp = key.compareTo(node.key);
        if (cmp < 0) return get(node.left, key);
        else if (cmp > 0) return get(node.right, key);
        else return node.value;
    }

}
```