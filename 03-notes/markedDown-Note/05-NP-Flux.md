28.10.2024

# Flux

## 1. Introduction aux flux d’entrée / sortie ( I/O streams)

Flux => canal for data exchange\
*input/output*\
Can be connected to perif. ou file


Source == always the same.\
Tuyau == tu peux arroser de plein de manière différente, mais ça reste de l'eau\

Tuyau can have multiple func.\
-> warm water\
-> change its color

**Attr. format.**
*left*
*right*
*boolalpha*

**Flags d'états:**\
*goodbit* -> alles klar\
*failbit* -> erreur logique\
*eofbit* -> end of file -> can't file it anymore\
*badbit* -> erreur irrécupérable

If closed -> still water inside\
(source indispo)\

Flux standard:
- cin
- cout\
(memoire tampon -> buffer)\
-> endl == retour à la ligne qui vide le buffer (implicite *flush*)
- cerr
- clog

Opé insert = << in exit flux

Opé extract = >> in entry flux

Both retournent une réf au flux concerné

## 2. Sortie et entrée standard 

### <"iostream>

- inclut <"ostream>\
-> entrée standard == clavier => console\
*can be redirected*

std::cout\
std::cerr -> print quickly bcs errors == emergencies\
std::clog -> print slowly bcs un journal peut se lire plus tard 

std::cin 

- standard input like keyboard
- need a var to store the input
- end input by **Enter**
- can put more than one\
-> either sep. by a space or enter

## 3. Lire et écrire des fichiers

### <"fstream> - W/R files
.bin & .txt\

Inherit from stream previously seen but for files

*Bonne pratique :*
1. **Ouvrez** le fichier avant de toute autre opération
2. **Ecrivez & || lisez** des données aves les opérateurs << ou >>
3. **Fermez** le fichier une fois vos opérations terminées

**std::ifstream** pour la lecture\
Input File stream\
**std::ofstream** pour l’écriture\
Onput File stream

**std::XXstream**\
IN/OUT-put at the same time

### <"ofstream>

Mode "OUT" par défaut:\
si inexistant -> crée\
si file créé -> écrase le contenu etou le fichier

- default flag -> *failbit*

.open -> open the file (duh...)
.close -> yeet physically the buffer content into the file

*append* -> **std::ios::app** ou **ios::app**\
Ajoute sans écraser !

### <"ifstream>

To read -> **std::ifstream**

**std::getLine**(var w/ the filename, str qui contiendra la ligne)\ 
-> lit par ligne le content du file .txt

Exemple: 
```cpp
#include <iostream> // std::cout
#include <fstream> // std::ifstream
#include <string> // std::string, std::getline

int main() {

std::ifstream file_in;

//ouvrir le fichier en lecture
file_in.open("sample.txt"); 

// Tant qu'il reste encore des choses à lire 
while (file_in) {
std::string une_ligne;

// Lire une ligne à la fois
std::getline(file_in, une_ligne); 
std::cout << une_ligne << '\n'; 
}

// fermer le fichier
file_in.close();

}
```

**std::get** -> récup. all char but only char

.open & .close -> not required to do so /!\ \

Exemple *w/*:
```cpp
std::ofstream file_out;

file_out.open("sample.txt");

file_out << "contenu du fichier\n";

file_out.close();
```

Exemple *without*:
```cpp
{// ouverture par initalisation
std::ofstream file_out("sample.txt");

// fermeture par sortie de scope
file_out << "contenu du fichier\n";
} 

```
Close w/ -> bonne pratique car manuel donc control

On peut mixer les deux ensembles:
```cpp
// ouvrir implicitement le fichier
std::ofstream file_out("sample.txt", std::ios::out);

// y écrire quelques lignes
file_out << "Ceci est la ligne 1\n";
file_out << "Ceci est la ligne 2\n";

// fermer explicitement le fichier 
file_out.close(); 

// Oups, nous avons oublié quelque chose
// réouvrir explicitement le fichier en mode append
file_out.open("sample.txt", std::ios::app);
file_out << "Ceci est la ligne 3\n";

// refermer explicitement le fichier 
file_out.close();
```

### Redirection de flux

Redirect. flux cin, cout, cerr, et clog d’un programme to files w/ cmd line w/  options *<, 1> et 2>*\
Exemple:\
*prog.exe < input.txt 1> out.txt 2> error.txt*

**<** redirect. input flux cin to read from file input.txt\
**1>** redirect. output cout to file out.txt\
**2>** write output cerr & clog in file error.txt

If redirect. output in *append* mode use of **>>** or **<<**:

*prog.exe < input.txt 1>> out.txt 2>> error.txt*

Each flux (!error) -> buffer\
buffer == also var == same shit

Can be redirect. -> changing of buffer used by the flux

rdbuf witouht args -> return ptr toward the flux\
rdbuf w/ args -> spec. new buffer like one of another flux

-> usable on every type of flux

Exemple:

```cpp
std::ofstream file_out("sortie.txt", std::ios::out);

// backup du buffer de cout
auto backup = std::cout.rdbuf();

// rediriger cout vers le fichier 
// en remplaçant son buffer par celui de file_out
std::cout.rdbuf(file_out.rdbuf());
std::cout << "Ligne écrite dans le fichier \n";

// remettre son buffer d'origine
std::cout.rdbuf(backup);
std::cout << "Ligne affichée sur la console \n";

file_out.close();
```
fstream fichier("exemple.txt", ios::in | ios::out | ios::app)\
-> ouverture hybrid + no stash

.seekg -> rewind (change pos.)

## 4. Lire et écrire des chaines de caractères

### <"sstream> -> stringstream

Flux where W/R in string instead of console\ 
Goes nowhere physically, still in memory, but not the same as cin

Access -> str()

All opé on cin && cout appiable

- allows to convert a nb into str and reverse
- output buffer to ulterior print
- or treat input line by line

No connect to anything, only to str, more powerful to treat str\


Exemple:\
Convert nb to str
```cpp
int nombre = 123; // nombre a convertir

stringstream convert; // flux de conversion

convert << nombre; // affichage comme pour cout

string chaine = convert.str(); // chaine contient "123"
```

Convert str to nb

```cpp
string text = "456"; // chaîne a convertir

stringstream convert(text); // flux de conversion

int nombre;

convert >> nombre; // nombre contient la valeur 456
```
Conversion nb to str:
- str -> int **stoi**
- str -> double **stod**
- nb -> str **to_string**

Exemple:
```cpp
int entier = stoi("123");
double reel = stod("3.14");
string chaine = to_string(entier) + " " + to_string(reel);
// chaine contient "123 3.140000"
// to_string ne permet pas de choisir le format
```

## 5. Sortie formatée

### <"iomanip>

Sortie == formatable through manipulateurs:\
2 libs : <ios> & <iomanip>

*En-tête Manipulateur Explication Persistance*\
Ne tronque pas le contenu
*proceeds to store back the guillotine I was taking out*
*angry French noises*

Persistance == will keep the format
Non-persistant == will go back to normal asap

<"ios>\
Non-param - already included in <"iostream>\
-> does not take any param.

internal - Just. left sign of nb -> nombre & right val\  
Persistant -> Oui\
left - Just. on the left sign+nb\
Persistant -> Oui\
right Just. on the right sign+nb\
Persistant -> Oui

- fill on the right if **left**
- fill on the left if **right**
- fill bet. sign & nb **internal**

<"iomanip">\
To be included for manip. param\
-> does take param.

setfill(char) Définit le paramètre comme caractère de remplissage\ Persistant -> Oui\
setw(int) Définit la largeur du champ\ 
Persistant -> Non

```cpp
int a = -12345; int wcol = 10; cout << "0123456789" << endl; 

cout << a << endl; // formatage par défaut

cout << setw(wcol) << a << endl; // colonne de 10 char

cout << left << setw(wcol) << a << endl; // justifié à gauche 

cout << right << setw(wcol) << a << endl; // justifié à droite (choix par défaut)

cout << internal << setw(wcol) << a << endl; // justifié interne

cout << setw(wcol) << a << endl; // left, right, internal persistent

cout << a << endl; // setw ne persiste pas. s'applique à 1 seul affichage

cout << setfill('*') << setw(wcol) << a << endl; // char de remplissage autre que ' '

cout << setw(wcol) << a << endl; // setfill persiste

cout << "Rempli avec " << cout.fill() << endl; // .fill() retourne le char de remplissage
```

**std::flush & std::endl**

*std::flush* force empty buffer to exit

*std::endl* == **\n + std::flush**\
If only retour ligne required, \n is enough

**std::boolalpha**

print bool... WAW PTN ;-;

behaviour can be modified w/ modif. de flux

*std::boolalpha* et *std::noboolalpha* == **Persistant**

```cpp
bool vrai = true, faux = false; 
cout << vrai << " " << faux << endl; //1 0

cout << boolalpha; 
cout << vrai << " " << faux << endl; // true false

cout << noboolalpha;
cout << vrai << " " << faux << endl; // 1 0
```

## 6. États des flux et validation des entrées

### User input manag.

if user input != int when int requested -> *can't eat it.*\
var put back to 0 then try to re-read the shit. Until they get it\
creates a fucking infinite loop
(BAH BRAVO NILS...) so even programming language can be allergic to smth... -.-'

**How to manag. input errors**
1. Detect. error
use the flags
    - cin.good()
    - cin.bad()
    - cin.eof()
    - cin.fail()
2. Wipe indic.
use cin.clear()
3. Empty buffer
cin.ignore(streamsize n, int delim = EOF)\
Yeet until the n char is reached or until the delim char\
(default == end of file)

**The cooking recipe to handle the user's shit**
```cpp
cin >> valeur;
if (cin.fail()) {
cin.clear();
cin.ignore(numeric_limits<streamsize>::max(), '\n');
}
```

**Detect. test of user's shit can also be written this way**
```cpp
if (not cin.good()) ...

if (not cin) ... 
// car la conversion de cin en bool équivaut à appeler .good()

if (not (cin >> valeur)) ... 
// car l'expression (cin >> valeur) retourne cin
```

## 7. Fonctions utiles

*>> used to read std::string*\
will passe any blank\
smash only when char, smash is racist
not always appropriate (WAW PTN RACISM IS NOT APPROPRIATE... -.-')

```cpp
stringstream in(" \n \t Hello, World ! ");

// int i  = 0
int i{};

// init. default == empty
string s;

while (in >> s) {

cout << ++i << " : " << s << endl;
/*
1 : Hello,
2 : World
3 : !
*/
}
```
```cpp
string str;
cin >> str; // l'utilisateur entre "James Bond"
cout << str << endl; 
// will print James which is not what we want...
```
How to patch -> *std::getline*\
**getline(flux, str)**

```cpp
string str;
getline(cin,str); // l'utilisateur entre "James Bond"
cout << str << endl;
// will print the whole shit
```

Third param to spé. char of teminaison other than *\n*

```cpp
stringstream in("James Bond/John Doe/Jack Smith");
int i{};
while (not in.eof()) {
string name;
getline(in, name, '/');
cout << ++i << " : " << name << endl;
}

/*
1 : James Bond
2 : John Doe
3 : Jack Smith
*/
```

char not included in st but deleted from flux

**istream::get(char)**\
allows to read flux of char one by one

```cpp
stringstream in("Une ligne avec des blancs\nUne autre ligne");
char c; 
while (in.get(c)) { cout << c; }
/*
Une ligne avec des blancs
Une autre ligne
*/
```
```cpp
stringstream in("Une ligne avec des blancs\nUne autre ligne");
char c;
while (in >> c) { cout << c; }
// UneligneavecdesblancsUneautreligne
```
Effect to contrast with opé >> smash racist

**istream::get()**\
Return readed char, non-racist smash


**istream::unget(), istream::putback(char)**
*Replace the char*\
Unget() put back la char read in flux to be read next time
```cpp
stringstream in("abcdefg");
char c; in.get(c); cout << c << endl;
in.unget();
while(in.get(c)) cout << c;
```

putback() **replace the char litterally**\
the char read is exchanged by the one given in param in the flux
```cpp
stringstream in("abcdefg");
char c; in.get(c); cout << c << endl;
in.putback('Z');
while(in.get(c)) cout << c;
```
