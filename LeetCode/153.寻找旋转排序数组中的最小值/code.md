







具体思路[看自己的博客文章]()



## 方法：二分

```go

func findMin(nums []int) int {
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
			return nums[mid]
		}
	}

	//随便返回一个即可，不会走到这里
	//因为最小值一定存在
	return -1
}

```

