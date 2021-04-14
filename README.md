# Leetcode
[知必会](https://github.com/wangzheng0822/algo)
[https://github.com/yuanguangxin/LeetCode](https://github.com/yuanguangxin/LeetCode)

## [二叉树](./二叉树.md)
## [链表](./链表.md)
## [回溯](./回溯.md)
## [BFS（广度优先遍历）](./BFS.md)
## [动态规划](./动态规划.md)
## [常用数据结构设计](./常用数据结构设计.md)

打乱数组（洗牌）leetcode第384题

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

