Download Link: https://assignmentchef.com/product/solved-coms228-assignment5-video-store-transactions
<br>
In this project, you will implement a self-adjusting binary search tree called the splay tree. It carries out selfoptimization based on the heuristic that recently accessed elements are quick to access again. With <em>n</em> nodes, the tree has the amortized running time of <em>O(logn)</em> per operation. (This is the time averaged over a worst-case sequence of operations.) Next, you will use a splay tree to simulate customer rental and return transactions at a video store.

The class <em>SplayTree</em> implements the data structure of splay tree. The class <em>Video</em> represents a video with rental information, while the class <em>VideoStore</em> makes use of a <em>SplayTree</em> object to simulate video transactions. You also need to implement the class <em>Transactions</em> to simulate video rental and return activities. To these four classes you may add new instance variables and methods. You cannot, however, rename or remove any existing ones, or change any from public to protected (or private), or vice versa.

<h1>1.  Splay Tree</h1>

The <em>SplayTree</em> class has been completed for you. You <strong>do not</strong> need to implement <em>SplayTree</em>.

If you would like to learn more about the inner workings of splay trees, please refer to the provided code, the included javadocs, and the attached <em>splayTrees.pptx</em>. A description of parts of the the classes functionality follows.

The splay tree is implemented by the following generic class:

<em>public class SplayTree&lt;E extends Comparable&lt;? super E&gt;&gt; extends AbstractSet&lt;E&gt; </em>A node in the tree is fully implemented by the public class Node within <em>SplayTree</em>.

<h2>1.1  Tree Construction, Methods, and Iterator</h2>

Three constructors are provided for the SplayTree class: <em>public SplayTree() public SplayTree(E data) public SplayTree(SplayTree&lt;E&gt; tree)</em>

The first constructor creates an empty tree (with <em>null</em> root).

The second constructor merely creates a tree root to store given data. The rest of the tree needs to be constructed by repeatedly calling the following method which performs a binary search tree addition: <em>public boolean addBST(E data)</em>

For efficiency of tree initialization, the method does not splay at the newly created node.

The third constructor copies over the structure of an existing splay tree.

The class has a private iterator class <em>SplayTreeIterator</em>. <strong>No iterator method splays</strong> at a node.

<h2>1.2  Tree Display</h2>

The <em>toString()</em> method has been overridden to display the configuration of the splay tree under the following rules:

Every node of the tree occupies a separate line with its data written out only. (Assume that the <em>toString() </em>method for the data class <em>E</em> has been properly overridden.)

The data stored at a node at depth <em>d</em> is printed with indentation <em>4d</em> (i.e., preceded by <em>4d</em> blanks). Starting at the root (at depth 0), it displays the nodes in a preorder traversal. More specifically, suppose a node <em>n</em> is shown at line <em>l</em>. Then, starting at line <em>l+1</em> , it recursively prints all nodes in the left subtree (if any) of <em>n</em>; recursively prints all nodes in the right subtree (if any) of <em>n</em>.

If a node has a left child but no right child, prints its right child as null.

If a node has a right child but no left child, prints its left child as null.

If a node is a leaf, it is printed with no further recursion.

The <em>toString()</em> method for the class E is assumed to be properly overridden. Shown next is a splay tree with 12 nodes to store integers (<em>E</em> instantiated as <em>int</em>). What follows is the expected output that would be generated from calling the <em>toString()</em> and <em>System.out.println()</em>.

<h1>2.  Video Store</h1>

The class <em>VideoStore</em> simulates rental and return transactions at a video store. Videos are objects of the Video class such that a <strong>single</strong> Video object represents all video copies of the same film.

Suppose the store keeps one copy of the film <em>The Godfather</em>. Then, a constructor call <em>Video(“The Godfather”, 1) </em>will create an entry to be put on the store’s inventory. Videos are compared <strong>by film title</strong> in the alphabetical order.

<h2>2.1  Inventory</h2>

The class VideoStore employs one splay tree to store its inventory: <em>protected SplayTree&lt;Video&gt; inventory;</em>

Every node in the tree is an object of the Node class.

<h2>2.2  Constructors and Video File</h2>

Two constructors are provided for the class:

<em>public VideoStore() public VideoStore(String videoFile) throws FileNotFoundException</em>

The default constructor initializes the inventory to be an empty splay tree. It is expected to later call the method <em>setUpInventory()</em> to complete the inventory construction.

The second constructor builds inventory over a <em>video file</em>. Each line of the file lists a film title followed by one or more blanks and then the number of video copies within a pair of parentheses.

<ol>

 <li>A negative number following a film title is treated as zero.</li>

 <li>If a line has a film title only, then the number of copies defaults to one.</li>

 <li>A film <strong>cannot</strong> appear on multiple lines in the file.</li>

</ol>

A sample video file videoList1.txt has the content below:

(In case you are momentarily short on film titles to compose a video file for testing, just check out American

Film Institute’s list of 100 Greatest Movies of All Time at <a href="http://www.afi.com/100years/movies.aspx">http://www.afi.com/100years/movies.aspx).</a>.)

The name of a video file is always provided by the parameter <em>videoFile</em> in various methods in the class <em>VideoStore</em>. The file format is assumed to be <strong>correct</strong> so you do <strong>not</strong> need to worry about checking it.

<h2>2.3  Video Acquisition</h2>

Whenever new videos are acquired by the store, their records will be added to the tree inventory. Additions are carried out by three methods:

<em>public void addVideo(String videoName, int n) public void addVideo(String videoName) public void bulkImport(String videoFile) throws FileNotFoundException</em>

The last method adds multiple videos of the films from a video file whose format was given in Section 3.2.

Please refer to their javadocs when you implement the above methods.

<h2>2.4  Video Query, Rental and Return</h2>

Methods are provided to simulate video queries and transactions. The stores supports single and bulk rentals and returns.

<em>public boolean available(String videoName)</em>

<em>public void videoRent(String videoName, int n) throws IllegalArgumentException, FilmNotInInventoryException, AllCopiesRentedOutException</em>

<em>public void bulkRent(String videoFile) throws FileNotFoundException, IllegalArgumentException, FilmNotInInventoryException, AllCopiesRentedOutException</em>

<em>public void videoReturn(String videoName, int n) throws IllegalArgumentException, AllCopiesRentedOutException</em>

<em>public void bulkReturn(String videoFile) throws FileNotFoundException, IllegalArgumentException, FilmNotInInventoryException</em>

In case a method may throw multiple exceptions, use the following decreasing order of importance:

<ol>

 <li>FileNotFoundException</li>

 <li>IllegalArgumentException</li>

 <li>FilmNotInInventoryException</li>

 <li>AllCopiesRentedOutException</li>

</ol>

The method <em>bulkRent()</em> and <em>bulkReturn()</em>, accepting a parameter <em>videoFile</em>, should always <strong>read through the entire video file. Concatenate the messages of all the exceptions into one string</strong>, which is then thrown with the exception ranked the <strong>highest</strong>. In the concatenated message, the exceptions should appear in the <strong>same order</strong> as the corresponding films in the video file.

For example, if <em>bulkRent()</em> is executed with a video file which requests sequentially 1 copy of <em>The Silence of the Lambs</em> (not in inventory), -2 copies of <em>Forrest Gump</em>, and 1 copy of <em>The Godfather</em> (rented out), then it will throw an <em>IllegalArgumentException</em> and print out the following message:

<h1>3.  Simulation of Video Transactions</h1>

Suppose a VideoStore object has been constructed over the file <em>videoList1.txt</em> given in Section 3.2. A second video file <em>videoList2.txt</em> has the content below:

A third video file <em>videoList3.txt</em> has the content:

Below is a sample simulation scenario executed by the <em>main()</em> method in the class <em>Transactions</em>. (User keystrokes are shown in bold and a larger font.)

Your code needs to print out text messages in the same format for user interactions. Please note the following:

To request for the rental or return of a single video, simply enter the film title. You may also enter “(1)” after the title though it is redundant.

To request for multiple copies of the same film, enter the number of copies within a pair of parentheses after the film title.

The transaction numbered 5 in the above scenario lists rented films and unrented films in the alphabetical order decided by the <em>compareTo()</em> method for <em>String</em> objects.