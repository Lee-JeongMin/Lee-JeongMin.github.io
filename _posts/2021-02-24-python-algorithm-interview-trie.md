---
layout: post
title: 파이썬 알고리즘 인터뷰_트라이
subtitle : 
tags: [Python Algorithm]
author: JeongMin Lee
comments : True
---

### 파이썬 알고리즘 인터뷰_트라이

-----

<<[파이썬 알고리즘 인터뷰](https://book.naver.com/bookdb/book_detail.nhn?bid=16406247) 서적 내용을 정리>>

* [문제01 트라이 구현](#문제01-트라이-구현)
* [문제02 팰린드롬 페어](#문제02-팰린드롬-페어)

<br>

##### 문제01 트라이 구현

-----

> [https://leetcode.com/problems/implement-trie-prefix-tree](https://leetcode.com/problems/implement-trie-prefix-tree/)
>
> 트라이의 insert, search, startWith 메소드를 구현하라.
>
> **Example:**
>
> ```python
>Trie trie = new Trie();
> 
> trie.insert("apple");
> trie.search("apple");   // returns true
>    trie.search("app");     // returns false
>    trie.startsWith("app"); // returns true
>    trie.insert("app");   
>   trie.search("app");     // returns true
>  ```

<br>

* 풀이1_딕셔너리를 이용해 간결한 트라이 구현

```python
# 트라이의 노드
class TrieNode:
    def __init__(self):
        self.word = False
        self.children = collections.defaultdict(TrieNode)
        
class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = TrieNode()

    # 단어 삽입
    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        node = self.root
        for char in word:
            node = node.children[char]
        node.word = True
        
    # 단어 존재 여부 판별
    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
            
        return node.word
        
    # 문자열로 시작 단어 존재 여부 판별
    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
            
        return True
        


# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```

Result

>  Runtime : 196ms, Memory : 33.2MB

<br>

##### 문제02 팰린드롬 페어

-----

> [https://leetcode.com/problems/palindrome-pairs](https://leetcode.com/problems/palindrome-pairs/)
>
> 단어 리스트에서 words[i]  + words[j]가 팰린드롬이 되는 모든 인덱스 조합 (i, j)을 구하라.
>
> **Example 1:**
>
> ```python
> Input: words = ["abcd","dcba","lls","s","sssll"]
> Output: [[0,1],[1,0],[3,2],[2,4]]
> Explanation: The palindromes are ["dcbaabcd","abcddcba","slls","llssssll"]
> ```
>
> **Example 2:**
>
> ```python
> Input: words = ["bat","tab","cat"]
> Output: [[0,1],[1,0]]
> Explanation: The palindromes are ["battab","tabbat"]
> ```
>
> **Example 3:**
>
> ```python
> Input: words = ["a",""]
> Output: [[0,1],[1,0]]
> ```

<br>

* 풀이1_팰린드롬을 브루트 포스로 계산

```python
class Solution:
    def palindromePairs(self, words: List[str]) -> List[List[int]]:
        def is_palindrome(word):
            return word == word[::-1]
        
        output = []
        for i, word1 in enumerate(words):
            for j, word2 in enumerate(words):
                if i == j:
                    continue
                if is_palindrome(word1 + word2):
                    output.append([i, j])
        return output
        
```

Result

>  Time Limit Exceeded

<br>

* 풀이2_트라이 구현

```python
# 트라이를 저장할 노드
class TrieNode:
    def __init__(self):
        self.children = collections.defaultdict(TrieNode)
        self.word_id = -1
        self.palindrome_word_ids = []
        
class Trie:
    def __init__(self):
        self.root = TrieNode()

    @staticmethod
    def is_palindrome(word: str) -> bool:
        return word[::] == word[::-1]
    
    # 단어 삽입
    def insert(self, index, word) -> None:
        node = self.root
        for i, char in enumerate(reversed(word)):
            if self.is_palindrome(word[0:len(word) - i]):
                node.palindrome_word_ids.append(index)
            node = node.children[char]
        node.word_id = index
        
    def search(self, index, word) -> List[List[int]]:
        result = []
        node = self.root
        
        while word:
            # 판별 로직
            if node.word_id >= 0:
                if self.is_palindrome(word):
                    result.append([index, node.word_id])
            if not word[0] in node.children:
                return result
            node = node.children[word[0]]
            word = word[1:]
            
        # 판별 로직
        if node.word_id >= 0 and node.word_id != index:
            result.append([index, node.word_id])
            
        # 판별 로직
        for palindrome_word_id in node.palindrome_word_ids:
            result.append([index, palindrome_word_id])
            
        return result
    
class Solution:
    def palindromePairs(self, words: List[str]) -> List[List[int]]:
        trie = Trie()
        
        for i, word in enumerate(words):
            trie.insert(i, word)
            
        results = []
        for i, word in enumerate(words):
            results.extend(trie.search(i, word))
        
        return results
```

Result

>  Runtime : 976ms, Memory : 21.1MB

