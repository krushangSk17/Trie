# Trie

```python
class TrieNode:
    def __init__(self) -> None:
        self.children = {}
        self.is_end = False
        self.number_of_children = 0  # This counts how many words have been inserted that pass through or terminate here

class Trie:

    def __init__(self) -> None:
        self.root = TrieNode()

    def insert(self, word):
        node = self.root
        for w in word:
            node.number_of_children += 1
            if w not in node.children:
                node.children[w] = TrieNode()  # Create new TrieNode if the character doesn't exist
            node = node.children[w]  # Increment for every word passing through or ending at this node
        node.is_end = True

    def search(self, word):
        node = self.root
        for w in word:
            if w not in node.children:
                return False
            node = node.children[w]
        return node.is_end

    def starts_with(self, word):
        node = self.root
        for w in word:
            if w not in node.children:
                return False
            node = node.children[w]
        return True

    def get_leaf_count(self, prefix):
        """ Returns the number of leaf nodes (words) starting with the given prefix. """
        node = self.root
        for w in prefix:
            if w not in node.children:
                return 0  # Prefix not found
            node = node.children[w]
        return node.number_of_children  # Return the count of words that pass through or end at this node
