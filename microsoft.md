## 54. Spiral Matrix
### Approach:
Setup a vector of {{0, 1}, {1, 0}, {0, -1}, {-1, 0}},  
As you can see, after each direction change, the number of moves decrease by 1  
after each traverse in each direction, increase index, and lower moves by 1,  
can you use % 2 to determine whether it is going up/down left/right

#### tips:
use index % 4 to guarantee 0 to 3

```
vector<int> spiralOrder(vector<vector<int>>& matrix) {
    vector<pair<int, int>> direction = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    vector<int> result;
    if (matrix.size() == 0) return {};
    int rr = matrix.size(), cc = matrix[0].size();
    int row = 0, col = -1;
    vector<int> matrix_length = {cc, rr - 1};
    int index = 0;
    while (matrix_length[index % 2]) {
        for (int i = 0; i < matrix_length[index % 2]; i++ ) {
            result.push_back(matrix[row += direction[index].first][col += direction[index].second]);
        }
        matrix_length[index % 2]--;
        index = ++index % 4;
    }
    return result;
}
```
