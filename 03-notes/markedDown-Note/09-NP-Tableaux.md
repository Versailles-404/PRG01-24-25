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
