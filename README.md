# Leetcode
[知必会](https://github.com/wangzheng0822/algo)
[https://github.com/yuanguangxin/LeetCode](https://github.com/yuanguangxin/LeetCode)

## [二叉树](./二叉树.md)
## [链表](./链表.md)
## [回溯](./回溯.md)
## [BFS（广度优先遍历）](./BFS.md)
## [动态规划](./动态规划.md)
## [常用数据结构设计](./常用数据结构设计.md)

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
    
    
### 吃葡萄
    long solution(long a, long b, long c) {
        long[] nums = new long[]{a, b, c};
        Arrays.sort(nums);
        long sum = a + b + c;

        // 能够构成三角形，可完全平分
        if (nums[0] + nums[1] > nums[2]) {
            return (sum + 2) / 3;
        }
        // 不能构成三角形，平分最长边的情况
        if (2 * (nums[0] + nums[1]) < nums[2]) {
            return (nums[2] + 1) / 2;
        }
        // 不能构成三角形，但依然可以完全平分的情况
        return (sum + 2) / 3;
    }
    
### 煎饼排序
leetcode第969题

    class Solution {
         List<Integer> list=new ArrayList<>();
        public List<Integer> pancakeSort(int[] arr) {
            sort(arr,arr.length);
            return list;
        }
       
        public void sort(int[] arr,int n){
            if(n==1){
                return;
            }
            int max=0;
            int maxIndex=0;
            for(int i=0;i<n;i++){
                if(arr[i]>max){
                    max=arr[i];
                    maxIndex=i;
                }
            }
            reverse(arr,0,maxIndex);
            list.add(maxIndex+1);
            reverse(arr,0,n-1);
            list.add(n);
            sort(arr,n-1);
        }
        public void reverse(int[] a,int i,int j){
            while(i<j){
                int temp=a[j];
                a[j]=a[i];
                a[i]=temp;
                i++;
                j--;
            }
        }
    }
    
    
### 接雨水
leetcode第42题

     class Solution {
        public int trap(int[] height) {
            if(height.length==0){
                return 0;
            }
            int left=0;
            int right=height.length-1;
            int res=0;
            int leftMax=height[0];
            int rightMax=height[height.length-1];
            while(left<=right){
                leftMax=Math.max(leftMax,height[left]);
                rightMax=Math.max(rightMax,height[right]);
                if(leftMax<rightMax){
                    res += leftMax-height[left];
                    left++;
                }else{
                    res+=rightMax-height[right];
                    right--;
                }
            }
            return res;
        }
    }

### 最长回文子串
leetcode第5题

    class Solution {
        public String longestPalindrome(String s) {
            String res="";
            for(int i=0;i < s.length();i++){
                String temp1=lp(s,i,i);
                String temp2=lp(s,i,i+1);
                res=res.length()>temp1.length()?res:temp1;
                res=res.length()>temp2.length()?res:temp2;
            }
            return res;
        }

        public String lp(String s,int left,int right){
            while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
                --left;
                ++right;
            }
            return s.substring(left+1,right);
        }
    }
    
    
### 括号合法性
leetcode第20题

    class Solution {
        public boolean isValid(String s) {
            Stack<Character> stack=new Stack<>();
            for(char c:s.toCharArray()){
                if(c=='('||c=='{'||c=='['){
                    stack.push(c);
            
                }else{
                    if(!stack.isEmpty() && get(c)==stack.peek()){
                        stack.pop();
                    }else{
                        return false;
                    }
                    
                }
            }
            return stack.isEmpty();
        }
        public Character get(char c){
            if(c==')'){
                return '(';
            }
            if(c=='}'){
                return '{';
            }
            if(c==']'){
                return '[';
            }
            return ' ';
        }
    }