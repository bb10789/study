# Math & Stats

For unique permutations, in each for-loop of the recursion, pass in a parameter i as start  
so the element before the current element don't get reran
parameter(int start, vector<vector<int>> result, vector<int> curr);
for (int i = start; i < nums.size; i++)

**Find kth Permutation**

| 1| 2|3 | 4|
|----|----|----|----|
|1234|2134|3214|4231|
|1243|2143|3241|4213|
|1324|2314|3124|4321|
|1342|2341|3142|4312|
|1432|2431|3412|4132|
|1423|2413|3421|4123|

with n = 4 and k = 9
we know that 9 is in the second column, we find that by dividing the n - 1 factorial  
factorial = {1, 1, 2, 6, 24}, so 9 / 6, since 6 is the # of rows there are in one column  
we break it down into each section until we are done

to find the position of each number:  
pos = k / factorial[n - 1]  
we also need to take care of the case where k % factorial == 0 bc while 6 is in the first row, 6 / 6 = 1 (should be 0)  

Helper method:
```
void permutation2String(int n, int k, vector<char>& nums, vector<int>& factorial, string& result) {
    if (nums.size() == 1) {
        result += nums[0];
    } else {
        int pos = k / factorial[n- 1];
        if (k % factorial[n - 1] == 0) pos--;
        result += nums[pos];
        nums.erase(nums.begin() + pos);
        permutation2String(n - 1, k - pos * factorial[n - 1], nums, factorial, result);
    }
}

```




**Integer Division Without Using * or /**

Check how many times a divisor can go in a dividend, and shift the bit << 1 if dividend is >= divisor << 1
subtract the dividend from divisor in the end

For example:
10 / 3
divisor 3 >> 6 -> 3 goes to while loop twice
dividend 9 -> ends
count = result + 1 >> 2 + 1

```
int divide(int dividend, int divisor) {
    int result = 0;
    if
    while (dividend - divisor > 0) {
        int currDivisor = divisor;
        int count = 1;
        while (currDivisor << 1 <= dividend) {
            currDivisor <<= 1;
            count <<= 1;
        }
        dividend -= divisor;
        result += count;
    }
    return result;
}
```

**Pythagorean Triplets**

**All Possible Combinations for a Given Sum**
basically like Permutations, however, to get unique elements, we have to pass in a start that signifies the start of for loop

**Find Missing Number**
n *(n + 1) /2, find all number to the size of array, then subtract by the total sum found in the actual array
3, 0, 1

3 * (3 + 1) /2 = 6  6 - (3 + 0 + 1) = 2

```
int missingNumber(vector<int> nums) {
	int result = 0;
	int i = 0;

	for (int num : nums) {
		result += num;
	}
	int size = nums.size();
	return (size * (size + 1) / 2) - result;
}
```

or you can use XOR, just XOR everything and the remaining number should be that, bc 1 | 1 == 0 but 1 | 0 == 1   

```
int missingNumber(vector<int>& nums) {
    int result = nums.size();
    int i = 0;
    for (int x : nums) {
        result ^= x ^ i++;
    }
    return result;
}
```

**Permutations2**

**Find All Subsets of a Set**
start with one element, and we copy the previous ones to put it into the back of the array
so {} {1} -> {} {1} {} {1} -> {} {1} {2} {1, 2}
**Is String a Valid Number?**

**Calculate Power of a Number**

**Calculate Square Root of a Number**
