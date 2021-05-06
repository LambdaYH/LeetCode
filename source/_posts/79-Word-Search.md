---
title: 79. Word Search
date: 2021-04-07 16:55:11 +0800
categories: leetcode
tags: 
- BackTrack
---
#### [79. Word Search](https://leetcode.com/problems/word-search/)

##### backtrack
```c++
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        for(int i = 0; i < board.size(); ++i)
        {
            for(int j = 0; j < board[0].size(); ++j)
            {
                if(word[0] == board[i][j])
                {
                    board[i][j] -= 65;
                    if(backTrack(board, word.substr(1), i ,j))
                        return true;
                    board[i][j] += 65;
                }     
            }
        }
        return false;
    }
private:
    bool backTrack(vector<vector<char>>& board, string word, int i, int j)
    {
        if(word == "")
            return true;
        if(i > 0 && word[0] == board[i - 1][j])
        {
            board[i - 1][j] -= 65;
            if(backTrack(board, word.substr(1), i - 1, j))
                return true;
            board[i - 1][j] += 65;
        }
        if(j > 0 && word[0] == board[i][j - 1])
        {
            board[i][j - 1] -= 65;
            if(backTrack(board, word.substr(1), i, j - 1))
                return true;
            board[i][j - 1] += 65;
        }
        if(i < board.size() - 1 && word[0] == board[i + 1][j])
        {
            board[i + 1][j] -= 65;
            if(backTrack(board, word.substr(1), i + 1, j))
                return true;
            board[i + 1][j] += 65;
        }
        if(j < board[0].size() - 1 && word[0] == board[i][j + 1])
        {
            board[i][j + 1] -= 65;
            if(backTrack(board, word.substr(1), i, j + 1))
                return true;
            board[i][j + 1] += 65;
        }
        return false;
    }
};
```
T(n) : O(n^2)<br>
S(n) : O(1)

一点开始搜索其周围

##### 优化
```c++
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        for(int i = 0; i < board.size(); ++i)
        {
            for(int j = 0; j < board[0].size(); ++j)
            {
                if(word[0] == board[i][j])
                    if(backTrack(board, word, i ,j, 1))
                        return true;   
            }
        }
        return false;
    }
private:
    bool backTrack(vector<vector<char>>& board, string& word, int i, int j, int index)
    {
        if(index == word.size())
            return true;
        board[i][j] -= 65;
        if(i > 0 && word[index] == board[i - 1][j])
        {
            if(backTrack(board, word, i - 1, j, index + 1))
                return true;
        }
        if(j > 0 && word[index] == board[i][j - 1])
        {
            if(backTrack(board, word, i, j - 1, index + 1))
                return true;
        }
        if(i < board.size() - 1 && word[index] == board[i + 1][j])
        {
            if(backTrack(board, word, i + 1, j, index + 1))
                return true;
        }
        if(j < board[0].size() - 1 && word[index] == board[i][j + 1])
        {
            if(backTrack(board, word, i, j + 1, index + 1))
                return true;
        }
        board[i][j] += 65;
        return false;
    }
};
```