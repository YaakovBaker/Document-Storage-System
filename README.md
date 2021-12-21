<h1><a id = "TOP" href = https://github.com/YaakovBaker/Document-Storage-System><Strong>Document Storage System</Strong></a></h1>

<h3><a id = "TOC">Table of Contents</a></h3>
<ul>
  <li><a href = "https://www.linkedin.com/in/yaakovbaker01/">Link to visit my LinkedIn</a></li>
  <li><a href = "#Summary">Summary</a></li>
  <li><a href = "#DS">Data Structures</a></li>
    <p>
      <ul>
        <li><a href = "#Trie">Trie</a></li>
          <p>
            <ul>
              <li><a href = "#Description-Trie">Description</a></li>
              <li><a href = "#put-Trie">put</a></li>
              <li><a href = "#getAllSorted-Trie">getAllSorted</a></li>
              <li><a href = "#getAllWithPrefixSorted-Trie">getAllWithPrefixSorted</a></li>
              <li><a href = "#deleteAll-Trie">deleteAll</a></li>
              <li><a href = "#deleteAllWithPrefix-Trie">deleteAllWithPrefix</a></li>
              <li><a href = "#delete-Trie">delete</a></li>
            </ul>
          </p>
        <li><a href = "#MinHeap">MinHeap</a></li>
          <p>
            <ul>
              <li><a href = "#Description-MinHeap">Description</a></li>
              <li><a href = "#upHeap-MinHeap">upHeap</a></li>
              <li><a href = "#downHeap-MinHeap">downHeap</a></li>
              <li><a href = "#getArrayIndex-MinHeap">getArrayIndex</a></li>
              <li><a href = "#reHeapify-MinHeap">reHeapify</a></li>
              <li><a href = "#insert-MinHeap">insert</a></li>
              <li><a href = "#remove-MinHeap">remove</a></li>
            </ul>
          </p>
        <li><a href = "#Stack">Stack</a></li>
          <p>
            <ul>
              <li><a href = "#Description-Stack">Description</a></li>
              <li><a href = "#push-Stack">push</a></li>
              <li><a href = "#pop-Stack">pop</a></li>
              <li><a href = "#peek-Stack">peek</a></li>
            </ul>
          </p>
        <li><a href = "#BTree">BTree</a></li>
          <p>
            <ul>
              <li><a href = "#Description-BTree">Description</a></li>
              <li><a href = "#split-BTree">split</a></li>
              <li><a href = "#entryShiftAndSplit-BTree">entryShiftAndSplit</a></li>
              <li><a href = "#entryExists-BTree">entryExists</a></li>
              <li><a href = "#get-BTree">get</a></li>
              <li><a href = "#put-BTree">put</a></li>
              <li><a href = "#moveToDisk-BTree">moveToDisk</a></li>
              <li><a href = "#setPersistenceManager-BTree">setPersistenceManager</a></li>
            </ul>
          </p>
      </ul>
   </p>
 </ul>

<h3><a name = "Summary"><Strong>Summary</Strong></a></h3>
  <p><br>•	Built a Document Storage System with Java in Data Structures. It utilized various Data Structures we learned about in that course: Trie (searching), Stack (undo actions), Heap (last use time of a document), BTree (storage). The stored documents are instances of the <i>Document</i> and <i>DocumentImpl</i> classes and can be either text documents or documents of binary data. The <i>DocumentImpl</i> has multiple methods for returning specific and important information of the document like its wordCounts, the data stored, and its the last time it was used. The <i>DocumentPersistenceManager</i> class manipulates the state of these Documents by either serializing documents to the disk or deserializing them to bring them back to memory, and even deleting them when a deleteMethod is called. This is utilized by the Btree to manage its space in memory so that if the amount of documents exceed a set limit then instead of storing the document it will store a refrence to it on disk. Documents can be brought to memory when they are searched for by the Trie since their last use time will get updated and other documents can then be placed on disk to make space for this searched document.</p>
  
 <h3><a name = "DS" href = "https://github.com/YaakovBaker/Document-Storage-System/tree/main/stage5/src/main/java/edu/yu/cs/com1320/project">Data Structures</a></h3>
 <p><br>• This project used several data structures during its life time. Every new stage of the project incorporated a new data structure or replaced an old one, like how the Btree replaced the HashTable for storage. In this final stage of the project the data structures used were a Trie for searching, a Stack to undo actions, a Heap to keep track of the last use time of a document, and a BTree to store documents in memory and their refrences on disk.
  <ul type = "disc">
    <li><a name = "Trie" href = "https://github.com/YaakovBaker/Document-Storage-System/blob/main/stage5/src/main/java/edu/yu/cs/com1320/project/impl/TrieImpl.java"><b>TrieImpl.java</b></a></li>
    <p>•	<a name = "Description-Trie">A Trie</a> is a search tree that is used for string searchs. A trie consists of nodes starting from the root where every node has one parent and many children nodes (links) stored in an array that is of a specified alphabet size. Each index in the array corresponds to a character value where a node is stored that corresponds to that character and within that node values may be stored like documents in our case, and another array of that nodes links. My <i>TrieImpl</i> offers put, delete, and search type of methods.
      <br>•	 The public <a name = "put-Trie"><b>put()</b></a> method accepts a <b>String</b> key and <b>Document</b> value to store as one of that keys values for a later search. This put calls a private put that recursively traverses down the trie and adds absent links until it finally reaches the end of the key where it will store the document. 
      <br>•	The public <a name = "getAllSorted-Trie"><b>getAllSorted()</b></a> method accepts a <b>String</b> key and a <b>Comparator</b> to return all the documents stored within that key sorted in a <b>List</b>. This search method calls a private <b>get()</b> method to recursively traverse the trie to find the node corresponding to the provided key so that we can access the documents stored there to be returned. If the link is null or the values are null or the set containing them is empty then it returns an empty <b>List</b>. 
      <br>•	The public <a name = "getAllWithPrefixSorted-Trie"><b>getAllWithPrefixSorted()</b></a> method accepts a <b>String</b> prefix and a <b>Comparator</b> to return all the documents with that given prefix sorted in a <b>List</b>. This prefix search calls a private <b>getForPrefix()</b> method that recursively goes down the trie visiting every node with this prefix and storing all the documents found into a set.
      <br>•	The public <a name = "deleteAll-Trie"><b>deleteAll()</b></a> method accepts a <b>String</b> key as an argument and calls the private <b>get()</b> method to find the node and put the values stored there in a <b>Set</b> to be returned, after which the private deleteAll is called recursively, starting with the root, to find the node and delete its values. If the subtrie rooted at that node is not empty then we will return our node to its parent, otherwise we will return null and remove the existence of this node.
      <br>•	The public <a name = "deleteAllWithPrefix-Trie"><b>deleteAllWithPrefix()</b></a> method accepts a <b>String</b> prefix as an argument and calls the private <b>getForPrefix()</b> method to get the list of values that will be deleted and then calls the private <b>get()</b> to get the node that's subtrie's values will be deleted. If the subtrie rooted at every node visited is not empty then we will return that node to its parent, otherwise we will return null and remove the existence of that node.
      <br>•	The public <a name = "delete-Trie"><b>delete()</b></a> accepts a <b>String</b> key and <b>Document</b> value. It calles the private <b>get()</b> to get the node of that key and then loop though that node's values until it finds the value to delete and save it in a local variable. Then the private <b>delete()</b> is called starting at the root and recursively traversing the trie until the node is foudn and the specified value is deleted. Then if this node still has values return it otherwise see if any of its links exist, if they exist return this node otherwise return null to the parent.
    <br>•	 There are more methods, but I found them too simple or not necessary to include explanations for here.<br></p>
    <li><a name = "MinHeap" href = "https://github.com/YaakovBaker/Document-Storage-System/blob/main/stage5/src/main/java/edu/yu/cs/com1320/project/impl/MinHeapImpl.java"><b>MinHeapImpl.java</b></a></li>
    <p>•	<a name = "Description-MinHeap">A MinHeap</a> is a tree where keys are stored in an array and where parents must be smaller than its children. This MinHeap is of a binary heap representation. A heap is a complete tree as each level except possibly the lowestlevel is completely filled with nodes. If the bottom isn't completely filled, the nodes at the bottom will be filled up from the left. The height of a complete binary tree of size n is log(n). This data structure allows for efficient inserts and deletes.
      <br>•	 The protected <a name = "upHeap-MinHeap"><b>upHeap()</b></a> method accepts an index as an argument. While the key at that index is less than its parent's key, swap its contents with its parent’s.  
      <br>•	 The protected <a name = "downHeap-MinHeap"><b>downHeap()</b></a> method accepts an index as an argument. It then identifies which of its children are smaller and if it is greater than that child swap them and continue testing until our element is in the correct spot.
      <br>•	 The protected <a name = "getArrayIndex-MinHeap"><b>getArrayIndex()</b></a> method accepts an element of generic type as an argument and searches for the index where that element is located. If no such element exists than a <b>NoSuchElementException</b> is thrown.
      <br>•	 The public <a name = "reHeapify-MinHeap"><b>reHeapify</b></a> method accepts an element of generic type as an argument. If the heap is empty then it throws a <b>NoSuchElementException</b>, otherwise it calls the protected method <b>getArrayIndex()</b> to search for the index of this element. If the call on <b>hasParent()</b> returns true then it tests which is greater (the element or its parent). If it returns true then it calls <b>downHeap()</b> otherwise it calls <b>upHeap()</b>. If the call on <b>hasParent()</b> returns false then it checks to see if the element has children, and if it does <b>upHeap()</b> is called, otherwise <b>downHeap()</b> is called.
      <br>•	 The public <a name = "insert-MinHeap"><b>insert()</b></a> method accepts an element of generic type as an argument. If the number of elements is greater than or equal to the size of the array minus one than the protected <b>doubleArraySize()</b> method is called. The element is then inserted at the bottom of the heap and <b>upHeap()</b> is called to maintain the MinHeap properties.
      <br>•	 The public <a name = "remove-MinHeap"><b>remove()</b></a> method throws a <b>NoSuchElementException</b> if the heap is empty, otherwise it saves the minimum value to be deleted in a local variable and calls swap on index 1, its location, and the element at the bottom of the heap and decrement the count of elements. <b>downHeap()</b> is then called to maintain heap properties and then the location where the to be deleted element is at is set to null.
      <br>•	 There are more methods, but I found them too simple or not necessary to include explanations for here.<br></p>
    <li><a name = "Stack" href = "https://github.com/YaakovBaker/Document-Storage-System/blob/main/stage5/src/main/java/edu/yu/cs/com1320/project/impl/StackImpl.java"><b>StackImpl.java</b></a></li>
    <p>•	<a name = "Description-Stack">A Stack</a> stores a sequence of values in LIFO order (Last-In, First-Out). The top of the stack is where operations occur. If you want to do more than just the operations on the top of the stack then that is up to client code you create to use the operations of the stack with extra logic you include in your client code to do what you want. I implement my Stack to work like a linked list. The elements of the Stack are a <b>StackEntry</b> that contains a pointer to the next element in the stack and the data being stored. The Stack data structure itself contains a pointer to the entry at the top.
      <br>•	 The public <a name = "push-Stack"><b>push()</b></a> method accepts an element of a generic type. If it is null then an <b>IllegalArgumentException()</b> is thrown, otherwise a new <b>Stackentry</b> is created and passed that element to store it. It's next link becomes what is currently the top and then replaces it as the new top.
      <br>•	 The public <a name = "pop-Stack"><b>pop()</b></a> method returns the element at the top of the stack and removes it. If the stack is empty then null is returned, otherwise the data stored in the top <b>StackEntry</b> is stored into a local variable, the top pointer points to the top <b>StackEntry's</b> next <b>StackEntry</b> as to remove any refrence to the previous top of the stack and then that local variable is returned.
      <br>•	 The public <a name = "peek-Stack"><b>peek()</b></a> method returns the element stored in the top <b>Stackentry</b> without removing them, but if the stack is empty null is returned instead.
      <br>•	 There are more methods, but I found them too simple or not necessary to include explanations for here.<br></p>
    <li><a name = "BTree" href = "https://github.com/YaakovBaker/Document-Storage-System/blob/main/stage5/src/main/java/edu/yu/cs/com1320/project/impl/BTreeImpl.java"><b>BTreeImpl.java</b></a></li>
    <p>•	<a name = "Description-BTree">A BTree</a> is a balanced-tree that supports external search in symbol tables that are kept on a disk or on the web. The tree consists of nodes that contain an array of <b>Entry</b> elements. Each <b>Node</b> object in my implementation has an even number m sized array, in my case 6, and allows for m-1 key-link pairs and at least m/2 key-link pairs except the root which can have at least 2. It also contains a count of how many entries are in that node as well as pointers to the next and previous node. Each <b>Entry</b> object contains a <b>Comparable/b> key, <b>Object</b> value, child <b>Node</b> and a boolean set to true if this is on disk and false if it's in memory. My BTree holds a few instance variables such as the root <b>Node</b>, the left most external <b>Node</b>, the height of the BTree, the number of key-value pairs in the BTree, and an instance of the <i>PersistenceManager</i> object.
      <br>•	 The private <a name = "split-BTree"><b>split()</b></a> method accepts the current <b>Node</b> to be split and an int height as arguments. It returns a new <b>Node</b> created by the split. It first constructs a new <b>Node</b> with an entryCount half the size of MAX, and sets the current <b>Node</b>'s entry count to that same number. It then copies the top half of the current <b>Node</b>'s entries to the new <b>Node</b>. Then if the height was 0, meaning an external <b>Node</b>, it sets the new <b>Node</b>'s next to the current's next, the new <b>Node</b>'s previous to be the current <b>Node</b>, and the current <b>Node</b>'s next to the new <b>Node</b>.  
      <br>•	 The private <a name = "entryShiftAndSplit-BTree"><b>entryShiftAndSplit()</b></a> method accepts a new <b>Entry</b>, an int index to place that entry into the current <b>Node</b>, and the int height. First the method shifts the entries in the current <b>Node</b> starting from the last <b>Entry</b> until the index for our new <b>Entry</b> and then places the new <b>Entry</b> into its location in the entries array of that <b>Node</b> and increments the count of entries in that <b>Node</b>. If the current number of entries is less than 6 then we return null as we don't need to do anything else, otherwise we have to call <b>split()</b> to split the <b>Node</b> and return the new <b>Node</b> that <b>split()</b> returns. 
      <br>•	 The private <a name = "entryExists-BTree"><b>entryExists()</b></a> method is called by <b>put()</b> if the <b>Entry</b> already exists in the BTree and it will be updating that <b>Entry</b>'s value. This method accepts the already existant <b>Entry</b>, Key, and Value as arguments. If the entry is on disk then it tries calling <i>PersistenceManager</i>'s <b>deserialize()</b> method and storing the Value returned locally and setting the existant <b>Entry</b>'s Value to that returned Value, otherwise if it is in memory and the existant <b>Entry</b>'s value is null then it stores the new Value into that existant <b>Entry</b> and returns null since there wasn't a Value already stored there. In the case of deserializing and if it was in memory, but not null then it locally stores the old Value of that <b>Entry</b>, updated its value to the new one, sets its status to be in memory, and returns the old Value. 
      <br>•	 The public <a name = "get-BTree"><b>get()</b></a> method accepts a Key as an argument. If that key is null then an <b>IllegalArgumentException()</b> is thrown, otherwise it calls the private <b>get()</b> which recursively, starting with the root <b>Node</b> and an int containing the height of the tree, checks if our current height is equal to 0, meaning we are at an external <b>Node</b>. If the height is not zero then we iterate through the current node's entries and if we are at the last key in this node or the key we are looking for is less than the next key, i.e. the desired key must be in the subtree below the current entry, then recurse into the current entry’s child node until we reach the height of 0. A null value is returned if an <b>Entry</b> corresponding to the given key is not found. Then back in the public <b>get()</b> if the <b>Entry</b> is not null then we check if it is on disk. If it is on disk we try to deserialize it by calling the <i>PersistenceManager</i>'s <b>deserialize()</b> method and set the entries on disk variable to false. After which we return the value stored at that <b>Entry</b>. If the <b>Entry</b> returned by the private <b>get()</b> was null then we return null as the value.
      <br>•	 The public <a name = "put-BTree"><b>put()</b></a> method accepts a Key and Value as arguments. If that key is null then an <b>IllegalArgumentException()</b> is thrown, otherwise it calls the private <b>get()</b> to see if it already exists. The <b>Entry</b> returned (null or not) is stored in a local <b>Entry</b> variable. If it is not null then the <b>entryExists()</b> method is called. If it is null then we call the private <b>put()</b> which returns a new <b>Node</b> and store it in a local variable. The private <b>put()</b> accepts a <b>Node</b>, Key, Value, and int height as arguments. It begins by creating a new <b>Entry</b> for that key-value pair. Then if the height is 0 it iterates through the current <b>Node</b>'s entries to find the index that the new <b>Entry</b> should be placed at, break out of the loop, and then call <b>entryShiftAndSplit()</b>. If the height is not 0 then it iterates through the current internal <b>Node</b>'s entries for the index to place into, then if it has reached the last key in this <b>Node</b> or the key that it's looking for is less than the next key, i.e. the desired key must be added to the subtree below the current <b>Entry</b>, then do a recursive call to <b>put</b> on the current <b>Entry</b>’s child. If the recursive call to <b>put()</b> returns null then null is returned to the public <b>put()</b> signifying that a new <b>Entry</b> was added, but a new <b>Node</b> was not created. If the recursive call to <b>put()</b> returns a <b>Node</b> then the new <b>Entry</b> is added to the <b>Node</b>. Afterwards <b>entryShiftAndSplit()</b> is called with the result of that being returned to the public <b>put()</b>. If the returned <b>Node</b> is null then null is returned to the client, otherwise split the root by creating a new <b>Node</b> to be the root, set the old root to be the new root's first <b>Entry</b>, and set the <b>Node</b> returned from the call to put to be the new root's second <b>Entry</b>. Then increase the height counter since a new root was created, and return null as the <b>Entry</b> is new and doesn't have an old value to return. 
      <br>•	 The public <a name = "moveToDisk-BTree"><b>moveToDisk()</b></a> method accepts a Key as an argument and calls the private <b>get()</b> to get the <b>Entry</b> of that key. If the <b>Entry</b> is not null and is in on disk is false then the value stored in the <b>Entry</b> is stored in a local variable. If the value is not null then the <b>Entry</b>'s value instance variable is set to null, the <b>Entry</b></a> is marked on disk, and the <i>PersistenceManager</i>'s <b>serialize()</b> method is called to serialize the key-value pair.
      <br>•	 The public <a name = "setPersistenceManager-BTree"><b>setPersistenceManager()</b> method sets the private <i>PersistenceManager</i> instance variable. This is called by the client code.
      <br>•	 There are more methods, but I found them too simple or not necessary to include explanations for here.<br></p>
    </ul>
 </p>
 <p>
<a href ="#TOP">Back To Top</a><br>
<a href = "https://www.linkedin.com/in/yaakovbaker01/">LinkedIn</a>
 </p>
