04.11.2024

# Arithmétics & Conversions

## Entiers
Entiers signés
    - Représentation en mémoire
    - numeric_limits
    - Dépassement 
Entiers non signés\
Alias de type et entiers de taille fixe\
Entiers littéraux\
Entrées / sorties entières\

### Entiers signé

- Bit
- Octet
- Byte

if maj like : CHAR_BIT == macro
CHAR_BIT from <"climits>

*nb* of bits *used* == *nb* int that we *can show*\
Avec n bits -(n/8) octets - on peut représenter jusque 2^n entiers différents\

n=4 -> 2^4 = 16 entiers différents

Entiers positifs -> 0 à 2^n-1 -1 codé en binaire (en base 2)\
1st bit always 0 bcs +, if 1 then entier == nég.

**Complément à 2**

-5 -> 5 == 0101 -> revert -> 1010 -> +1 -> 1011\
val. nég -> val. absolue -> val bin -> revert bin -> add 1

**Tailles d'entiers**
- signed short int
min. 16
- signed int
min. 16
- signed long int
min. 32
- signed long long int (-> titre, selon Manu)
min. 64

*On peut également utiliser le type caractère signed char comme un entier sur 8 bits.*\
**Le mot clé signed n’est pas optionnel dans ce cas**\

*Size range:*\
sizeof(short) <= sizeof(int) <= sizeof(long) <= sizeof(long long)

**sizeof(the titre)** -> return size of the titre in bytes\
ou\
**sizeof** *expression/var*

Example of use / / ! \ \ BEWARE OF THE ARCHI
```cpp
cout << "short : " << sizeof(short) * CHAR_BIT << endl;
cout << "int : " << sizeof(int) * CHAR_BIT << endl;
cout << "long : " << sizeof(long) * CHAR_BIT << endl;
cout << "long long : " << sizeof(long long) * CHAR_BIT << endl;
```
**Windows:**\
short : 16\
int : 32\
long : 32\
long long : 64

**Linux**\
short : 16\
int : 32\
long : 64\
long long : 64

### Numeric limits
type numérique est d’utiliser les méthodes de **std::numeric_limits**
Exemples:
```cpp
std::numeric_limits<type>::lowest() 
// plus petite valeur représentable 
std::numeric_limits<type>::max() 
// plus grande valeur représentable 
std::numeric_limits<type>::digits 
// nombre de bits hors bit de signe
std::numeric_limits<type>::is_signed 
// vrai pour les types signés
std::numeric_limits<type>::is_integer 
// vrai pour les types entiers
```
------------------------------------
```cpp
#include <iostream>
using namespace std;
int main() {
cout << " ** signed short int ** " << endl;
cout << "lowest : " << std::numeric_limits<short>::lowest() << endl;

cout << "max : " << std::numeric_limits<short>::max() << endl;
cout << "digits : " << std::numeric_limits<short>::digits << endl;

cout << "\n ** signed int ** " << endl;
cout << "lowest : " << std::numeric_limits<int>::lowest() << endl;

cout << "max : " << std::numeric_limits<int>::max() << endl;
cout << "digits : " << std::numeric_limits<int>::digits << endl;
cout << "\n ** signed long long int ** " << endl;
cout << "lowest : " << std::numeric_limits<long long>::lowest() << endl;

cout << "max : " << std::numeric_limits<long long>::max() << endl;

cout << "digits : " << std::numeric_limits<long long>::digits << endl;

}

```
Output:\ 
**signed short int**\ 
lowest : -32768\
max : 32767\
digits : 15\
**signed int**\ 
lowest : -2147483648\
max : 2147483647\
digits : 31\
**signed long long int**\
lowest : -9223372036854775808\
max : 9223372036854775807\
digits : 63\

**Overflow**\
Result of calcul with type given cannot be represented by the type\
    Std C++ of overflow on calcul in signed int -> undefined result
    -> **inutilisable**

```cpp
//std::numeric_limits<int>::max() qui vaut 2'147'483'647*
int a = 2'000'000'000;
int b = 1'000'000'000;
int c = a + b;
cout << a << " + " << b << " = "
<< c << endl;
//2000000000 + 1000000000 = -1294967296
```

Si comportement indéfini:
```cpp 
//Probably in complém. 2 = -2147483648
cout << numeric_limits<int>::max() + 1;
```
**CANNOT BE TRUSTED** (aiiiiiiie cooonfiaaaaaaance... mdr bien sûr la vipère...)\

So you check the calcul before doing it
- Les 2 opérandes sont positives et le résultat est\ 
*> numeric_limits<'int>::max()*\
- Les 2 opérandes sont négatives et le résultat est\ 
*< numeric_limits<'int>::lowest()*

Check both of the previous posibilities:
```cpp 
bool sum_would_overflow(int lhs, int rhs) {
return (lhs >= 0) ?
numeric_limits<int>::max() - lhs < rhs :
rhs < numeric_limits<int>::lowest() - lhs;
}
```
Minus and multiply can also overflow

### Entiers non signés

Must add **unisgned**\
```cpp
// unsigned char ( 8 bits ) : 0 -> 255
cout << "unsigned char ( " << std::numeric_limits<unsigned char>::digits << " bits ) : "
<< +std::numeric_limits<unsigned char>::lowest() << " -> "
<< +std::numeric_limits<unsigned char>::max() << endl;

// unsigned short ( 16 bits ) : 0 -> 65535
cout << "unsigned short ( " << std::numeric_limits<unsigned short>::digits << " bits ) : "
<< std::numeric_limits<unsigned short>::lowest() << " -> "
<< std::numeric_limits<unsigned short>::max() << endl;

// unsigned int ( 32 bits ) : 0 -> 4294967295
cout << "unsigned int ( " << std::numeric_limits<unsigned>::digits << " bits ) : "
<< std::numeric_limits<unsigned>::lowest() << " -> "
<< std::numeric_limits<unsigned>::max() << endl;

// unsigned long long ( 64 bits ) : 0 -> 18446744073709551615
cout << "unsigned long long ( " << std::numeric_limits<unsigned long long>::digits << " bits ) : "
<< std::numeric_limits<unsigned long long>::lowest() << " -> "
<< std::numeric_limits<unsigned long long>::max() << endl;
```
Even if behaviour is weird af -> not an overflow...\
if max value representable on unsigned value if +1 -> **goes back to 0**

**Arithmétique modulo 2^n**

+ - et * are defined in *modulo 2^n*\

## Réels
- In memory : IEEE 754, zéro, nombres dénormalisés, infini, NaN
- C++ : float, double, long double
- Input/Output -> fixed, scientific, defaultfloat, hexfloat, 
showpoint, setprecision(n)
- lib : <'cmath>

**virgule flottante/floating point op**

![images](/img/showReel-math.png)

**base** (*b*) => int usually 2 or 10\
**sign** (*s*) => bin sign {0,1}\
**exposant** (*e*) => int\
**mantisse réelle** (*m*) => 1 <= *m* < *b*  -> forme normalisée for 1 pair (*m,e*) code even *r*

Exemple: for *314,2*

![images](/img/reel-exemple1.png)

*r* = (−1)^*s*⋅ *m* ⋅ *b^e* -> bin \
*e* via un entier pos. *E* - biais constant *B*\

![images](/img/entier-biais.png)

*m* via un entier pos. *M* avec *p* chiffres en base *b*\
0 <= *M* < *b ^ p*\

![images](/img/mantisse.png)

**approximation de la valeur** de *r*.\
Avec *p* chiffres en base *b* pour coder la mantisse:

![images](/img/mantisse2.png)

**erreur relative** bet val codée and the *r* => € = 1/b^(p-1)

### double - float

**SLIDE 51-52**

## Conversion entre types

**Forme fonctionnelle**\

```cpp
int e = 42;
double d1 = double(e); // forme fonctionnelle
double d2 = (double)e; // operator de cast
double d3 = static_cast<double>(e); // static_cast
double d4 = e; // conversion implicite
```
*static cast* -> safer than classical cast\
Require type in 1 word
```cpp
using ull = unsigned long long; unsigned long long u = ull(e);
```

5 signed type, 5 unsigned, 3 real types == 156 convert possible\
Promo numeral to int\
Convert:\
- int to int
- all numeral to real
- real to int

Promo:\
*Get more room to live -> no loss*
- char, signed char, unsigned char, signed short, ou 
unsigned short -> int
- bool -> int
- 

Conversion:\
*Get less room to live == more problem to come*\
If it doesn't fit, will yeet

```cpp
for(int s : { 100, 200, 8100, 40000, -10 }) 
cout << setw(5) << s << " : " << setw(4) << +(unsigned char) s << "(uc) " 
<< setw(4) << +(signed char) s << "(sc) " << setw(5) << (unsigned short) s << "(us) " 
<< setw(6) << (signed short) s << "(ss)" << setw(11) << (unsigned int) s << "(ui)\n";
/*
100 : 100(uc) 100(sc) 100(us) 100(ss) 100(ui) 
200 : 200(uc) -56(sc) 200(us) 200(ss) 200(ui) 
8100 : 164(uc) -92(sc) 8100(us) 8100(ss) 8100(ui) 
40000 : 64(uc) 64(sc) 40000(us) -25536(ss) 40000(ui) 
-10 : 246(uc) -10(sc) 65526(us) -10(ss) 4294967286(ui)
*/
```

*Int convert -> compl. to 2*

signed ↔ unsigned no change of bit\
long → court shorten left bits\
court → long adds zeros (unsigned) or signeing bits (signed) on the left

```cpp
for(int s : { 200, 40'000, 42'000'000, -10 })
cout << setw(8) << setfill(' ') << dec << s << " : " << hex << setfill('0')
<< setw(8) << (signed int) s << "(si) " << setw(8) << (unsigned int) s << "(ui) "
<< setw(4) << (signed short) s << "(ss) " << setw(4) << (unsigned short) s << "(us) "
<< setw(16) << (signed long long) s << "(sl) " << setw(16) << (unsigned long long) s << "(ul)\n";

/*
200 : 000000c8(si) 000000c8(ui) 00c8(ss) 00c8(us) 00000000000000c8(sl) 00000000000000c8(ul)
40000 : 00009c40(si) 00009c40(ui) 9c40(ss) 9c40(us) 0000000000009c40(sl) 0000000000009c40(ul)
42000000 : 0280de80(si) 0280de80(ui) de80(ss) de80(us) 000000000280de80(sl) 000000000280de80(ul)
-10 : fffffff6(si) fffffff6(ui) fff6(ss) fff6(us) fffffffffffffff6(sl) fffffffffffffff6(ul)
*/
```

*Real to int*\
Fraction part -> yeeted
```cpp
int a = 2.55;       // a = 2
int b = -2.55;      // b = -2
double c = 2.55;
int d = c + 0.5;    // troncature => 3
```
Val not showable in int -> undefined result
```cpp
unsigned char a = 300;       // conversion entier → entier : a = 44
unsigned char b = 300.;      // conversion réel → entier : b indéterminé
                             // b = 0 (Apple LLVM 8.1)
                             // b = 255 (Windows gcc)
unsigned char c = int(300.); // conversion double → int → unsigned char
                             // c = 44
```

### Round manag.

*trunc* yeet post ,\
*round* int nearest of it for 0.5\
*floor* int smallest or =\
*ceil* int bigger or =

```cpp
/*
value trunc round floor ceil
---------------------------------
 2.3   2.0   2.0   2.0   3.0
 3.8   3.0   4.0   3.0   4.0
 5.5   5.0   6.0   5.0   6.0
-2.3  -2.0  -2.0  -3.0  -2.0
-3.8  -3.0  -4.0  -4.0  -3.0
-5.5  -5.0  -6.0  -6.0  -5.0
*/
```

- truncf, floorf, roundf, ceilf
- truncl, floorl, roundl, ceill

real to int can be shiny:
```cpp
double d = 100 * 4.35;
cout << d << " ?= " << int(d) << endl;
// 435 ?= 434
```

real calcul done with finished precision in its bin image\
-> result:
```cpp
cout << setprecision(20) << d << endl;
// 434.99999999999994316
```

**Implicit convert.**\
can mix type, however BEWARE of shitty results

exemple: \
auto x = 5 * 3.14F + 5.3e-2;\
        int  float   double\
         |     |        |\
     float--*---        |\
            |           |\
          float         |\
            |           |\
          double        |\
            |_____+_____|\
                double

Eval des express. selon *priorité des opé.*
1. Unaire (+,-)
2. Multiplicatif (*,/,%)
3. Additif (+,-)

Unaire -> apply if needed promo numérique int\
Express. +a & -a -> int si a == char or short signed or nah
```cpp
unsigned char a = 65;
unsigned short b = 1;
unsigned int c = 1;
cout << a << " " << +a << " " << -a << " " << -b << " " << -c << endl;
// A 65 -65 -1 4294967295
```

**For bin opé:**

NB promo int to type char or short signed or not\
    if opérande = long double convert the other in long double\
    same for double and float\
    et si bet. 2 int depend on signed or not and rank.\
    ( signed → unsigned )\
    ( int → long → long long )

int, long ---------------------------> long\
int, long long ----------------------> long long\
int, unsigned int -------------------> unsigned int\
int, unsigned long ------------------> unsigned long\
int, unsigned long long -------------> unsigned long long\
long, long long ---------------------> long long\
long, unsigned long -----------------> unsigned long\
long, unsigned long long ------------> unsigned long long\
long long, unsigned long long -------> unsigned long long\
unsigned int, unsigned long ---------> unsigned long\
unsigned int, unsigned long long ----> unsigned long long\
unsigned long, unsigned long long ---> unsigned long long

If better type -> can also win\
Depends on data model used by the pc

unsigned int , long\
unsigned int , long long\
unsigned long, long long\

If opérande signe can represent all val of unsigned opé\
-> unsigned convert into signed one

Else both are converted in unsigned type version of signed type

int et long use 32 bits and long long 64 bits *Windows*

unsigned int , long -> unsigned long\
unsigned int , long long -> long long\
unsigned long, long long -> long long\

int use 32 bits, long & long long 64 bits *Linux-MacOS*

```cpp
unsigned int a = 1; long b = 2;
unsigned long c = 1; long long d = 2;
cout << a - b << " " << c - d << endl;
// Linux-MacOS -> -1 18446744073709551615
// Windows -> 4294967295 -1
```

**Beware of comparisons**\
Opé rules for arithmétique applies also to opé de comparaison\
Will be troublesome if comparison of int signed and unsigned one:
```cpp
signed int a = -1;
unsigned int b = 1;
cout << boolalpha;
cout << (signed(-1) < signed(1)) << endl;       // True
cout << (unsigned(-1) < unsigned(1)) << endl;   // False
cout << (a < b) << endl;                        // False
```

