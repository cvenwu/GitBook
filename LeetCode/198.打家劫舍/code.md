# [198. 打家劫舍](https://leetcode-cn.com/problems/house-robber/)

## 方法一：自己的dp

步骤：
1. 明确base case：dp[0][0]=0,
               dp[0][1]=nums[0]
2. 状态：dp[i][0]，
         其中第2维取值0，1分别表示不偷，偷。
         其中第1维表示偷到第i个房屋时可以获取的最大偷窃金额
3. 选择：偷 或 不偷
4. 状态转移方程：
      dp[i][0] = max(dp[i-1][0], dp[i-1][1])
      dp[i][1] = dp[i-1][0] + nums[i]


> 执行用时：0 ms, 在所有 Go 提交中击败了100.00%的用户
> 		内存消耗：2.1 MB, 在所有 Go 提交中击败了5.44%的用户

```go
func rob(nums []int) int {
	if len(nums) <= 0 {
		return 0
	}

	dp := [][]int{{0, nums[0]}}

	for i := 1; i < len(nums); i++ {
		dp = append(dp, []int{max(dp[i-1][0], dp[i-1][1]), dp[i-1][0] + nums[i]})
	}

	return max(dp[len(nums)-1][0], dp[len(nums)-1][1])

}
func max(num, num2 int) int {
	if num > num2 {
		return num
	}

	return num2
}
```



## 方法二：LeetCode上的dp


步骤：
1. 明确base case：dp[0]=nums[0],
2. 状态：dp[i]表示前 i 间房屋能偷窃到的最高总金额
3. 选择：偷 或 不偷
4. 状态转移方程：
      dp[i] = max(dp[i-1], dp[i-2]+nums[i])

> 执行用时：0 ms, 在所有 Go 提交中击败了100.00%的用户
> 		内存消耗：2 MB, 在所有 Go 提交中击败了57.77%的用户

```go
func rob(nums []int) int {
	if len(nums) <= 0 {
		return 0
	}

	dp := []int{nums[0]}

	for i := 1; i < len(nums); i++ {
		dp = append(dp, max(nums[i] + dp[i-2], dp[i-1]))
	}

	return dp[len(nums)-1]

}

func max(num, num2 int) int {
	if num > num2 {
		return num
	}

	return num2
}
```

