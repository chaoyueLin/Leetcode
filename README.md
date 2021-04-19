# Leetcode
[知必会](https://github.com/wangzheng0822/algo)
[https://github.com/yuanguangxin/LeetCode](https://github.com/yuanguangxin/LeetCode)

## [二叉树](./二叉树.md)
## [链表](./链表.md)
## [回溯](./回溯.md)
## [BFS（广度优先遍历）](./BFS.md)
## [动态规划](./动态规划.md)
## [常用数据结构设计](./常用数据结构设计.md)

### 打乱数组（洗牌）
leetcode第384题

	class Solution {
	    private int[] array;
	    private int[] original;
	
	    Random rand = new Random();
	
	    private int randRange(int min, int max) {
	        return rand.nextInt(max - min) + min;
	    }
	
	    private void swapAt(int i, int j) {
	        int temp = array[i];
	        array[i] = array[j];
	        array[j] = temp;
	    }
	
	    public Solution(int[] nums) {
	        array = nums;
	        original = nums.clone();
	    }
	    
	    public int[] reset() {
	        array = original;
	        original = original.clone();
	        return original;
	    }
	    
	    public int[] shuffle() {
	        for (int i = 0; i < array.length; i++) {
	            swapAt(i, randRange(i, array.length));
	        }
	        return array;
	    }
	}

### 字符串相乘
leetcode第43题

    public String multiply(String num1, String num2) {
        if(num1.equals("0")|| num2.equals("0")){
            return "0";
        }
        int m=num1.length();
        int n=num2.length();
        int[] result=new int[m+n];
        for(int i=m-1;i>=0;i--){
            int x=num1.charAt(i) - '0';
            for(int j=n-1;j>=0;j--){
                int y=num2.charAt(j) - '0';
                result[i+j+1]+=x*y;
            }

        }
        for(int i=m+n-1;i>0;i--){
            result[i-1]+=result[i]/10;
            result[i]%=10;
        }
        for(int i=0;i<m+n;i++){
            System.out.print(result[i]);
        }
        int index=result[0]==0?1:0;
        StringBuilder sb=new StringBuilder();
        for(;index<m+n;index++){
            sb.append(result[index]);
        }
        return sb.toString();

    }
    
### 灯泡开关
leetcode第319题

	public int bulbSwitch(int n) {
        return (int)Math.sqrt(n);
    }
    
### 石头游戏
leetcode第877题

    public boolean stoneGame(int[] piles) {
        return true;
    }
