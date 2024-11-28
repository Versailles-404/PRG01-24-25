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
Multiple func. can have same name\
-> BUT profile must have nb & order of types in param\
To deter. which one to pick

```cpp
int somme (int a, int b) {
    return a + b;
}
double somme (double a, double b) {
    return a + b;
}

int main() {
    cout << somme(10, 20) << endl;
    cout << somme(1.0, 1.5) << endl;
}
```
**HOWEVER** tin tin tiiiiiiiiiiiiiin

To dodge issue on duplicated code of func. like above:
```cpp
// Décla template, T == var type 
template <typename T>
// Can guess the type, very shiny, indeed... but will be troublesome lmao
T somme(T a, T b) {
    return a + b;
}

// So the main will look like this with a template:
int main() {
    // <int> => type T of the template
    cout << somme<int>(10, 20) << endl; 
    // <double> => type T of the template
    cout << somme<double>(1.0, 1.5) << endl;
}
```
Kinda an overloader of func. without having to write it multiple times\

**BUT** it never all shiny and paquerettes... u know life quoi..\
SO. Here are the issues of doing that bcs life and prog are bitches:\

### THE DECLA. & DEF.
Goes in pair to make the func. generic
- before func. -> **template**
- followed by typename generic **<'typename T>**\
*typename might be replaced by class in old code*

typename in list of param generics can be used like any other type\
-> décla. (param, return type)\
-> in the def. body

```cpp
// déclaration
template <typename T> 
void echanger(T& v1, T& v2);

// définition
template <typename T> 
void echanger(T& v1, T& v2) {
    T temp = v1;
    v1 = v2; 
    v2 = temp;
}
```

### Instanciation

- Def of a func == only a moule ain't gonna give u cake if you don't make it/use it
- Compile. a file containing only déf. généric\
-> don't give any code lmao
- To make compile generate code:\
-> MUST instancier func. generique with effective types

```cpp
/*
1. Implicit call of func. with specified type or nah
-> if unspecified types , will be deducted from args
*/
int main() {
int a = 0, b = 1;
echanger<int>(a, b); //
// instanciation implicite, avec spécification du type,
// et appel de echanger<int>(int&, int&)
}

// Explicit instance by décla.
template void echanger<int>(int&, int&);
```

### Params
Can have multiples generic params sep. in the list by *,*\
```cpp
template <typename T, typename U> 
void f(T v1, U v2) {
…
}
```

Such a func. instancies itself by spé. effective types wanted sép. by ,
```cpp
template void f<int, double>(int, double);
```

If we give liess types than in instanciation -> **déduc. args**

**Not required** to spé. effective types wanted -> can be **deducted from context**
```cpp
template <typename T> void echanger(T& v1, T& v2);
```

Can be instan. explicitely like that:

```cpp
template void echanger<>(int&, int&); // T=int est déduit
template void echanger(char&, char&); // T=char est déduit
```

Or implicitely without any type

```cpp
int a = 0, b = 1;
echanger<>(a, b); // deux versions possibles pour
echanger(a, b); // l'instanciation et l'appel de
// echanger<int>(int&, int&)
```

**FOR IMPLICIT INSTAN.** by func. call\
-> can spé. or not val. by typenames\
- all
- only the firsts
- none (<'> == optional)

```cpp
// unspéc. val. will be deducted
template <typename T, typename U> void f(T v1, U v2) { … }

// T = int, U = double (et a et b peuvent être convertis)
f<int, double>(a, b); 

// T = int, U sera déduit du type de b (et a peut être converti)
f<int>(a, b);

// T et U seront déduits des types de a et b
f<>(a, b);
```

### Deduction


```cpp
template <typename T1, typename T2, typename T3>
void f(P1 p1, P2 p2, P3 p3, P4 p4);

int main() {
    A1 a1; A2 a2; A3 a3; A4 a4;
    f(a1, a2, a3, a4);
}
```

-Args generic Ti: 
-> T1 = T\
-> T2 = U

Func. params Pi 
P1 = const vector<'T>
P2 = pair<'T, U>

Effective params Ai
A1(v) = vector<'int>
A2(p1) = pair<'int, double>
A2(p2) = pair<'double, int>

```cpp
template <typename T, typename U>
void f(const vector<T>& v, pair<T, U> p);
int main() {
    vector<int> v;
    pair<int, double> p1;
    pair<double, int> p2;
    f(v, p1);   // 1: vector<int> = vector<T>
                // -> T = int, U non spécifié
                // 2: pair<int, double> == pair<T, U> 
                // -> T = int, U = double
                // 1 ∩ 2: T = int, U = double -> OK
    f(v, p2);   // 1: vector<int> == vector<T> 
                // T = int, U non spécifié
                // 2: pair<double, int> == pair<T, U>
                // T = double, U = int
                // 1 ∩ 2: impossible pour T
                // -> erreur de compilation 
}
```

**ATTENTION DOGGOS AND CATTOS**

W/ déduc. generic param -> **ALWAYS EXACT TYPE which is passed**\
*Théodore can't déduc. AND convert at the same time*

```cpp
template <typename T> 
void f(T v1, T v2) { … }
int main() {
    int i1, i2;
    double d1, d2;
    // f<int>(int,int)
    f(i1, i2); 
    // f<double>(double,double)
    f(d1, d2); 
    // erreur de compilation
    f(i1, d1); 
    // f<int>(int,int) avec conversion de d1 en int
    f<int>(i1, d1); 
    // f<double>(double,double) avec conversion de i1 en double
    f<double>(i1, d1); 
}
```

Déduc. not possible for args if not a param of the func.\
All args non-déduc. -> MUST be explicitely spé in instan.

```cpp
template <typename To, typename From>
To convert(const From& val) {
    return (To) val;
}
int main() {
    double d = 0.5;
    int i = convert<int>(d); 
    // convert<int, double>(double);
    int i = convert<>(d); 
    // ne compile pas
}
```

### Default params
Can spé val by default to generic params
```cpp
template <typename To = int, typename From = int>
To convert(const From& val) {
    return (To) val;
}
```

Not oftenly used for generic func. bcs déduc. args is prio. over default val.
```cpp
double d;
convert(d); // convert<int, double>
convert<int>(d); // convert<int, double>
convert<int, int>(d); // convert<int, int>
```

Can be useful for not-déduc. params
```cpp
template <typename From, typename To = float> // ordre inversé
To convert(const From& val) {
    return (To) val;
}

double d;
convert(d); // convert<double, float>
convert<int>(d); // convert<int, float>
convert<int, int>(d); // convert<int, int>
```
Overload of func. allows to get same result naturelly

**HOWEVER** widely used for generic classes like\
*std::stack* décla. like this:
```cpp
template <typename T, typename Container = std::deque<T>> class stack;
```

### Overload of generic func.
Like for classic func. -> overload possible\
How to differenciate them:
- nb params (bewary of default val.)
- params types
- réfs.

Can also give same name to simple func. and to generic func.
```cpp
template <typename T> 
void f(T);

template <typename T> 
void f(T, T);

template <typename T> 
void f(T, int);

template <typename T, typename U> 
void f(T, U&);

template <typename T, typename U> 
void f(T, const U&);

void f(int, float);
```

### Resolution
If specifies explicitely generic params when call of overload func.\
-> Resolution == follows exactly same rules as for classical func.\

Exemples call to f<'long>(i):
- has to choose bet. e f<'long>(long&) & f<'long>(const long&)
- selects 2nd bcs no convert of int& to long&

```cpp
template <typename T> int f(T&) {
    return 1;
}
template <typename T> int f(const T&) {
    return 2;
}
int main() {
int i = 42;
    cout << f<long>(i); // 2
    cout << f<int>(i); // 1
    cout << f<int>(42); // 2
}
```

**W/ deduc. of generic params**\
Below, *f(v)* can call:
- func. 1 with T = vector<'int>
- func. 2 with T = int

Overload resolution picks func. 2 bcs 1st param (vector<'T>) == ++spécialised than func. 1 (T)

Param généric P1 ++specialised than P2:
- foreach param efective that allows f(a) to call f<'T>(P2)
- f(a) can also call f<'T>(P2)
- BUT NOT IN REVERSED

```cpp
template <typename T> 
int f(T) { return 1; }

template <typename T> 
int f(vector<T>) { return 2; }

int main() {
    vector<int> v(42);
    cout << f<vector<int>>(v); // 1
    // seule appelable si T = vector<int>
    cout << f<int>(v); // 2
    // seule appelable si T = int
    cout << f(v); // 2
    // les 2 fonctions sont appelables, 
    // mais P2 est plus spécialisé que P1
}
```

### Specialisation 
- *f1 ++ spé than f2* -> ensemble effectives params able to call f1 is a sub-ensemble of f2
- *2,3 & 4* ++spé than *1* -> all func. that can call them can also call *1*
- *4 ++spé than 3* -> all func can also call *3*
- *none ++spé**\ 
-> bet. *2 & 3* nor bet. *2&4*\
-> however -> no issue of resolution bcs n == void

```cpp
template <typename T> void f(T) {...} // 1
template <typename T> void f(T*) {...} // 2
template <typename T> void f(vector<T>) {...} // 3
template <typename T> void f(vector<vector<T>>) {...} // 4
```
![img](/img/Ensembles.png)
