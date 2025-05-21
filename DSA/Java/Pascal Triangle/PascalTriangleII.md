# Pascal Triangle II

level: Easy, Medium
Submission Date: May 21, 2025
type: arrays, dynamic programming
Date: May 21, 2025

```java
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> ans = new ArrayList<>();
        for(int i = 0; i < rowIndex; i++ ){
            if(i==0 || i==rowIndex) ans.add(1);
            else{
                int no = pascalNo(rowIndex, i);
                ans.add(no);
            }
        }

        ans.add(1);

        return ans;
    }

    public int pascalNo(int i, int j ){
        if( i==0 || i==1 || j==0 || i==j){
            return 1;
        }
        int a = pascalNo(i-1, j); 
        int b = pascalNo(i-1, j-1);

        return a+b;
    }
}
```

There are a few issues in my code that can be improved or fixed:

1. **Off-By-One in Loop Condition**:
    
    The loop should run until `i <= rowIndex`, not `i < rowIndex`, because Pascal's triangle is 0-indexed and the row index should start from 0.
    
2. **Inefficient Recursive Approach**:
    
    The function `pascalNo(i, j)` recursively calls itself, and this will be very inefficient for large values of `i` and `j`, as it recalculates the same values multiple times. It can be improved by either using **dynamic programming** (storing the results) or using an iterative approach.
    
3. **Edge Case Handling**:
    
    The base case checks for `i == 0 || i == 1 || j == 0 || i == j` are correct, but the recursion calls can be made more efficient to avoid redundant calculations.
    

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> ans = new ArrayList<>();
        
        // Start with the first element in the row, which is always 1
        ans.add(1);
        
        // Generate the row iteratively
        for (int i = 1; i <= rowIndex; i++) {
            // Update the row values in reverse order to avoid overwriting the values we need
            for (int j = i - 1; j > 0; j--) {
                ans.set(j, ans.get(j) + ans.get(j - 1)); // Update value in place
            }
            // Add the last element of the row, which is always 1
            ans.add(1);
        }
        
        return ans;
    }
}
```

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> row = new ArrayList<>();
        
        // Initialize the first row (rowIndex = 0), which is just [1]
        row.add(1);
        
        // Use DP to build the row from 1 to rowIndex
        for (int i = 1; i <= rowIndex; i++) {
            // Start by adding 1 at the beginning of the row
            row.add(1);
            
            // Update the row elements in reverse order (to avoid overwriting values)
            for (int j = i - 1; j > 0; j--) {
                row.set(j, row.get(j) + row.get(j - 1)); // Add value from previous row
            }
        }
        
        return row;
    }
}
```