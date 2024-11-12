# struct, enum et std::pair

**struct**
- Déf, décla, init. & affect
- Member access
- Param given, return val
- récup of members

**std::pair**\
**enum**
- Déf, décla, init. & affect
- Limitations
- enum class
- Param given, return val
- comparison
 
```cpp
struct Section {
int number; 
string name; 
};
struct Chapter {
string title;
Section section1;
Section section2;
Section section3;
};
int main() {
Chapter chapter5 {
.title { "struct, enum et pair"},
.section1 { 1, "struct"},
.section2 { 2, "std::pair"},
.section3 { 3, "enum"}
};
}
```

## struct
Allows to déf. type of struct. with keyword **struct**

Déf model of struct -> décla instances (var of it) as much as needed

Struct. can group one or more of elem. -> member or champs\
-> can have diff. types
- each member has a name -> give access to it
- unlike tab where we use index

**Définition**\
```cpp
struct [ nom_de_type ] {
    declaration_membre;
    [ declaration_membre; ... ]
} [ identificateur, ... ]; 
```
- nom_de_type (optionnal)\
-> give a name to the type structured -> allows to re-use later
- declaration_membre\
-> décla of member separated by ;
- identificateur (optionnal)\
-> décla var of this type

Can use a maj. initial for struct. model\
Member (champs, in min.) -> stored in memory in order of definition

Examples:
- Members can be of the same type
```cpp
struct Coord {
double x, y, z;
};
```
- Or nah
```cpp
struct Date {
int jour;
int mois;
int annee;
};
```
- It can also have an object, a struct member
```cpp
struct Personne {
string nom;
int age;
Date naissance;
};
```
- Members can be const and or have default val.
```cpp
struct UneStruct {
const char cste = 'A';
int entier;
double* ptr = nullptr;
};
```

**Déclaration**

- As usual décla based on type and can be init.
- Members not init. unless construct does
- When init. partiel (*agrégat*), val used by pos.\
-> lacking value = **0**

```cpp
Date date1; // ??, ??, ????
Date date2 = {1, 2, 2019}; // 1, 2, 2019
Date date3 = {1, 2}; // 1, 2, 0
Personne Vide; // «», ??, ??, ??, ????
Personne Anna = {"Anna", 4, date2}; // «Anna», 4, 1, 2, 2019
Personne Jean = {"Jean", 18, {11, 3, 2005}}; // «Jean», 18, 11, 3, 2005 
Personne Paul = {"Paul", 27, 31, 7, 1996 }; // «Paul», 27, 31, 7, 1996
```

Slide 8