# 03.10.2024

# Fonctions

Made to have one bloc instead of many doing the same shit.\
-> just need to call the func and give it param.\
instead of a shit load of line -> only 1

## Passage par valeur

When call of func and given param in () -> conversion to make it enter correctly in the container.\
ordre d'éval indéfini

## Passage par réf

int& a -> réf

Si on passe une réf, réf == synonyme so it will be applied to the shit given when we'll call the function\
Allows to have param d'entrée et de sortie\
Unlike passage de valeur -> can't give another type from the func or only 1 of the 2 if it asks for 2.

-> danger ! can potentially write on r/unallaowed (shall not change) part of the memory !\
EXEMPLE:
 
```
void echanger(int& a, int& b) { 
        int t;
        cout << "debut echange: a = " << a << " , b = " << b << endl;
        t = a; a = b; b = t;
        cout << "fin echange : a = " << a << " , b = " << b << endl;
}
int main() {
    int c = 3, d = 5;
    cout << "avant echange: c = " << c << " , d = " << d << endl;
    echanger(c, d);
    cout << "apres echange: c = " << c << " , d = " << d << endl;
    return EXIT_SUCCESS
}
```

avant échange: c = 3 , d = 5\
début échange: a = 3 , b = 5\
fin échange : a = 5 , b = 3\
après échange: c = 5 , d = 3

## Passage de ptr/addresse

If given an adress in a func. must tell it the type of what's at the address\
(must say to Théodore what to bring to the places he'll go)\
-> allows more magouille than réf\

when func. called, must give address as well\
*func(&a, &b)*

Plus moche avec des ptr que des réf, mais ++ powerfull at least\

# 03.10.2024

# Fonctions - suite

Conversion des types when pass of values\
Dolce vitàààààà

```
void afficher(int p1, char p2) {
cout << "p1 = " << p1 << " , p2 = " << p2 << endl;
}
int main() {
const char CAR = 'A';
afficher(1, 'A');
afficher(1, 65);
afficher('A', 67);
afficher(CAR, CAR + 1);
return EXIT_SUCCESS;
}
```
Va afficher :\
p1 = 1 , p2 = A\
p1 = 1 , p2 = A\
p1 = 65 , p2 = C\
p1 = 65 , p2 = B

HOWEVER w/ réf :\
```
void f(int& p1, char& p2) {}
---------
toto = 3
tata = 6
void f(toto, tata){
    toto+=tata;
    tata*=toto;
}
cout << toto << " " << tata << endl;
toto = 9
tata = 18
```

with & will modify the chosen var\
-> cannot give the wrong type of var to the func.\
else -> ERROR\
Same for const -> cannot be modified mf... give the RIGHT type if const give const type, if type then type

Les chats font pas les chiens.

if void f(const int& p1, const char& p2) {}

-> passage par val == copie mais pas de copie si on utilise des réf\
si wrong type -> copie convertie

### Types des paramètres lors du passage par référence constante
Avec le passage par référence constante, on peut transmettre sans copie

des variables du même type\
des constantes du même type\
des constantes littérales du même type\

On peut également transmettre, au prix d’une conversion et copie dans une variable temporaire cachée

des variables de type convertible\
des constantes de type convertible\
des constantes littérales de type convertible\
et de manière générale, toute expression de type convertible

## Return

Interrompt la fonction -> instruc. post return never exe\
Si plusieurs return -> can be used with switch et if\
Can be used alone -> just stop the prog.\
Return réf




























