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


## 5. Longest Palindromic Substring
### Approach:
A palindrome can start with 'a', 'aa', so for each letter in a string, we expand from it
and get the size of the possible palindrome, by calling recursion of (s, start - 1, end + 1);
keep track of visited by putting 'X' on visited nodes,   
we will call dfs helper on ever

```
string longestPalindrome(string s) {
    string result = "";
    int max_count = 0;
    for (int i = 0; i < s.size(); i++) {
        int one_letter = isPalindrome(s, i, i);
        int two_letter = isPalindrome(s, i, i + 1);
        int max_string = max(one_letter, two_letter);
        if (max_string > max_count) {
            max_count = max_string;
            int start = i - (max_count - 1) / 2;
            result = s.substr(start, max_count);
        }

    }
    return result;
}

int isPalindrome(string& s, int start, int end) {
    if (start < 0 || end == s.size() || s[start] != s[end]) {
        return 0;
    } else if (start - end == 0) {
        return 1 + isPalindrome(s, start - 1, end + 1);
    } else {
        return 2 + isPalindrome(s, start - 1, end + 1);
    }
}
```


212. Word Search II

Idea here is to build a Trie that can store the entire word and whenever we see
a letter matching the Trie, we check the next letter in the Trie using
word[i] - 'a' as an index using dfs x {x-1, x + 1, y-1, y+1}

DFS end condition:
isEnd is reached on Trie
out of range in table
if the index is not found on Trie

    h
e     e
l     l
l     e
o     n

```
private:
    class Trie{
        public:
        Trie* values[26];
        bool isEnd;
        int idx;

        Trie() {
            fill_n(this->values, 26, nullptr);
            isEnd = false;
            idx = 0;
        }
    };


    void insert_word(Trie* root, string& word, int idx) {
        for (int i = 0; i < word.size(); i++) {
            int index = word[i] - 'a';
            if (root->values[index] == nullptr) root->values[index] = new Trie();
            root = root->values[index];
        }
        root->isEnd = true;
        root->idx = idx;
    }

    void find_word(Trie* root, int i, int j, vector<vector<char>>& board, unordered_set<string>& result, vector<string>& word) {
        if (i < 0 || j < 0 || i >= board.size() || j >= board[0].size()) {
            return;
        }
        int index = board[i][j] - 'a';
        if (board[i][j] == 'X') {
            return;
        } else if (root->values[index] == nullptr) {
            return;
        } else if (root->values[index]->isEnd) {
            result.insert(word[root->values[index]->idx]);
            root->values[index]->isEnd = false;
        }

        char temp = board[i][j];
        root = root->values[index];
        board[i][j] = 'X';
        find_word(root, i + 1, j, board, result, word);
        find_word(root, i - 1, j, board, result, word);
        find_word(root, i , j + 1, board, result, word);
        find_word(root, i, j - 1, board, result, word);
        board[i][j] = temp;
    }
public:
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        if (board.size() == 0 || words.size() == 0) {
            return {};
        }
        unordered_set<string> s;
        Trie* root = new Trie();
        vector<string> result;
        int wordCount = words.size();
        for (int i = 0; i < words.size(); i++) {
            insert_word(root, words[i], i);
        }
        for (int i = 0; i < board.size(); i++) {
            for (int j = 0; j < board[0].size() && wordCount > s.size(); j++) {
                find_word(root, i, j, board, s, words);
            }
        }
        result.insert(result.end(), s.begin(), s.end());
        return result;
    }
```
