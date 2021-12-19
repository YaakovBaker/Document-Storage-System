<h1><a href = https://github.com/YaakovBaker/Document-Storage-System><Strong>Document Storage System</Strong></a></h1>

<h3>Summary</Strong></h3>
  <p><br>•	Built a Document Storage System with Java in Data Structures. It utilized various Data Structures we learned about in that course: Trie (searching), Stack (undo actions), Heap (last use time of a document), BTree (storage). The stored documents are instances of the <i>Document</i> and <i>DocumentImpl</i> classes and can be either text documents or documents of binary data. The <i>DocumentImpl</i> has multiple methods for returning specific and important information of the document like its wordCounts, the data stored, and its the last time it was used. The <i>DocumentPersistenceManager</i> class manipulates the state of these Documents by either serializing documents to the disk or deserializing them to bring them back to memory, and even deleting them when a deleteMethod is called. This is utilized by the Btree to manage its space in memory so that if the amount of documents exceed a set limit then instead of storing the document it will store a refrence to it on disk. Documents can be brought to memory when they are searched for by the Trie since their last use time will get updated and other documents can then be placed on disk to make space for this searched document.</p>
  
 <h3>Data Structures</h3>
 <p><br>• This project used several data structures during its life time. Every new stage of the project incorporated a new data structure or replaced an old one, like how the Btree replaced the HashTable for storage. In this final stage of the project the data structures used were a Trie for searching, a Stack to undo actions, a Heap to keep track of the last use time of a document, and a BTree to store documents in memory and their refrences on disk.
  <ul type = "disc">
    <li><a href = "https://github.com/YaakovBaker/Document-Storage-System/blob/main/stage5/src/main/java/edu/yu/cs/com1320/project/impl/TrieImpl.java"><b>TrieImpl.java</b></a></li>
    <li><a href = "https://github.com/YaakovBaker/Document-Storage-System/blob/main/stage5/src/main/java/edu/yu/cs/com1320/project/impl/MinHeapImpl.java"><b>MinHeapImpl.java</b></a></li>
    <li><a href = "https://github.com/YaakovBaker/Document-Storage-System/blob/main/stage5/src/main/java/edu/yu/cs/com1320/project/impl/StackImpl.java"><b>StackImpl.java</b></a></li>
    <li><a href = "https://github.com/YaakovBaker/Document-Storage-System/blob/main/stage5/src/main/java/edu/yu/cs/com1320/project/impl/BTreeImpl.java"><b>BTreeImpl.java</b></a></li>
    </ul>
 
