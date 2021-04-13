# nSum
## 两数之和
leetcode第1题。题中加上假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。
	
	public int[] twoSum(int[] nums, int target) {
    
        HashMap<Integer,Integer> map=new HashMap<>();
        for(int i=0;i<nums.length;i++){
            map.put(nums[i],i);
        }
        for(int i=0;i<nums.length;i++){
            int other=target-nums[i];
            if(map.containsKey(other)&& i!=map.get(other)){
                return new int[]{i,map.get(other)};
            }
        }
        return new int[]{};
    }
    
如果不是，放回的不是下标而是数组的值，可以排序后用双指针的思路

	public List<List<Integer>> twoSum(int[] nums,int lo, int target) {
        Arrays.sort(nums);
        int hi=nums.length-1;
        List<List<Integer>> res=new ArrayList<>();
        while(lo < hi){
            int sum = nums[lo] + nums[hi];
            int left = nums[lo], right = nums[hi];
            if (sum < target) {
                while (lo < hi && nums[lo] == left) lo++;
            } else if (sum > target) {
                while (lo < hi && nums[hi] == right) hi--;
            } else {
                List<Integer> list=new ArrayList<>();
                list.add(left);
                list.add(right);
                res.add(list);
                while (lo < hi && nums[lo] == left) lo++;
                while (lo < hi && nums[hi] == right) hi--;
            }
        }
        return res;
    }
    
    
## 三数之和
上文两数之和的埋笔

	public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> list=new ArrayList<>();
        for(int i=0;i<nums.length;i++){
            List<List<Integer>> temp=twoSum(nums,i+1,0-nums[i]);
            for(List<Integer> l:temp){
                l.add(nums[i]);
                list.add(l);
            }
            while( i < nums.length-1 && nums[i]==nums[i+1]){
                i++;
            }
        }
        return list;
    }

    public List<List<Integer>> twoSum(int[] nums,int lo, int target) {
        Arrays.sort(nums);
        int hi=nums.length-1;
        List<List<Integer>> res=new ArrayList<>();
        while(lo < hi){
            int sum = nums[lo] + nums[hi];
            int left = nums[lo], right = nums[hi];
            if (sum < target) {
                while (lo < hi && nums[lo] == left) lo++;
            } else if (sum > target) {
                while (lo < hi && nums[hi] == right) hi--;
            } else {
                List<Integer> list=new ArrayList<>();
                list.add(left);
                list.add(right);
                res.add(list);
                while (lo < hi && nums[lo] == left) lo++;
                while (lo < hi && nums[hi] == right) hi--;
            }
        }
        return res;
    }


