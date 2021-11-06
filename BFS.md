# BFS 广度优先遍历

    // 计算从起点 start 到终点 target 的最近距离
    int BFS(Node start, Node target) {
        Queue<Node> q; // 核心数据结构
        Set<Node> visited; // 避免走回头路

        q.offer(start); // 将起点加入队列
        visited.add(start);
        int step = 0; // 记录扩散的步数

        while (q not empty) {
            int sz = q.size();
            /* 将当前队列中的所有节点向四周扩散 */
            for (int i = 0; i < sz; i++) {
                Node cur = q.poll();
                /* 划重点：这里判断是否到达终点 */
                if (cur is target)
                    return step;
                /* 将 cur 的相邻节点加入队列 */
                for (Node x : cur.adj())
                    if (x not in visited) {
                        q.offer(x);
                        visited.add(x);
                    }
            }
            /* 划重点：更新步数在这里 */
            step++;
        }
    }

二叉树按层遍历 leetcode第102题

	class Solution {
	    public List<List<Integer>> levelOrder(TreeNode root) {
	        List<List<Integer>> ret = new ArrayList<List<Integer>>();
	        if (root == null) {
	            return ret;
	        }
	
	        Queue<TreeNode> queue = new LinkedList<TreeNode>();
	        queue.offer(root);
	        while (!queue.isEmpty()) {
	            List<Integer> level = new ArrayList<Integer>();
	            int currentLevelSize = queue.size();
	            for (int i = 1; i <= currentLevelSize; ++i) {
	                TreeNode node = queue.poll();
	                level.add(node.val);
	                if (node.left != null) {
	                    queue.offer(node.left);
	                }
	                if (node.right != null) {
	                    queue.offer(node.right);
	                }
	            }
	            ret.add(level);
	        }
	        
	        return ret;
	    }
	}

二叉树的锯齿形层序遍历 leetcode第103题

	public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
	        List<List<Integer>> res=new LinkedList<>();
	        if(root==null){
	            return res;
	        }
	        Queue<TreeNode> queue=new LinkedList<>();
	        queue.offer(root);
	        boolean flag=true;
	        while(!queue.isEmpty()){
	            int size=queue.size();
	            LinkedList<Integer> level=new LinkedList<>();
	            for(int i=0;i<size;i++){
	                TreeNode cur=queue.poll();
	                if(flag){
	                    level.offerLast(cur.val);
	                }else{
	                    level.offerFirst(cur.val);
	                }
	                if(cur.left!=null){
	                    queue.offer(cur.left);
	                }
	                if(cur.right!=null){
	                    queue.offer(cur.right);
	                }
	            }
	            res.add(new LinkedList<Integer>(level));
	            flag=!flag;
	        }
	        return res;
	    }
        	
二叉树的最小高度 leetcode第111题
 
         public int minDepth(TreeNode root) {
            if(root ==null){
                return 0;
            }
            Queue<TreeNode> q=new LinkedList<>();
            q.offer(root);
            int mStep=1;
            while(!q.isEmpty()){
                int size =q.size();
                for(int i=0;i<size;i++){
                    TreeNode cur=q.poll();
                    if(cur.left==null && cur.right==null){
                        return mStep;
                    }
                    if(cur.left!=null){
                        q.offer(cur.left);
                    }
                    if(cur.right!=null){
                        q.offer(cur.right);
                    }
                }
                mStep++;
            }
            return mStep;
        }