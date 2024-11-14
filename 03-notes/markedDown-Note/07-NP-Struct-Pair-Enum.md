# struct, enum et std::pair

## struct
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

## Pointeurs

Access to members of a struct. -> instance name & member name sep. by a **.**\
(For r/w rights)
```cpp
// référence sur une date
Date& refDate = date1;
cout << refDate.jour;
refDate.jour = 12;
```
W/ ptr => address of a struct:
1. Dereferenced the ptr w/ *  to access the member with op. **.**

**.** comes before the *

HOWEVER ! (objection !)\

**->** opé => does both in order and enlight the syntax and the reading

```cpp
Date* ptrDate = &date1; // pointeur sur une date
cout << (*ptrDate).jour; // ( ) nécessaires
cout << ptrDate->jour;
ptrDate->jour = 12;
```

![img](/img/tab-struct-accessMember.png)

### passage de param Return

struct can be used like any other var -> can be used as param so can be returned\
Since it can be **composed of multiple feature/var** -> return more than 1 param\
LIKE A BATMAN, UNDER COVER ! It seems to be *one var returned*...
BUT ! TADAAAAA it's a *member of a struct* !

slide 11

### Comparaison
slide 12

##  std::pair<T1,T2>
From lib <'utility> and pair is a generic template\
Can ease task by dodging struct crea.\
TOO LONG to create a struct for smol shits (my chlong is jelly now...)\
Instead this below my friend, is way simpler/shorter
```cpp
pair<int,int> divmod(int numerateur, int denominateur) {
return {numerateur / denominateur, numerateur % denominateur};
}
int n = 42, d = 12;
auto qr = divmod(n, d);
cout << n << " / " << d << " = " << qr.first << endl;  // 42 / 12 = 3
cout << n << " % " << d << " = " << qr.second << endl; // 42 % 12 = 6
auto [q, r] = divmod(n, d);
cout << n << " / " << d << " = " << q << endl;         // 42 / 12 = 3
cout << n << " % " << d << " = " << r << endl;         // 42 % 12 = 6
```
Than creating a struct just to hold to bitched together:
```cpp
struct { T1 first; T2 second };
```

**Definition**\
```cpp
// Le record mondial absolu est de 56,7°C. Il a été établi à Furnace
// Creek, dans la vallée de la mort, en Californie, le 10 juillet 1913
pair<Date, double> Furnace_Creek{{10, 7, 1913}, 56.7};
pair<Date, double> record_mondial = Furnace_Creek;
cout << "Record de " << record_mondial.second
<< " degrés en l'an " << record_mondial.first.annee << endl;
auto [date, temperature] = Furnace_Creek;
auto [jour, mois, an] = date;
cout << "Record de " << temperature
<< " degrés en l'an " << an << endl;
// Record de 56.7 degrés en l'an 1913
```

## enum
Good to fight magic nb\
Décla way:
```cpp
enum [ nom_de_type ]
{ const_enum [ = expression ]
[ , const_enum [ = expression ] ... ]
} [ identificateur [ , ... ] ];

```
*nom_de_type* -> optionnal\
gives a name to type enumered -> reusable later\

*const_enum*\
bet. {} -> list all const enumerable possible

*=expression* -> optionnal\
gives int val equival. to enum const\
Defauolt -> 1st const == 0 next one are ++ each

*identificator* -> optionnal\
post }, decla. var.

Examples:
```cpp
enum Saison {PRINTEMPS, ETE, AUTOMNE, HIVER};
enum Saison saison1, saison2; // comme en C

enum Saison {PRINTEMPS, ETE, AUTOMNE, HIVER };
Saison saison1, saison2; // pas valable en C

enum Saison {PRINTEMPS, ETE, AUTOMNE, HIVER}
saison1, saison2; // une seule ligne

enum {PRINTEMPS, ETE, AUTOMNE, HIVER} saison1, saison2; 
// si on ne réutilise pas le type
```

**Affectation**\
Examples:
To affect ETE to saison1:
```cpp
saison1 = ETE;
saison1 = saison2; // si saison2 vaut ETE;
saison1 = (Saison)1; // PRINTEMPS = 0, ETE = 1, ...
saison1 = Saison(1);
```
But not 
```cpp
saison1 = 1; // possible en C
```
Convert. type enum -> int does implicitely
```cpp
int entier = saison1; // entier vaut 1
int entier2 = ETE; // entier2 vaut 1
```

Limits:\
- no verif. when convert.
```cpp 
enum Saison {PRINTEMPS, ETE, AUTOMNE, HIVER};
Saison saison1 = Saison(12); 
// valide, mais seules les valeurs de 0 à 3 ont un sens.
```
- const of enum can't be reused
```cpp 
enum Couleur {VERT, ROSE, BLEU};
enum Fleur {MARGUERITE, ROSE, VIOLETTE};
/*
error: redefinition of enumerator 'ROSE'
enum Fleur {MARGUERITE, ROSE, VIOLETTE};
                        ^
note: previous definition is here
enum Couleur {VERT, ROSE, BLEU};
                    ^
*/
```
**enum class**\
Dif. -> marry the content to the class.\
Yeet ambiguity !\
no convert implicit anymore but explicit possible
```cpp
int entier = saison1; 
/*error: cannot initialize a variable of type 
'int' with an lvalue of type 'Saison'
int entier = saison1; 
    ^ ~~~~~~~
*/
```
```cpp
int entier = (int)saison1; 
// explicit way to convert
```
Unlike enum classic w/ enum class -> id const can be reused
```cpp
enum class DirH {GAUCHE, CENTRE, DROITE};
enum class DirV {HAUT, CENTRE, BAS};
DirH horizontal = DirH::CENTRE;
DirV vertical = DirV::CENTRE;
```

**Comparaison & param**

enum & enum class == int\
Comparaison-> natural

```cpp
enum class DirH {GAUCHE, CENTRE, DROITE};
bool meme_direction (DirH lhs, DirH rhs) {
return lhs == rhs;
}
```
param can be done by copy or ref if needed\
can return enum or enum class
```cpp
Jour prochain_jour (Jour jour, int n = 1) {
return (Jour)(((int)jour + n) % 7);
}
```