---
title: Trie
date: 2021-04-14 21:09:47
tags: leetcode刷题记录
categories: 数据结构

---

### 前缀树
<!--more-->
## Trie
* Trie树，即前缀树，又称单词查找树，字典树，是一种树形结构，是一种哈希树的变种。典型应用是用于统计和排序大量的字符串（但不仅限于字符串），所以经常被搜索引擎系统用于文本词频统计。
* Trie树的核心思想是空间换时间，利用字符串的公共前缀来降低查询时间的开销以达到提高效率的目的。 它的优点是：最大限度地减少无谓的字符串比较，查询效率比哈希表高。
* 模板题<https://leetcode-cn.com/problems/implement-trie-prefix-tree/>
```c++
//prefix 前缀
class Trie {
private:
    vector<Trie*> children;
    bool isEnd;

    Trie* searchPrefix(string prefix)
    {
        Trie* node = this;
        for (char ch : prefix) {
            ch -= 'a';
            if (node->children[ch] == nullptr) {
                return nullptr;
            }
            node = node->children[ch];
        }
        return node;
    }
public:
    Trie(): children(26), isEnd(false) { }

    void insert(string word)
    {
        Trie* node = this;
        for (char ch : word) {
            ch -= 'a';
            if (node->children[ch]==nullptr) {
                node->children[ch] = new Trie();
            }
            node = node->children[ch];
        }
        node->isEnd = true;
    }
    //如果字符串 word 在前缀树中，返回 true（即，在检索之前已经插入）；否则，返回 false 。
    bool search(string word) {
        Trie* node = this->searchPrefix(word);
        return node != nullptr && node->isEnd;
    }
    //如果之前已经插入的字符串 word 的前缀之一为 prefix ，返回 true ；否则，返回 false 。
    bool startsWith(string prefix) {
        return this->searchPrefix(prefix) != nullptr;
    }
};
```
