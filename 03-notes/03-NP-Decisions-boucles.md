# 30.09.2024

Bloc de code pour former une instruc. composé\
{} only required\
Décla can have its own décla. de var.\

Var décla in bloc != visible outside of it

*Bloc imbriqué*\
Works as one instruc.\
Can include other blocs\
Indentation ignored par le compil. only helps the stoopid hooman goblin\
Si var have same name in bloc imbriqué, only the most imbriquée visible\
-> masque les autres\

:: -> to recup var global\

Flux d'entrée -> lecteur du clavier\

## If … Else

```
else if possible
if(x<0){
}
else if ( x == 0) {
}
else{
}
```

?
See msg de Chris

id what's common first, then condition then what it returns
```
if(a<0)
{
b+= a;
} else{
b-=2*a;
}

b+= a>0 ? a : +2*a

if(a>0)
{
b+=1;
}else if(a==0){
b=0;
}else{
b*=2;
}

b=a>0 ? b+1 : (a == 0 ? 0 : 2*b)
```
## Switch
-> break et fallthrough

Only == can't < or >

Ordre des cases et default: belec for syntax
But for logic changes everything
Si default
-> vérif. default
Si rien rien -> belec du truc

Si no break -> will exe everything will not care abt the thing
-> fall through



enum type
->

## If constexpr

condition ré-évaluable

# 01.10.2024

# Boucles

## While

{init; while(condition) {instructions; actions;}}

exemple
```
int i = 4;
while(i != 4){
cout << --i;
}
```
    3210

if condition never true -> never goes into he while

## For

for(init.; condition; action){\
}\
all optional\

int i = 0 -> temporaire, only in the for, not outside


-> parcourir un intervalle [a;b[
(Tester-Init-Incrém.
-> groups it in 1 & ++ lisible

## Do-While

do instruction/s répétée/s; while (condition)\
si condition du while fausse, -> fall through\

**Debugging**\
-> suivi manuel\
-> debugger\
-> point d'arrêt

---------------
**Boucles imbriquées**\
-> parse tableaux en 2D\
the more imbriqued loop, the more dimension for the tab

on peut utilisé la , pour ajouter des actions, init. et conditions

## SAUTS

break;\
continue;\
goto ETIQUETTE:








































