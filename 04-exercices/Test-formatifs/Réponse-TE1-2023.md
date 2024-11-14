# Exercice 1
## 1.1 
4/5*5./3. = **0**
(5/3)*(3.0/2) = **1.5**
7/2.*2/7 = **1**

*correction: 0 1.5 1*

## 1.2
1st loop 2x
2nd loop -> 2x
-> 4x
1st 0 +1+1 ->
2nd 2 +2 +2 -> **6**

*correction:*
*1st 0 +1 -> 1*
*2nd 1 +2 +2 -> 5*

## 1.3 
8+12-> **20**
*correction: mauvaise lecture du chevron...*
*donc c'est l'autre condition qui s'applique*
*-> 4*

## 1.4
**5**

*correction: 5*

## 1.5
nothing

*correction: Pas de sortie*

## 1.6
- funk: incrément -> incrément une val + retourne un bool en true 

result -> **true_**

*correction: 1 0*
*print pas de false ou true, ça print 1 ou 0*
*il faut un truc de plus pour print de "false" ou "true", sinon print en chiffre donc 1 ou 0*

## 1.7 
123456789
**W-X-Y-Z-Z-Z-Z-Z-Z-**

*correction: WX-X-YZ-Z-Z-Z-Z-Z-Z-*
*LE PUTAIN DE BREAK WSH*

## 1.8
Loop -> 3x
i++ 3x -> 
D
DDD
**DDDDD**

*correction: DDD*
*on rajoute le résultat précédent à + str*

# Exercice 2
char -> table ASCII -> peut être considéré comme un nb car il en a un associé -> promo de char à int
## 2.1
char ou int

*correction: int*

## 2.2
float ou double

*correction: double*
*double est le type par défaut*

## 2.3 
double ou float

*correction: double*

## 2.4
int != float ou double

*correction: bool*
*si comparaison -> val de vérité donc bool*

## 2.5
int

*correction: bool*

# Exercice 3
## 3.1
Non

*correction: Non*

## 3.2
Oui

*correction: Oui*

## 3.3
Meh

*correction: Non*
*p3 -> pointeur constant -> peut pas changer d'adresse*

*si doute -> NON*

## 3.4
Oui

*correction: Non*
*point on int then to an immut. part of the memory*

## 3.5
Meh

*correction: Oui*
*ptr points on const int but ptr itself not a const*

# Exercice 4
```
#include < iostream >
using namespace std;

// Function specification after main
string getSeason(int mois);

int main() {
    int mois = 0;
    cin >> mois;
    cout << getSeason(mois);
    return EXIT_SUCCESS;
}

string getSeason(int mois) {
    // Code à compléter
    string season;

    switch(mois){
        case 1:
        season = "hiver";
        return season;
        case 2:
        season = "hiver";
        return season;
        case 3:
        season = "printemps";
        return season;
        case 4:
        season = "printemps";
        return season;
        case 5:
        season = "printemps";
        return season;
        case 6:
        season = "été";
        return season;
        case 7:
        season = "été";
        return season;
        case 8:
        season = "été";
        return season;
        case 9:
        season = "automne";
        return season;
        case 10:
        season = "automne";
        return season;
        case 11:
        season = "automne";
        return season;
        case 12:
        season = "hiver";
        return season;
    }
}
```