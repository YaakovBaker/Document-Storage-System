<h1><a href = https://github.com/YaakovBaker/Document-Storage-System><Strong>Document Storage System</Strong></a></h1>

<h3><a id = "TOC">Table of Contents</a></h3>
<ul>
  <li><a href = "#Summary">Summary</a></li>
  <li><a href = "#DS">Data Structures</a></li>
    <p>
      <ul>
        <li><a href = "#Trie">Trie</a></li>
        <li><a href = "#MinHeap">MinHeap</a></li>
        <li><a href = "#Stack">Stack</a></li>
        <li><a href = "#BTree">BTree</a></li>
      </ul>
   </p>
 </ul>

<h3><a name = "Summary"><Strong>Summary</Strong></a></h3>
  <p><br>•	Built a Document Storage System with Java in Data Structures. It utilized various Data Structures we learned about in that course: Trie (searching), Stack (undo actions), Heap (last use time of a document), BTree (storage). The stored documents are instances of the <i>Document</i> and <i>DocumentImpl</i> classes and can be either text documents or documents of binary data. The <i>DocumentImpl</i> has multiple methods for returning specific and important information of the document like its wordCounts, the data stored, and its the last time it was used. The <i>DocumentPersistenceManager</i> class manipulates the state of these Documents by either serializing documents to the disk or deserializing them to bring them back to memory, and even deleting them when a deleteMethod is called. This is utilized by the Btree to manage its space in memory so that if the amount of documents exceed a set limit then instead of storing the document it will store a refrence to it on disk. Documents can be brought to memory when they are searched for by the Trie since their last use time will get updated and other documents can then be placed on disk to make space for this searched document.</p>
  
 <h3><a name = "DS" href = "https://github.com/YaakovBaker/Document-Storage-System/tree/main/stage5/src/main/java/edu/yu/cs/com1320/project">Data Structures</a></h3>
 <p><br>• This project used several data structures during its life time. Every new stage of the project incorporated a new data structure or replaced an old one, like how the Btree replaced the HashTable for storage. In this final stage of the project the data structures used were a Trie for searching, a Stack to undo actions, a Heap to keep track of the last use time of a document, and a BTree to store documents in memory and their refrences on disk.
  <ul type = "disc">
    <li><a name = "Trie" href = "https://github.com/YaakovBaker/Document-Storage-System/blob/main/stage5/src/main/java/edu/yu/cs/com1320/project/impl/TrieImpl.java"><b>TrieImpl.java</b></a></li>
    <p>•	A Trie is a search tree that is used for string searchs. A trie consists of nodes starting from the root where every node has one parent and many children nodes (links) stored in an array that is of a specified alphabet size. Each index in the array corresponds to a character value where a node is stored that corresponds to that character and within that node values may be stored like documents in our case, and another array of that nodes links. My <i>TrieImpl</i> offers put, delete, and search type of methods.
      <br>•	 The public <b>put()</b> method accepts a <b>String</b> key and <b>Document</b> value to store as one of that keys values for a later search. This put calls a private put that recursively traverses down the trie and adds absent links until it finally reaches the end of the key where it will store the document. 
      <br>•	The public <b>getAllSorted()</b> method accepts a <b>String</b> key and a <b>Comparator</b> to return all the documents stored within that key sorted in a <b>List</b>. This search method calls a private <b>get()</b> method to recursively traverse the trie to find the node corresponding to the provided key so that we can access the documents stored there to be returned. If the link is null or the values are null or the set containing them is empty then it returns an empty <b>List</b>. 
      <br>•	The public <b>getAllWithPrefixSorted()</b> method accepts a <b>String</b> prefix and a <b>Comparator</b> to return all the documents with that given prefix sorted in a <b>List</b>. This prefix search calls a private <b>getForPrefix()</b> method that recursively goes down the trie visiting every node with this prefix and storing all the documents found into a set.
      <br>•	The public <b>deleteAll()</b> method accepts a <b>String</b> key as an argument and calls the private <b>get()</b> method to find the node and put the values stored there in a <b>Set</b> to be returned, after which the private deleteAll is called recursively, starting with the root, to find the node and delete its values. If the subtrie rooted at that node is not empty then we will return our node to its parent, otherwise we will return null and remove the existence of this node.
      <br>•	The public <b>deleteAllWithPrefix()</b> method accepts a <b>String</b> prefix as an argument and calls the private <b>getForPrefix()</b> method to get the list of values that will be deleted and then calls the private <b>get()</b> to get the node that's subtrie's values will be deleted. If the subtrie rooted at every node visited is not empty then we will return that node to its parent, otherwise we will return null and remove the existence of that node.
      <br>•	The public <b>delete()</b> accepts a <b>String</b> key and <b>Document</b> value. It calles the private <b>get()</b> to get the node of that key and then loop though that node's values until it finds the value to delete and save it in a local variable. Then the private <b>delete()</b> is called starting at the root and recursively traversing the trie until the node is foudn and the specified value is deleted. Then if this node still has values return it otherwise see if any of its links exist, if they exist return this node otherwise return null to the parent.<br></p>
    <br>•	 There are more methods, but I found them too simple or not necessary to include explanations for here.<br></p>
    <li><a name = "MinHeap" href = "https://github.com/YaakovBaker/Document-Storage-System/blob/main/stage5/src/main/java/edu/yu/cs/com1320/project/impl/MinHeapImpl.java"><b>MinHeapImpl.java</b></a></li>
    <p>•	A MinHeap is a tree where keys are stored in an array and where parents must be smaller than its children. This MinHeap is of a binary heap representation. A heap is a complete tree as each level except possibly the lowestlevel is completely filled with nodes. If the bottom isn't completely filled, the nodes at the bottom will be filled up from the left. The height of a complete binary tree of size n is log(n). This data structure allows for efficient inserts and deletes.
      <br>•	 The protected <b>upHeap()</b> method accepts an index as an argument. While the key at that index is less than its parent's key, swap its contents with its parent’s.  
      <br>•	 The protected <b>downHeap()</b> method accepts an index as an argument. It then identifies which of its children are smaller and if it is greater than that child swap them and continue testing until our element is in the correct spot.
      <br>•	 The protected <b>getArrayIndex()</b> method accepts an element of generic type as an argument and searches for the index where that element is located. If no such element exists than a <b>NoSuchElementException</b> is thrown.
      <br>•	 The public <b>reHeapify</b> method accepts an element of generic type as an argument. If the heap is empty then it throws a <b>NoSuchElementException</b>, otherwise it calls the protected method <b>getArrayIndex()</b> to search for the index of this element. If the call on <b>hasParent()</b> returns true then it tests which is greater (the element or its parent). If it returns true then it calls <b>downHeap()</b> otherwise it calls <b>upHeap()</b>. If the call on <b>hasParent()</b> returns false then it checks to see if the element has children, and if it does <b>upHeap()</b> is called, otherwise <b>downHeap()</b> is called.
      <br>•	 The public <b>insert()</b> method accepts an element of generic type as an argument. If the number of elements is greater than or equal to the size of the array minus one than the protected <b>doubleArraySize()</b> method is called. The element is then inserted at the bottom of the heap and <b>upHeap()</b> is called to maintain the MinHeap properties.
      <br>•	 The public <b>remove()</b> method throws a <b>NoSuchElementException</b> if the heap is empty, otherwise it saves the minimum value to be deleted in a local variable and calls swap on index 1, its location, and the element at the bottom of the heap and decrement the count of elements. <b>downHeap()</b> is then called to maintain heap properties and then the location where the to be deleted element is at is set to null.
      <br>•	 There are more methods, but I found them too simple or not necessary to include explanations for here.<br></p>
    <li><a name = "Stack" href = "https://github.com/YaakovBaker/Document-Storage-System/blob/main/stage5/src/main/java/edu/yu/cs/com1320/project/impl/StackImpl.java"><b>StackImpl.java</b></a></li>
    <p>•	A Stack stores a sequence of values in LIFO order (Last-In, First-Out). The top of the stack is where operations occur. If you want to do more than just the operations on the top of the stack then that is up to client code you create to use the operations of the stack with extra logic you include in your client code to do what you want. I implement my Stack to work like a linked list. The elements of the Stack are a <b>StackEntry</b> that contains a pointer to the next element in the stack and the data being stored. The Stack data structure itself contains a pointer to the entry at the top.
      <br>•	 The public <b>push()</b> method accepts an element of a generic type. If it is null then an <b>IllegalArgumentException()</b> is thrown, otherwise a new <b>Stackentry</b> is created and passed that element to store it. It's next link becomes what is currently the top and then replaces it as the new top.
      <br>•	 The public <b>pop()</b> method returns the element at the top of the stack and removes it. If the stack is empty then null is returned, otherwise the data stored in the top <b>StackEntry</b> is stored into a local variable, the top pointer points to the top <b>StackEntry's</b> next <b>StackEntry</b> as to remove any refrence to the previous top of the stack and then that local variable is returned.
      <br>•	 The public <b>peek()</b> method returns the element stored in the top <b>Stackentry</b> without removing them, but if the stack is empty null is returned instead.
      <br>•	 There are more methods, but I found them too simple or not necessary to include explanations for here.<br></p>
    <li><a name = "BTree" href = "https://github.com/YaakovBaker/Document-Storage-System/blob/main/stage5/src/main/java/edu/yu/cs/com1320/project/impl/BTreeImpl.java"><b>BTreeImpl.java</b></a></li>
    <p>•	A BTree is a balanced-tree that supports external search in symbol tables that are kept on a disk or on the web. The tree consists of nodes that contain an array of <b>Entry</b> elements. Each <b>Node</b> object in my implementation has an even number m sized array, in my case 6, and allows for m-1 key-link pairs and at least m/2 key-link pairs except the root which can have at least 2. It also contains a count of how many entries are in that node as well as pointers to the next and previous node. Each <b>Entry</b> object contains a <b>Comparable/b> key, <b>Object</b> value, child <b>Node</b> and a boolean set to true if this is on disk and false if it's in memory. My BTree holds a few instance variables such as the root <b>Node</b>, the left most external <b>Node</b>, the height of the BTree, the number of key-value pairs in the BTree, and an instance of the <i>PersistenceManager</i> object.
      <br>•	 The private <b>split()</b> method accepts the current <b>Node</b> to be split and an int height as arguments. It returns a new <b>Node</b> created by the split. It first constructs a new <b>Node</b> with an entryCount half the size of MAX, and sets the current <b>Node</b>'s entry count to that same number. It then copies the top half of the current <b>Node</b>'s entries to the new <b>Node</b>. Then if the height was 0, meaning an external <b>Node</b>, it sets the new <b>Node</b>'s next to the current's next, the new <b>Node</b>'s previous to be the current <b>Node</b>, and the current <b>Node</b>'s next to the new <b>Node</b>.  
      <br>•	 The private <b>entryShiftAndSplit</b> method 
      <br>•	 The public <b>put()</b> method
      <br>•	 The public <b>get()</b> method accepts a Key as an argument. If that key is null then an <b>IllegalArgumentException()</b> is thrown, otherwise it calls the private <b>get()</b> which recursively, starting with the root <b>Node</b> and an int containing the height of the tree, checks if our current height is equal to 0, meaning we are at an external <b>Node</b>. If the height is not zero then we iterate through the current node's entries and if we are at the last key in this node or the key we are looking for is less than the next key, i.e. the desired key must be in the subtree below the current entry, then recurse into the current entry’s child node until we reach the height of 0. A null value is returned if an <b>Entry</b> corresponding to the given key is not found. Then back in the public <b>get()</b> if the <b>Entry</b> is not null then we check if it is on disk. If it is on disk we try to deserialize it by calling the <i>PersistenceManager</i>'s <b>deserialize()</b> method and set the entris on disk variable to false. After which we return the value stored at that <b>Entry</b>. If the <b>Entry</b> returned by the private <b>get()</b> was null then we return null as the value.
      <br>•	 The public <b>moveToDisk()</b> method accepts a Key as an argument and calls the private <b>get()</b> to get the <b>Entry</b> of that key. If the <b>Entry</b> is not null and is in on disk is false then the value stored in the <b>Entry</b> is stored in a local variable. If the value is not null then the <b>Entry</b>'s value instance variable is set to null, the <b>Entry</b> is marked on disk, and the <i>PersistenceManager</i>'s <b>serialize()</b> method is called to serialize the key-value pair.
      <br>•	 The public <b>setPersistenceManager()</b> method sets the private <i>PersistenceManager</i> instance variable. This is called by the client code.
      <br>•	 There are more methods, but I found them too simple or not necessary to include explanations for here.<br></p>
    </ul>
 
<a href ="#TOC">Back To Top</a>
