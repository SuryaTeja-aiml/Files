# Tree Data Structure

---

## Tree Data Structure ante enti?

**Tree** ante data ni **parent-child relationship** lo store chese hierarchical structure.

### Real-life examples:

* Family tree (kutumba vruksham)
* College hierarchy (principal → HOD → faculty)
* File system (folders → subfolders → files)
* HTML DOM structure

### Tree lo main components:

| Component | Explanation |
|-----------|-------------|
| **Root** | Starting node - tree start |
| **Parent** | Kindha children unna node |
| **Child** | Parent ki connect ayyi unna node |
| **Leaf** | Children leni node - tree antha varaku |

**Simple ga cheppalante:** Tree ante **one-to-many relationship** ni represent chese structure.

---

## Tree structure ela untundhi?

```
        A        ← Root (start)
       / \
      B   C      ← Children (A ki pillalu)
     / \
    D   E        ← Leaf nodes (inka kindha evaru ledu)
```

---

## Python lo Tree ela implement chestham?

Python lo direct "Tree" ane datatype ledu. Maname **class create chesi** tree build cheskovali.

### Step 1: Tree Node class create cheyyadam

```python
class Node:
    def __init__(self, data):
        self.data = data           # Node lo store chese value
        self.children = []         # Ee node ki unna children list
```

**Key concepts:**
- `__init__` = magic method (constructor) - object create ayinappudu automatic ga run avuthundhi
- `self` = current object reference
- `self.data` = ee particular node ki belong aina data
- `self.children = []` = initial ga empty list, taruvatha children add chestham

### Step 2: Tree build cheyyadam

```python
# Root node create cheyyadam
root = Node("A")

# Children nodes create cheyyadam
child1 = Node("B")
child2 = Node("C")

# Root ki children connect cheyyadam
root.children.append(child1)
root.children.append(child2)

# B ki grandchildren add cheyyadam
child1.children.append(Node("D"))
child1.children.append(Node("E"))
```

**Ela work avuthundhi:**
- Nodes separate ga create avuthayi
- `append()` dwara connections create chestham (references store chesthundi)
- List lo order maintain avuthundhi

### Step 3: Tree print cheyyadam (Traversal)

```python
def print_tree(node, level=0):
    # Current node print cheyyadam with indentation
    print(" " * level + node.data)
    
    # Prathi child kosam recursively call cheyyadam
    for child in node.children:
        print_tree(child, level + 2)

# Usage
print_tree(root)
```

**Output:**
```
A
  B
    D
    E
  C
```

**Traversal explanation:**
- **Traversal** ante tree lo prathi node ni visit cheyyadam
- `level` parameter indentation kosam (depth chupinchataniki)
- Spaces tree structure visually create chesthayi
- Recursion dwara automatic ga anni nodes visit avuthayi

---

## Important Concepts - Deep Dive

### 1. Tree nodes memory lo ela untayi?

**Key point:** Nodes **pakkana pakkana memory lo undavu**. Avi **references dwara connect** ayyi untayi.

```python
root = Node("A")
```

Idi jargedappudu:
- Python memory lo **kotha object create** avuthundhi
- Aa object lo `data = "A"` mariyu `children = []` store avuthayi
- `root` variable aa object **address ni point** chesthundhi

### 2. Root, Parent, Child, Leaf - clarity

**Root:**
- Tree start starting point
- **Eppuduuu child avvadu** (top lo untundhi)
- Special case: Single node unte adhe root + leaf kuda

**Parent:**
- Kindha **minimum okka child** unte aa node parent
- Root ki children unte **root kuda parent**

**Child:**
- Paina okka node ki connect ayyi unna node
- Oka child ki malli children unte **adhi parent kuda** avuthundhi

**Leaf:**
- **Only parent untundhi**, children undaru
- Tree bottom lo untayi

### 3. Class enduku use chestham? Function enduku kaadhu?

**Function:**
- Okate pani chesthundhi
- Data store cheyyaleru

**Tree node requirement:**
- Data store cheyali (`data`)
- Children list store cheyali (`children`)
- **Data + behavior rendu kavali** → anduke **class**

### 4. `self` ante enti?

`self` = **current object reference** (number kaadhu, counter kaadhu)

**Example:**
```python
root = Node("A")
```

Internally Python chesedhi:
```python
Node.__init__(root, "A")  # self = root object
```

**Analogy:** Prathi student ki separate bag untundhi. `self.data` ante "ee particular student bag lo unna data".

### 5. Connection ela create avuthundhi?

```python
root.children.append(child1)
```

Ikkada jarigedi:
- List lo **child1 object address** store avuthundhi (data kaadhu)
- Idi **reference** (connection) create chesthundhi
- Memory lo separate ga unna nodes connect ayyinatte

---

## Binary Tree

### Binary Tree ante enti?

**Binary Tree** ante prathi node ki **maximum 2 children matrame** unde tree.

**Rule:** Oka node ki 0, 1, leda 2 children - antha ekkuva kaadhu

- Left child
- Right child

### Structure example:

```
        A
       / \
      B   C
     / \   \
    D   E   F
```

### Python lo implementation:

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None      # Left child reference
        self.right = None     # Right child reference

# Tree build cheyyadam
root = Node("A")
root.left = Node("B")
root.right = Node("C")
root.left.left = Node("D")
root.left.right = Node("E")
root.right.right = Node("F")
```

**Key difference:**
- General tree lo `children` list
- Binary tree lo `left` and `right` direct references
- Assignment use chestham, append kaadhu

### Binary Tree Traversal Orders

#### 1. Inorder (Left → Root → Right)

```python
def inorder(node):
    if node:
        inorder(node.left)          # Left ki vellu
        print(node.data, end=" ")   # Root print cheyyi
        inorder(node.right)         # Right ki vellu

# Output: D B E A C F
```

#### 2. Preorder (Root → Left → Right)

```python
def preorder(node):
    if node:
        print(node.data, end=" ")   # Root first
        preorder(node.left)         # Taruvatha left
        preorder(node.right)        # Taruvatha right

# Output: A B D E C F
```

#### 3. Postorder (Left → Right → Root)

```python
def postorder(node):
    if node:
        postorder(node.left)        # Left first
        postorder(node.right)       # Taruvatha right
        print(node.data, end=" ")   # Last ki root

# Output: D E B F C A
```

**Logic:** Recursion use chesi prathi node visit chestham. Order maripothe output kuda maruthundhi.

---

## Binary Search Tree (BST)

### BST ante enti?

**BST** = Binary Tree + Ordering rule

**Critical Rule:**
- Left child < Parent
- Right child > Parent

### Example:

```
      10
     /  \
    5    15
   / \
  3   7
```

### Insert logic:

```python
def insert(root, value):
    # Base case: empty spot dorikindhi
    if root is None:
        return Node(value)
    
    # Value compare chesi direction decide cheyyadam
    if value < root.data:
        root.left = insert(root.left, value)   # Left ki vellu
    else:
        root.right = insert(root.right, value) # Right ki vellu
    
    return root
```

### Ela work avuthundhi?

**Example:** Values insert chesthunnam - 10, 20, 5

**Step 1:** Insert 10
```
10  (root empty, 10 becomes root)
```

**Step 2:** Insert 20
```
10
  \
   20  (20 > 10, so right ki poyindhi)
```

**Step 3:** Insert 5
```
    10
   /  \
  5    20  (5 < 10, so left ki poyindhi)
```

**Key points:**
- Insert order matter kaadhu
- **Value comparison** decide chesthundhi position
- Prathi level lo comparison jaruguthundhi
- Wrong input error ivvadhu, kani tree shape affect avuthundhi

### BST Worst Case Problem:

Sorted order lo insert chesthe (1, 2, 3, 4, 5):

```
1
 \
  2
   \
    3
     \
      4
```

Idi **linked list laaga** maruthundhi → search slow avuthundhi

**Solution:** AVL Tree

---

## AVL Tree

### AVL Tree ante enti?

**AVL Tree** = Self-Balancing Binary Search Tree

BST + Automatic balancing

**Balance Rule:**
```
|height(left) - height(right)| ≤ 1
```

### Enduku AVL kavali?

**BST problem:** Worst case lo linked list avuthundhi (slow search)

**AVL solution:** Automatic ga **rotate chesi balance** maintain chesthundhi

**Benefit:** Search always fast - guaranteed **O(log n)** time

### Balance Factor:

```
Balance Factor = height(left subtree) - height(right subtree)
```

Allowed values: **-1, 0, +1 matrame**

### Imbalance vasthe em avuthundhi?

Balance factor **±2** vasthe → **Rotation compulsory**

**Rotation types:**
- Left Rotation
- Right Rotation
- Left-Right Rotation
- Right-Left Rotation

**Important:** ±2 difference allow cheyyamu. AVL strict ga ±1 rule follow chesthundhi. Lekapothe performance guarantee pothundhi.

### AVL vs Red-Black Tree:

| Feature | AVL Tree | Red-Black Tree |
|---------|----------|----------------|
| Balance | Chala strict | Konchem loose |
| Search | Fast | Slow |
| Insert/Delete | More rotations | Less rotations |
| Usage | Search-heavy apps | Linux, Java |

---

## Heap

### Heap ante enti?

**Heap** = Complete Binary Tree with special ordering rule

**Two types:**

1. **Max Heap:** Parent value >= Children (largest value root lo)
2. **Min Heap:** Parent value <= Children (smallest value root lo)

### Structure:

```
        10         (Max Heap)
       /  \
      5    8
     / \
    2   3
```

**Rules:**
- Binary Tree
- **Complete tree** (levels left to right fill avvali)
- Sorting kaadhu - just parent-child rule

### Array representation:

Heap ni usually **array lo store** chestharu

Index `i` ki:
- Parent = `(i-1) // 2`
- Left child = `2*i + 1`
- Right child = `2*i + 2`

### Use cases:

- **Priority Queue**
- CPU Scheduling
- Dijkstra Algorithm
- Top K elements find cheyyadam
- Min/Max **O(1) time** lo find cheyyadam

### Operations:

**Insert:**
1. Array last lo add cheyyi
2. Parent tho compare cheyyi
3. Rule satisfy ayye varaku swap cheyyi (heapify up)

**Delete root:**
1. Root remove cheyyi
2. Last element ni root position ki techi
3. Rule satisfy ayye varaku swap cheyyi (heapify down)

---

## Trie

### Trie ante enti?

**Trie** (Prefix Tree) = Strings store chese special tree structure

**Key feature:** Common prefixes share avuthayi

### Example:

Words: cat, car, can

```
    root
     |
     c
     |
     a
    /|\
   t r n
```

### Node structure:

```python
class TrieNode:
    def __init__(self):
        self.children = {}        # Dictionary - character → child node
        self.endOfWord = False    # Complete word ikkada aythunda?
```

### Use cases:

- **Auto-complete** (Google search suggestions)
- **Spell checker**
- **Dictionary** implementation
- **Phone contacts** search
- IP routing

### Key advantage:

Search time = **word length** (dictionary lo enni words unte em matter kaadhu)

Example: "cat" search cheyyadaniki time = 3 (dictionary lo 10 words unte leda 10,000 words unte)

### Insert logic:

```python
def insert(root, word):
    node = root
    for char in word:
        if char not in node.children:
            node.children[char] = TrieNode()
        node = node.children[char]
    node.endOfWord = True
```

**Ela work avuthundhi:**
- Letter by letter travel chestham
- Common prefix repeat avvadhu (memory save)
- "cat" mariyu "car" ki "ca" common - share avuthundhi

---

## Common Questions - Clear Answers

### Q1: Object ante enti?

**Answer:** Memory lo **separate box** laga. Dantlo data + references untayi. Variable aa box address ni point chesthundhi.

### Q2: `self` count ah? 0 nunchi start avuthunda?

**Answer:** Kaadhu. `self` ante **current object reference** - number kaadhu, counter kaadhu. Python automatic ga pass chesthundhi.

### Q3: Nodes separate ga define cheyyala?

**Answer:** Kaadhu. Root, Parent, Child, Leaf - ivi **roles** matrame, separate objects kaavu. Structure batti Python automatic ga classify chesthundhi.

### Q4: Append ante connection create avuthunda?

**Answer:** Avunu. Append list lo **reference (address) store** chesthundhi - data kaadhu. Idi connection create chesinattu.

### Q5: Recursion ela work avuthundhi?

**Answer:** Function thaane thane ni call chesthundhi:
1. Current node process cheyyi
2. Children ki call cheyyi
3. Prathi child same pani chesthundhi
4. Leaf node daggara automatic ga stop

### Q6: BST lo wrong order lo insert chesthe error vasthunda?

**Answer:** Error radu. Kani tree shape affect avuthundhi. Worst case lo linked list laaga aavadaం (slow). AVL tree ee problem solve chesthundhi.

### Q7: Level 0 enduku? 1 enduku kaadhu?

**Answer:** Convention. Root ki depth = 0. Prathi level kindaki poye koddi +1. Visual hierarchy kosam spaces multiply chestham.

### Q8: Tree output lo alphabets compare cheyyadam?

**Answer:** Kaadhu. Output lo A, B, C, D compare cheyyadam kaadhu. **Structure** choodadam - evaru evariki children ani.

---

## Summary Table

| Data Structure | Max Children | Ordering Rule | Balance | Main Use |
|----------------|--------------|---------------|---------|----------|
| General Tree | Unlimited | Ledu | Ledu | Hierarchies |
| Binary Tree | 2 | Ledu | Ledu | Basic structure |
| BST | 2 | Left < Parent < Right | Ledu | Sorted search |
| AVL Tree | 2 | Left < Parent < Right | Avunu | Fast guaranteed search |
| Heap | 2 | Parent-child rule | Ledu | Priority queue |
| Trie | Many | Ledu | Ledu | String search |

---

## Key Takeaways

1. **Tree** = hierarchical relationships store chese structure
2. **Nodes** memory lo references dwara connect (adjacent kaavu)
3. **Recursion** = tree operations ki main technique
4. **Different trees** different problems solve chesthayi:
   - BST → sorted data kosam
   - AVL → guaranteed performance kosam
   - Heap → priority management kosam
   - Trie → string operations kosam
5. **Balance** = large trees lo performance ki critical

---

**Trees are fundamental!** Databases, compilers, AI, file systems - anni lo use avuthayi.

---