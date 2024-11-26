# Tableaux
1. std::array<'T,n>
2. std::vector<'T>
3. std::span<'T>
4. Tableaux multidimensionnels
5. Tri à bulles
6. Tri par sélection
7. Tri par insertion
8. Comparaison des tris

**Array**\
- Fixed size

**Vector**\
- flex. size

## std::array<T,n>
up to 22 slide

## std::vector<T>
Goes above *array<T,n>* limitations
- Allows dynamically memory blocks where elements were stored
- Re-allows, if needed, transparently for the user (memory manag.)
- Slight overcost in memory *3\*sizeof(T\*)*

What it offers
- same interface as *std::array<T,n>* (besides .fill)
- ++ methods allows to resize the tab & to add/delete elements

### Declaration
Exemple:

```cpp
std::vector<int> v1; // tableau redimensionnable de 0 int
std::vector<double> v2; // tableau redimensionnable de 0 double
std::vector<std::string> v3; // tableau redimensionnable de 0 std::string
std::vector<std::array<double, 3>> v4; 
// tableau redimensionnable de 0 tableaux de 3 double
```
**Default init:**

```cpp
v.size() == 0 and v.empty() == true
```

### Agrégat & copy
Alike with *array*
```cpp
vector<int> v1 {3, 1, 4, 2}; // v1 contient [3, 1, 4, 1] 
vector<int> v2 = v1; // v2 contient [3, 1, 4, 1] 
```

**However** can't init w/ agregat partial unlike *array*\
-> not mandatory to precise the element's type -> can be deducted by itself

```cpp
vector v3 = v1; // v3 de type vector<int>
vector v4 { 3u, 1u, 4u, 2u }; // v4 de type vector<unsigned>
```

### Init by filling
Exemple:

```cpp
vector<int> v1(4, 10); // v1 contient [10, 10, 10, 10]
vector v2(2, 7u); // v2 de type vector<unsigned> contient [7, 7]
vector<double> v3(3); // v3 contient [0., 0., 0.]
vector<bool> v4(2); // v4 contient [false, false]
```

### Insertion
Has to be done manually... (thank u c#, luv u)\
Tuto step-by-step:
1. ++ vector size
2. Move all elements from the pos to the end of the vector to one pos to the back
3. Copy new elements to the requested place

Exemple:
```cpp
void insertion(vector<int>& v, size_t pos, int val) {
    if (pos > v.size()) // position d'insertion illicite
        return;
    v.resize(v.size()+1); // maintenant, v.size() >= 1
    for(size_t i = v.size()-1; i > pos; --i)
        v[i] = v[i-1];
        v[pos] = val;
}
```
**VERY EXPENSIVE OP. IF *POS* IS FAR FROM END OF THE VECTOR**

### Delete
Has to be done manually... (thank u c#, luv u)\
Tuto step-by-step:
1. Move all elements following the *pos* to the start
2. -- vector size

**// ! \\\\ methods for it insert, erase, emplace, emplace_back, … see chap 15**

### Existing methods (in this chap.)
- resize()
- clear()
- push_back()
- pop_back()
- capacity()
- reserve()
- shrink_to_fit()

### vector w/ const 
Useless shit that makes it loose its purpose

## std::span<T>
Another tab...

```cpp
vector<int> v(n); // classe std::vector
array<int,n> a; // classe std::array
int t[n]; // tableau classique, «à la C»
int* p = new int[n]; // tableau alloué dynamiquement
```

They were sad to have 4 similar func. So they decided to create this\
**span<T>**\
Offers a view without storing it itself (only stores the address)\
-> very good for func. param.\
Can't manage the size, for ex. with vectors

### Décla. init.
**span<'T> nom (T* p, size_t n);**

- T deduct. from p's type
-> *span nom (T\* p, size_t n);*
- Can init. obj. that knows its nb elements  (w/ vector || array)
- Elements != copied when init.

```cpp
vector<int> v {1, 2, 3, 4};
span<int> s1(&(v[0]),v.size());
span s2(&(v[0]),v.size());
span s3(v.data(), v.size());
span s4(v);
array<unsigned, 3> a {6u, 7u, 8u};
span s5(a.data(),a.size());
span s6(a); 
double t[5] = {1., 2., 3., 4., 5.};
span s7(t,5); 
span s7(t);
short* p = new short[3];
span s8(p,3); 
```

### Const
2 places so 4 possibilities\
1. span<'T>
2. span<'const T>
*-> can't modif. elements by span*
3. const span<'T>
*-> can't change which tab span sees*
4. const span<'const T>

Only *span<'const T>* can see *const vector<'T>* or *const array<'T,n>*

```cpp
vector<int> v1;
span<int> s11(v1);
span<const int> s12(v1);
const vector<int> v2;
// span<int> s2(v2);
span<const int> s2c(v2);
s12 = v2; // change le tableau vu
const span<int> s13(v1);
// s13 = v1;
// les lignes commentées ne compilent pas
```

### Pass of param.
- Usually used to pass a tab to a func.
- Like a val
- Func. !modif. val of elements must use -> *span<'const T>*
- Func. modif val of elements -> *span<'T>*
- Func !modif nb of elements

```cpp
void display(span<const int> s) {
cout << '[';
for (int e : s)
cout << e << ',';
cout << "\b]\n";
}
void fill(span<int> s, int val) {
for (int& e : s)
e = val;
}

vector<int> v{1, 2, 3, 4};
const array<int, 3> a{5, 6, 7};
display(v);  // [1,2,3,4]
display(a);  // [5,6,7]
fill(v, 42); // [42,42,42,42]
display(v);
```

### Methods
Can def. span that sees only a part of the tab. from a pos. (index)
```cpp
vector<int> v{1, 2, 3, 4, 5, 6};
span s1(&v[1],2); // s1 voit {2, 3}
```

*s.subspan(pos,len)*
```cpp
span s2 = span(v).subspan(1,2);
// s1 et s2 voient les même élément
```

*s.first(len)*
```cpp
span s3(&v[0],3);
span s4 = span(v).first(3);
// s3 et s4 voient les même éléments
```

*s.last(len)*
```cpp
span s6(&v[v.size()-2],2);
span s7 = span(v).last(2);
// s6 et s7 voient les même éléments
```

## Multi-dimensional tab

## Bubble tri

