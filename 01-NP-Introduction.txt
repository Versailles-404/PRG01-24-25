17.09.2024

Some history points - see pdf pptx

In order crea. prog. language :
⦁	Fortran - Formula Translator - 1954
⦁	Algol - Algorithmic Oriented Language - 1958
⦁	CPL - Combiened Programing Language - 1963
⦁	BCPL - Basic CPL - 196
⦁	B - yeet everything bcs of being so basic - 1969
⦁	C - comes after B, duh - 1972
Agnostique à la plateforme
⦁	C++ - lang. Orienté object - 1983
More history… Just look at those fucking slides.

Générique -> réutilisation intelligente du code
->same behavior for everything, knows how to behave in every cases
-> how to surcharger fonctions
_____________________________________
1st year
Sem 1 - C++ (PRG1)
Sem 2 - C++ (ASD) - C (PRG2)
2nd year
Sem 1 - Java (POO)
Sem 2 - C++ (POA)
______________________________________

Fonction main ->
⦁	Case sensitive. main is main
⦁	Obligatoire.
⦁	MUST (should… else u ain't gonna run it elsewhere) RETURN : int
⦁	Come compil. can return nothing but not in the norme 
(comportement indéfini)
-> where to put param in main ? Cmd line ? Will be put in main
For some v. should say what it is.
() no param

-> instructions inside main
cout = console out == console.writeline but instead of () -> 
cout << test << endl;
Very powerful - can be used for debugging
endl = end line == ; solo -> reoutr à la ligne et ; REQUIRED

main always return int
return = 0 -> EXIT_SUCCESS
return = 1 -> EXIT_FAILURE
Both from cstdlib
Use this to know in validation to see if code is working or nah
Also use { } to put instruc. of funct. inside like C# 
______________________________________

Magic number -> wtf
Valeur qui apparaîssent et le rendent ilisible -> PUT IT IN THE FUCKING CONST. 
______________________________________

Fichier d'en-tête -> librairie (lib) #include <librairie>
On va pas réinventer la ptn de roue. TMTC, merci M. Deschamps
iostream -> can't print
cstdlib -> can't see if success or nah
After lib -> namespace
Ex: using namespace std;
Espace de nommage (?) = to be sure the name is correct and the function is well identified, like a last name.
STD == standard
Allows to separate dif. function with the same name
______________________________________

Editeur de liens ? -> Linker
Compilateur donne du code objet
Editeur de liens en mange
Compilateur compile en langage machine pour que la machine comprenne
Can we exploit le code objet ? Must translate in what ?
Editeur de liens takes all files and creates link between everything and produce an exe to be executable
Also takes the lib in 

Beware of the réf. from libs and namespaces
Si erreur de l'éditeur de liens -> erreur dans les appels des fonct. De lib et de namespace
______________________________________

Si exécution and still error -> erreur dans le code (proba dans l'algo)
Si pas d'erreur, alles gut !
______________________________________

Normalement de nos jours, ils sont fusionnés, le compilateur avec l'éditeur
______________________________________

G++ -c file -> return .cpp file ->  ou .o pas encore executable -> show erreur de compilation

If file .o -o file.exe -> translate it

Selon - on peut avoir plusieurs avertisseurs
______________________________________
19.09.2024

CMakeLists.txt -> config proc. Compil.
(call files kinda like .ps1)
Beware of filepath & name ! -> in this file
______________________________________

Errors ->

Syntax -> fucking code othrographe (like that ptdr…)
; -> end of a line (order) think abt telegraphe -> stop. To each line to finish it
Snowball the shit
->NE COMPILE PAS

Link -> if main not found or anything called in the prog.

Exceptions -> execution fault - big shit big time - break the prog. (BAJ BRAVO NILS, SUPER POUR LA CAMERA)
Try to open inexistant resources but called in prog -> error
Si on essaie de lire un endroit de la mémoire, mais que c'est déjà attribué, surtout hors programme -> erreur
->COMPILE MAIS PAS EXECUTABLE

Segmentation fault -> GOLD shiny big time en sécu -> tentative de r/w smwh à un endroit interdit (oh nio so dramatiiiiic)
Pointeur - bête noir (ASKIP)
frr, t'attribue, tu utilises, tu nettoies et pis voilà ptn, laisse rien trainer, just beware of the fucking leaks. Comme la lessive enft ou une map d'une ville/un immeuble

Runtime -> erreur d'execution ou de logique
Ça compile MAIS, "hollo wolrd is koay" mais si c'est pour SpaceX un peu moins (faute de frappe, best boi du TDAH bitch -.-')
Relire le code et chercher les problème de logique -> THE hardest one T-T (askip, selon le prof)
->COMPILE, EXECUTE MAIS PAS CONFORME
______________________________________

Si ça compile pas de ouf, mais sur la bonne voie -> point partiel ;-; (yay)
Mais si c'est de la chance tu te fais niquer T-T 
______________________________________

Explication du pseudo-code
______________________________________
