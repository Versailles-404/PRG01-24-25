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



































