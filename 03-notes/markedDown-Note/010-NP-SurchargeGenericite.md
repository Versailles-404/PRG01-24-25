# Fonctions Surchargées et généricité

1. Func. overload
2. Généricité (func.)
3. Opé overload

## 1. Func. overload
Means 2 func. same name but dif. params\
**Signature func. == carac. of its params**\
- nb param && order
- types && pass. style (val, réf or ref const)
-> Compilateur will call following effective param rather than formal ones of candidate funcs.

**Those don't help to diff. 2 overloads**\
- return type
- default val.
- const of paramt passed as val.

```cpp
int add(int lhs, int rhs=0) {
return lhs + rhs;
}
```

```cpp
short add(const int lhs, const int rhs) {
return short(lhs + rhs);
}
```

If 2 func. w/ same name only dif. by any of those 2 bitches:\
-> Compilateur (Théodore) will scream to death\
"error: functions that differ only in their return type cannot be overloaded"\
WHICH MEANS: **decla error on 2nd func.**

![img](/img/call-overload-func.png)

Which overload called:
- 0 func. called *(f(vector<'int>(4)))* → erreur de compilation
- 1 func. called *(f("hello"s))* → elle est appelée
- 2+ func. called → which to pick ?\
Tries multiple criterias less strict each time it tries smth:\
-> if criteria select 0 func. -> less strict\
-> if criteria select 1 precisely -> called \
-> if criteria selects more than 1 -> erreur de compilation

### Criteria 1 : call without convert.
![img](/img/call-without-convert.png)

### ATTENTION PLS LADIES AND GENTLEMEN
![img](/img/attention-call.png)

### Criterias 2: simple convert.
![img](/img/criterias2.png)

### Criterias 3: promotion
![img](/img/criterias3.png)

### Criterias 3: type convert.
![img](/img/criterias4.png)

### Summary bcs fuck this
Compil. will always search best match by testing the order
- exact match
- simple convert. match\
->var into const.\
-> tab into ptr.
- promo. num. match\
-> bool, char, short => int\
-> float             => double
- convert. type match

Théodore will stop at 1st match found\
Ambiguity if multiple proto match the lvl

**ATTENTION BITCHES AND BROS**\
C++, unlike Java, best implicit convert !=exist
```cpp
void f(short n) {cout << "Appel de f(short n)" << endl;}
void f(long n) {cout << "Appel de f(long n)" << endl;}
int main() {
int n = 1;
f(n); // Erreur à la compilation. Appel ambigu
}
```
f(n) call == ambigu bcs degradant convert int -> short == same lvl as ajust type\

## Multiple params. func.
Will apply 4 criteries on each param stopping at 1st criterias matching\
Takes n of ensembles if it finds 1 func. precisely == call non-ambiguous

![img](/img/multiple-call-param.png)

# 2. Genericité (func.)
Allows to create model/template -> to make shit go generics\
Such as:
- func.
- class
- var
- alias of family types

## Décla.
```cpp
template <typename T>
T somme(T a, T b) {
 return a + b;
}
```

```cpp
int main() {
cout << somme<int>(10, 20) << endl;
cout << somme<double>(1.0, 1.5) << endl;
}
```
