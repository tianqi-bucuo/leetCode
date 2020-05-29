请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。


利用双端队列的两端皆可添加元素的特性，设打印列表（双端队列） tmp ，并规定：
- 奇数层 则添加至 tmp 尾部 ，
- 偶数层 则添加至 tmp 头部 。

```Java
public List<List<Integer>> levelOrder(TreeNode root) {
    Queue<TreeNode> queue = new LinkedList<>();
    List<List<Integer>> res = new ArrayList<>();
    if(root != null) 
        queue.add(root);
    while(!queue.isEmpty()) {
        LinkedList<Integer> tmp = new LinkedList<>();
        for(int i = queue.size(); i > 0; i--) {
            TreeNode node = queue.poll();
            if(res.size() % 2 == 0){
                // 偶数层 -> 队列头部
                tmp.addLast(node.val); 
            }else{
                // 奇数层 -> 队列尾部
                tmp.addFirst(node.val);
            }  
            if(node.left != null) 
                queue.add(node.left);
            if(node.right != null) 
                queue.add(node.right);
        }
        res.add(tmp);
    }
    return res;
}
```