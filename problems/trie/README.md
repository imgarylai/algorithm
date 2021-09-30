# Trie 字典樹

`Trie` 是利用 `Hash Table` 的優勢所衍伸出的一種資料格式，很常被應用在[**物件導向程式設計**](../object-oriented-design/)的題目，因為，而且題目通常不會給出任何可以使用出 Trie 的提示，所以通常都會需要自己去建立 `TrieNode` 這個物件，並且題目很常會需要在 Trie 的節點上去記錄一些資訊。

這些資訊很重要是因為，`Trie` 的遍歷是一般而言依靠著 `DFS` 在執行的，這些記錄在 `TrieNode` 上的資訊有助於我們快速查找到答案，或是減少搜索的空間。

最簡單可以上手的題目是從 [208. Implement Trie \(Prefix Tree\)](implement-trie-prefix-tree.md) 開始

