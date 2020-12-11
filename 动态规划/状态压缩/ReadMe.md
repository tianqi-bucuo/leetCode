## 状态压缩的一些基本操作

定义两个集合 **A** 和 **B** : 

    int A, B

元素 **i** :

    int i

操作

- A = 0           // empty A

- A | B           // union

- A & B           // intersection

- A |= 1 << i     // insert i

- A &= 1 << i     // erase i

- A ^= 1 << i     // erase i (i exist)

- (A & B) == B    // B is A's subset

- initialize a size of set, and it's universal set
    - int size = 15     // size of set
    - int all = (1 << size) - 1     // universal set
    - all ^ A       // complement of A

// enumeration the subset of all

for (int i = 0; i < all; i++)   subset = i;

// enumeration the subset of A

int subset = A

do{
    subset = (subset - 1) & A
} while (subset != A)

// count the number of element in A

int temp = A, cnt = 0

while (temp != 0) {
    temp &= (temp - 1);
    cnt++;
}

// i is a power of 2

(i & (i - 1)) == 0

// lowbit

lowbit(i) = i & (-i)