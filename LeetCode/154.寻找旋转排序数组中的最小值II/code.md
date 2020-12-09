# [154. 寻找旋转排序数组中的最小值 II](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)





具体思路[看自己的博客文章]()

## 方法：二分



```go

func findMin(nums []int) int {
	if len(nums) == 0 {
		return 0
	}

	l, r := 0, len(nums)-1
	for l <= r {
		if nums[l] < nums[r] {
			return nums[l]
		}
		mid := l + (r-l)>>1
		if nums[mid] > nums[r] {
			l = mid + 1
		} else if nums[mid] < nums[r] {
			r = mid
		} else if nums[mid] == nums[r] {
			r = r - 1
		}
	}

	//最后结束时一定有l = r + 1，所以因为r向左移动了一步就直接返回l
	return nums[l]
}
```

