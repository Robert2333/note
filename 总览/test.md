  


# Two Sum

Given an array of integers, return **indices **of the two numbers such that they add up to a specific target.

You may assume that each input would have**exactly**one solution, and you may not use thesameelement twice.

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

简要：即给你一个数组，一个数，求出数组中哪两个元素相加之和等于给定的值

```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i=0;i<nums.length;i++){
            for(int j=0;j<nums.length && j!=i;j++){
                if(nums[i]+nums[j]==target)
                {
                    int [] result=new int[2];
                    result[0]=i;
                    result[1]=j;
                    return result;
                }
            }
        }
        return null;
    }
}
```

我的解决方案如上，可知，时间复杂度为$$O(n^2)$$

---

$$O(1)$$解决方案，用空间换时间，使用HashMap的索引

```
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[] { map.get(complement), i };
        }
        map.put(nums[i], i);
    }
    throw new IllegalArgumentException("No two sum solution");
}
```

**Complexity Analysis:**

* Time complexity :O\(n\)O\(n\). We traverse the list containingnnelements only once. Each look up in the table costs onlyO\(1\)O\(1\)time.

* Space complexity :O\(n\)O\(n\). The extra space required depends on the number of items stored in the hash table, which stores at mostnnelements.



