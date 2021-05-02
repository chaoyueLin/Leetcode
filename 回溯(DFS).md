# 回溯
回溯就是全排列,就是深度优先遍历DFS

	result = []
	def backtrack(路径, 选择列表):
    	if 满足结束条件:
        	result.add(路径)
        	return

    	for 选择 in 选择列表:
        	做选择
        	backtrack(路径, 选择列表)
        	撤销选择
        	
 N皇后 leetcode第51题
 
     class Solution {
        
        List<List<String>> res = new ArrayList<>();
        
        public List<List<String>> solveNQueens(int n) {
            char[][] chessboard = new char[n][n];
            for (char[] c : chessboard) {
                Arrays.fill(c, '.');
            }
            backTrack(n, 0, chessboard);
            return res;
        }


        public void backTrack(int n, int row, char[][] chessboard) {
            if (row == n) {
                res.add(Array2List(chessboard));
                return;
            }

            for (int col = 0;col < n; ++col) {
                if (isValid (row, col, n, chessboard)) {
                    chessboard[row][col] = 'Q';
                    backTrack(n, row+1, chessboard);
                    chessboard[row][col] = '.';
                }
            }

        }


        public List Array2List(char[][] chessboard) {
            List<String> list = new ArrayList<>();
            
            for (char[] c : chessboard) {
                list.add(String.copyValueOf(c));
            }
            return list;
        }


        public boolean isValid(int row, int col, int n, char[][] chessboard) {
            // 检查列
            for (int i=0; i<n; ++i) {
                if (chessboard[i][col] == 'Q') {
                    return false;
                }
            }

            // 检查45度对角线
            for (int i=row-1, j=col-1; i>=0 && j>=0; i--, j--) {
                if (chessboard[i][j] == 'Q') {
                    return false;
                }
            }

            // 检查135度对角线
            for (int i=row-1, j=col+1; i>=0 && j<=n-1; i--, j++) {
                if (chessboard[i][j] == 'Q') {
                    return false;
                }
            }
            return true;
        }

    }
    
    
全排列，leetcode第46题

    List<List<Integer>> res = new LinkedList<>();

    /* 主函数，输入一组不重复的数字，返回它们的全排列 */
    List<List<Integer>> permute(int[] nums) {
        // 记录「路径」
        LinkedList<Integer> track = new LinkedList<>();
        backtrack(nums, track);
        return res;
    }

    // 路径：记录在 track 中
    // 选择列表：nums 中不存在于 track 的那些元素
    // 结束条件：nums 中的元素全都在 track 中出现
    void backtrack(int[] nums, LinkedList<Integer> track) {
        // 触发结束条件
        if (track.size() == nums.length) {
            res.add(new LinkedList(track));
            return;
        }

        for (int i = 0; i < nums.length; i++) {
            // 排除不合法的选择
            if (track.contains(nums[i]))
                continue;
            // 做选择
            track.add(nums[i]);
            // 进入下一层决策树
            backtrack(nums, track);
            // 取消选择
            track.removeLast();
        }
    }
    
子集,leetcode第78题

    class Solution {

        List<List<Integer>> res=new LinkedList<>();
        public List<List<Integer>> subsets(int[] nums) {
            LinkedList<Integer> track=new LinkedList<>();
            backTrack(track,nums,0);
            return res;
        }
        
        public void backTrack(LinkedList<Integer> track,int[] nums,int start){
            res.add(new ArrayList<>(track));
            for(int i=start;i<nums.length;i++){
                track.add(nums[i]);
                backTrack(track,nums,i+1);
                track.removeLast();
            }
            
        }
    }
    
    
组合,leetcode第77题

    class Solution {
        List<List<Integer>> res=new ArrayList<>();
        public List<List<Integer>> combine(int n, int k) {
            if(n<=0|| k<=0){
                return res;
            }
            LinkedList<Integer> track=new LinkedList<>();
            backTrack(track,1,n,k);
            return res;
        }
        public void backTrack(LinkedList<Integer> track,int start,int n,int k){
            if(track.size()==k){
                res.add(new LinkedList<Integer>(track));
                return;
            }
            for(int i=start;i<=n;i++){
                track.add(i);
                backTrack(track,i+1,n,k);
                track.removeLast();
            }
        }
    }
    
    
括号生成,leetcode第22题

    class Solution {
        LinkedList<String> res=new LinkedList<>();
        public List<String> generateParenthesis(int n) {
            if(n==0){
                return res;
            }
            StringBuffer track=new StringBuffer();
            backTrack(track,n,n);
            return res;
        }
        public void backTrack(StringBuffer track,int left,int right){
            if(right<left){
                return;
            }
            if(left<0||right<0){
                return;
            }
            if(left==0&&right==0){
                res.add(track.toString());
            }
            track.append("(");
            backTrack(track,left-1,right);
            track.deleteCharAt(track.length() - 1);

            track.append(")");
            backTrack(track,left,right-1);
            track.deleteCharAt(track.length() - 1);
        }
    }
    
    
数独,leetcode第37题

    class Solution {
        public void solveSudoku(char[][] board) {
            backtrack(board,0,0);
        }
        boolean backtrack(char[][] board, int i, int j) {
            int m = 9, n = 9;
            if (j == n) {
                // 穷举到最后一列的话就换到下一行重新开始。
                return backtrack(board, i + 1, 0);
            }
            if (i == m) {
                // 找到一个可行解，触发 base case
                return true;
            }

            if (board[i][j] != '.') {
                // 如果有预设数字，不用我们穷举
                return backtrack(board, i, j + 1);
            } 

            for (char ch = '1'; ch <= '9'; ch++) {
                // 如果遇到不合法的数字，就跳过
                if (!isValid(board, i, j, ch))
                    continue;

                board[i][j] = ch;
                // 如果找到一个可行解，立即结束
                if (backtrack(board, i, j + 1)) {
                    return true;
                }
                board[i][j] = '.';
            }
            // 穷举完 1~9，依然没有找到可行解，此路不通
            return false;
        }

        boolean isValid(char[][] board, int r, int c, char n) {
            for (int i = 0; i < 9; i++) {
                // 判断行是否存在重复
                if (board[r][i] == n) return false;
                // 判断列是否存在重复
                if (board[i][c] == n) return false;
                // 判断 3 x 3 方框是否存在重复
                if (board[(r/3)*3 + i/3][(c/3)*3 + i%3] == n)
                    return false;
            }
            return true;
        }
        
    }