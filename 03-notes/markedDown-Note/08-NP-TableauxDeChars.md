# Chaînes de caractères
1. Type char
-> ASCII\
-> <'cctype>
2. Chaînes littérales
3. Classe std::string
4. Opé & méthodes std::string
5. std::string_view
6. Above ASCII

## Type char
Stored on 1 byte\
- *signed char* -> int bet. -128 & 127
- *unsigned char* -> int bet. 0 & 255
- *char* -> signed or naj depend on compil.

Allows to store char through ASCII tab\
Modif. de sign != affect char coded on 8bits\
Litteral const char -> bet. ''

**Primitiv ASCII table** ouga bouga caverne: \
![images](/img/basic-ASCII.png)

**Affichage**\
given to opé flux **<<** if we show char or its val.\
**BEWARE OF PROMO TYPES**\

**Shiny const:**\
![images](/img/shiny-const.png)

### Char categories
<'cctype> func. allows to know which cat. the char belongs to\
Return 1 for *true* else the char nb and 0 for *false*

- *isalnum(int a)* -> letter of nb
- *isalpha(int a)* -> màj or min 
- *iscntrl(int a)* -> char de control (0-31 & 127)
- *isdigit(int a)* -> is a nb
- *isxdigit(int a)* -> is hexa nb
- *isgraph(int a)* -> showable non-white (33-126)
- *islower(int a)* -> min. alphabet
- *isupper(int a)* -> màj alphabet
- *isprint(int a)* -> showable char (32-126)
- *ispunct(int a)* -> ponctuation
- *isspace(int a)* -> space, tab, end of line and line return
- *isblank(int a)* -> space or tab

**Rappel**
*Chaine de char* == "shit"\
To write it in bet. "tut" must put *\"*\
Same to write a \\ u put them 2x
To write a chain on multiple line -> \ to return line (won't empty the buffer)\

Exemple:
```cpp
int main() {
cout << "Hello, World !" << endl;
cout << " \" et \\ au milieu d’une 
chaine" 
<< endl;
cout << "Une chaine \
ecrite sur plusieurs \
lignes" << endl;
cout << "Une"
" chaine "
"en " "plusieurs"
"parties" << endl;
}
/*
Hello, World !
" et \ au milieu d’une chaine
Une chaine ecrite sur plusieurs lignes
Une chaine en plusieursparties
*/
```
**Chaine brute** -> prefix. **R**\
Dodge all the syntax to have to put shiny char to make it in format\
 R"(" et ") ou R"xyz( et "xyz)
Exemple:
```cpp
// syntaxe originale
cout << " \" et \\ au milieu d’une chaine" << endl;

// syntaxe chaine brute
cout << R"( " et \ au milieu d’une chaine)" << endl;

// syntaxe chaine brute alternative
cout << R"abc(Placer les memes caracteres entre les "( initial et )" final 
permet d'ecrire )" dans la chaine brute )abc" << endl;
/*
" et \ au milieu d’une chaine
" et \ au milieu d’une chaine
Placer les memes caracteres entre les "( initial et )" final permet 
d'ecrire )" dans la chaine brute
*/
```

litteral const type == const char* not string\
Conversion.
```cpp
auto s1 = string("hello"); // conversion explicite
auto s2 = "hello"s; // conversion par suffixe
```

## std::string
Store chaine de char in var type *std::string*\
//!\\\ Not fundamental type of C++ -> defined in <'string>
```cpp
#include <string>
using namespace std;
…
string s = "Hello, World!";
```

**Init**
If not defined == chaine of void *smol void on a leash hehehe*\
**Literal chaine**
```cpp
string s1 = "Hello, World!";
string s2("Hello, World!");
string s3{"Hello, World!"};
```

**copied chiane**
```cpp
string s4 = s1;
string s5(s1);
string s6{s1};
```

Most intersting == **construct**

Construct. fills **string(size_t n, char c)**\
-> create chaine with n nb of the char
```cpp
string s1(6, 'a'); // "aaaaaa"
```
Construct. fills buffer **string(const char* p, size_t n)**\
-> create chaine with first n char from buffer starting with address **p**\
ouga bouga type
```cpp
const char* p = "Hello, world !";
string s2(p,5); // "hello"
string s3("Hello, World!", 4); // "hell"
string s4(s2.data(),2); // "he"
```

Construct. **string(string str, size_t pos, size_t len)**\
-> create chaine of len char copied from char in pos. from str chaine\
if *len* isn't given, str copied until its end
start nb from 0

```cpp
// indices 01234567890123 
string hello("Hello, World!"); 
string s1(hello, 0, 4); // contient la chaîne "Hell"
string s2(hello, 7, 5); // contient la chaîne "World"
string s3(hello, 7); // contient la chaîne "World!"
string s4(hello); // contient la chaîne "Hello, World!"
```

**//!\\\ BEWARYYYYY //!\\\\**\
    ``When we construt. chain w/ 2 param -> second being an int``\
    ``-> construct. from buffer, if first param == literal chaine``\
    ``-> construct by under-chaine with 3rd param len not specified, if first param type == std::string``\

## Opé & methods

**=** -> give value to str\
implicit convert expr. from char or chains in C, const. litteral as well
```cpp
string str1, str2, str3;
str1 = "Test string: "; // chaîne C littérale
str2 = 'x'; // caractère
str3 = str1; // string
```

### Affectation
*.assign(...)*-> invoke itself with same args as construct.\
```cpp
string str,
world("World!"),
hw("Hello, World!");

// les lignes suivantes sont équivalentes
str.assign(world);
str.assign(hw, 7, 6);
str.assign("World!");
str.assign("World!!!!", 6);

// cette ligne donne la chaîne "WWWWWW"
str.assign(6, 'W');
```

### Concat.
Opé -> **+**
Concat. chains bet. them same for char (even alone)\
Is okay:
```cpp
string hello("Hello, ");
string world("World!");
string s1 = hello + world; // "Hello, World!"
string s2 = "Hello, " + world; // "Hello, World!"
string s3 = hello + "World!"; // "Hello, World!"
```

Will give u shit\
-> 2 litteral chains\
-> std::string & int\
-> litteral chain + char

Is not okay:
```cpp
string erreur1 = "Hello, " + "World!"; 
// ne compile pas

string erreur2 = hello + 5; 
// ne compile pas

string erreur3 = "Hello, " + 'W'; 
// comportement indéfini
```

Opé -> **+=**

```cpp
string str("Hello");
str += ','; // même effet que str = str + ','; 
// str contient "Hello,"
str += " World"; // même effet que str = str + " World"; 
// str contient maintenant "Hello, World"
string exclamation("!");
str += exclamation; // même effet que str = str + exclamation; 
// str contient maintenant "Hello, World!"
```

### Appondre
*.append(...)*
More option than concat. classic
```cpp
string str("Hello, "),
world("World!"),
hw("Hello, World!");

// les lignes suivantes sont équivalentes
str.append(world);
str.append(hw, 7, 6);
str.append("World!");
str.append("World!!!!", 6);

// la ligne suivante ajoute la chaîne "WWWWWW"
str.append(6, 'W');
```

### Unsafe index content requester 
Char access -> []**\
Index use\
Behaviour undefined when we give param out of interval bet. 0 and end of chain -1
```cpp
string hello("Hello, World!");
char fifth = hello[4];
hello[4] = ' ';
cout << hello << endl;
cout << fifth << " remplacé par un blanc" << endl;
/*
Hell , World!
o remplacé par un blanc
*/
```
### Safe index content requester
**at()**\
Moare secured *french accent*\
Same as [] but check if the index nb is in the intervale\
-> will throw an exception
```cpp
string hello("Hello, World!");
char fifth = hello.at(4);
hello.at(4) = ' ';
cout << hello << endl;
cout << fifth << " remplacé par un blanc" << endl;
```

Nb char of a chain w/ *.length()* or *.size()*\
will return var type size_t -> unsigned int\

```cpp
string s("Hello");
size_t longueur = s.length(); // 5
size_t taille = s.size(); // 5 aussi
```
### Empty
*.empty()*\
Check if empty
```cpp
string s("Hello");
bool vide1 = s.size() == 0; // false
bool vide2 = s.empty(); // idem, mais plus clair
```
### Resize
*.resize(size_t len, char c)*\
Change chain size\
-> len == new size\
-> c spé char used to complete chain if ++ its size\
'\0' will be used as default char

```cpp
// 01234567
string s("Hello"); // "Hello"
s.resize(8, '!'); // "Hello!!!"
s.resize(4); // "Hell"
s.resize(6); // "Hell\0\0"
```

### Sub-chain
*.substr(size_t pos, size_t len)*\
Extract sub-chain of *len* char starting at pos\
len lacking -> extract until the end\
pos lacking -> extract from the start

```cpp
// 0123456789*12
string s("Hello, World!");
string s1 = s.substr(0, 5); // "Hello"
string s2 = s.substr(7, 5); // "World"
string s3 = s.substr(7); // "World!"
string s4 = s.substr(); // "Hello, World!"
```

### Insertion 
*.insert(size_t pos, string str)*\
Insert chain str in pos.\
++ its size of the chaine unless it's a ""str\
str can be replaced like in method append, assign, etc...

### Replace
*.replace(size_t pos, size_t len, string str)*\
replace chain *str* by the sub-chain of length *len* starting at *pos*\
-> change size of chain if st.length != len\
-> *str* can be replaced like in method append\

### Delete
*.clear()*\
empty the chain\
WAAAAAAAAAAAAAAAAAAAAAW ROCKET SCIENCE BITCH\

*.erase(size_t pos, size_t len)*\
erase *len* char starting at *pos*\
-> until the end if *len* unspecified\
-> Starting from the beginning if *pos* unspecified\
*synonyme de clear()*

```cpp
string s("This is an example sentence.");
s.erase(9, 9); // "This is a sentence."
s.erase(13); // "This is a sen"
s.erase(); // ""
```

## string_view
Ptr under batman desguise that pt on a chain of char (can see also only a part of it)\

