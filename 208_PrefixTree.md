## LeetCode  208 前缀树
设计
medium

### 描述
实现一个 Trie (前缀树)，包含 insert, search, 和 startsWith 这三个操作。

示例:

Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // 返回 true
trie.search("app");     // 返回 false
trie.startsWith("app"); // 返回 true
trie.insert("app");   
trie.search("app");     // 返回 true
说明:

你可以假设所有的输入都是由小写字母 a-z 构成的。
保证所有输入均为非空字符串。

### 解答
前缀树可以理解为字典连接的字典。我第一次做的时候没有考虑到每个节点还需要有一个判断当前是否为单词的
布尔量，自己定义树节点的数据结构，然后构建前缀树即可。
注意字典可以用 Python 的`defaultdict`，这样就不用再判断键是否存在了。

```Python
class TreeNode:
    def __init__(self):
        self.dict = collections.defaultdict(TreeNode)
        self.is_word = False
        
class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = TreeNode()

    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        cur = self.root
        for letter in word:
            cur = cur.dict[letter]
        cur.is_word = True
        

    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        cur = self.root
        for letter in word:
            cur = cur.dict.get(letter)
            if not cur: return False
        return cur.is_word

    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        cur = self.root
        for letter in prefix:
            cur = cur.dict.get(letter)
            if not cur: return False
        return True
```

