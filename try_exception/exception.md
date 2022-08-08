


Salut les amis, aujourd'hui nous allons parler des **exception** en python. Oui des **exception** car, même si une instruction est syntaxiquement correcte, elle peut générer une erreur lors de son exécution **(exemple la division par 0, accés a un fichier qui n'existe pas, etc).** Les erreurs détectées durant l'exécution sont appelées des exceptions et ne sont pas toujours fatales: nous appredrendrons ici à comment les traiter dans vos programmes. Tout au long de ce tutoriel nous allons:

  1. montrer l'utilisation des blocs try-except, 
  2. l'utilisation des clauses *else* et *finally* dans une exception
  3. montrer comment un utilisateur peut déclencher une exception

  

## A. Utilisation des blocs try-exception

Lors de l'appel d'une fonction, l'interpreteur Python peut rencontrer des problémes qu'il n'est pas en mesure d'executer. Dans ces cas, il jette une exception et renvoie un message d'erreur. Par exemple, soit l'instruction définie comme suite:

 `val = int(input('Veuillez saisir un nombre entier'))`

Dans cette instruction on demande à l'utilisateur de saisir un nombre entier. Et supponsons un seul instant qu'il saisisse des chaînes de caractères contenant des valeurs alphabétiques ou des caractéres spéciaux; eh bien **Python** enverra un message d'erreur de type *«ValueError: could not
convert string to int… »* car la fonction **int()** ne permet de convertir que des chaînes constituer des valeurs en chiffres. Dans cette situation, on est face à une exception. Si cette exception n'est pas gérée par le programme dont l'instruction fait partie, le resultat est l'arrêt du programme avec affichage d'un message d'erreur. 

Mais, le langage python offre les possibilités au programmeur de contrôler les instructions pouvant générer des exceptions et de définir ses propres traitements d'erreur. Ces traitements sont basés sur l'utilisation **« try »** et **« except »**  qui figurent également parmi les *33* mots réservés de python. Les instructions susceptibles de générer des exceptions sont placées à l'interieur d'un bloc **« try »** et les instructions à exécuter en cas d'exceptions sont définies à l'intérieur d'un bloc **« except »**. 

un bloc **try** doit être accompagné d'au moins un bloc **except**. Plusieurs blocs except peuvent être associés à un même bloc **try**. Ainsi, un ensemble **try-except** s'ecrira de la forme:



```{r echo = TRUE, warning = FALSE}
try:
    instructions
except ErrorType1:
    instructions si ErrorType1
except ErrorType2:
    instructions si ErrorType2
except (ErrorType3, ErrorType4)
    instructions si autre erreur
```







**_NB:_** il existe 03 manières d'ecrire la ligne except:
 1. En indiquant le nom de l'erreur concernée. exemple: except Error:
 2. En indiquant un tuple contenant plusieurs erreur. Exemple: except (Error1, ..., Errorn):
 3. En n'indiquant rien. Exemple: except:
 

### 1. Indiquant le nom de l'erreur

**_Petit exemple_**: Demandons à l'utilisateur de saisir des valeurs et lui redemander une nouvelle fois la saisie afin qu'il entre une nouvelle valeur convenable.


```{r echo = TRUE, warning = FALSE}
try:
    val = float(input('Veuillez saisir un nombre :'))
except ValueError:
    print('La nouvellee entrée n'est pas valide')
    val = float(input('Veuillez recommencez s'il vous plait:'))
```
 
**Autre exemple** Dans cet exemple, essayons d'ouvrir un fichier en uttilisant la fonction **open()**. si le fichier n'est pas trouvé au chemin indiqué la fonction envoie une exception de type **IOError**. la gestion de cette exception permet l'affichage d'un message adéquat:


```{r echo = TRUE, warning = FALSE}
try:
    nomFichier = input("Entrez un nom de fichier : ")
    myFichier = open(nomFichier)
except IOError:
    print("Erreur de lecture du fichier")
    sys.exit()
```

**Remarque**: Il est également possible pour le programmeur de déclencher explitement une exception grâce à l'instruction **raise** «Nom d'une Exception», et aussi il est possible de définir de nouvelles pour des exceptions particuliers

### 2. En indiquent un tuple d'erreur

Une clause except peut nommer plusieurs exceptions sous la forme d'un tuple entre parenthéses.

```{r echo = TRUE, warning = FALSE}
try:
    instructions
except(ErrorType1, ErrorType2, ErrorType3):
    instructions si ErrorType1 ou ErrorType2 ou ErrorType3

```



### 3. En indiquant rien

**exemple**: Utilisation de l'instruction except avec l'instruction pass

Soit la liste x suivante:

x = ['North', '6.47', '4.03', 'Yorkshire', '6.13', '3.76', 'Northeast',
'6.19', '3.77', 'East', 'Midlands', '4.89', '3.34']

Les éléments de cette liste sont tous en caractéres. On souhaite alors convertir les élements en chiffres en format num"rique en utilisant la fonction float(). Nous choisissons alors d'élaborer une boucle qui scanne tous les éléments un à un. Dans cette situation, il n'est nécessaire de lever une exception qui indique de passer à l'élément suivant lorsque l'élément actuel n'est pas convertible. Pour cela, on élabore la boucle suivante:

```{r echo = TRUE, warning = FALSE}
for i in range(len(x) ):
    try:
        x[i] = float(x[i] )
    except:
        pass
```

l'instruction pass permet de continuer la boucle lorsqu'une chaine de caractére non convertible esr rencontrée.

L'instruction **« pass »** est trés proche des instructions **« break »** et **« continue »**


## B. Utilisation des clause else et finally dans une exception

 Au même titre que pour les clauses **« if »**, il est possible d'adjoindre un bloc **« else »** aux blocks de gestion d'exceptions: ce dernier ne sera alors exécuté que si aucune exception n'a été levée. Par ailleurs, il est aussi possible d'ajouter un block **« finally »** à la definition d'une exception. les instructions de ce dernier bloc seront exécutées qu'il y'ait des exceptions ou pas (par exemple instruction à executer pour fermer un fichier ouvert par des instructions try). L'exemple ci-dessous illustre des clauses else et finally.



```{r echo = TRUE, warning = FALSE}
try:
    num = int(input('Entrer un nombre: '))
except ValueError:
    print('Vous devez entrer un nombre')
else:
    print('Vous avez bien entré un nombre')
finally:
    print('Ce texte sera toujours imprimé')
```

Comme signalé précédemment, le bloc else est exécuté quand l'exception ne se produit pas c'est à dire lorsque le bloc try fonctionne correctement Quant au bloc finally, il sera toujours exécuté, même si un return, break ou continue intervient dans le code avant l'instruction finally. Exemple: except

```{r echo = TRUE, warning = FALSE}
def myFunction():
    try:
        return 1
    except:
        pass
    finally:
        print(2)
```

## C. Les exceptions déclenchées par l'utilisateur: l'instruction raise

L'instruction raise permet au programmeur de decléncher une exception. Par exemple:

**raise NameError('MyError')**

cette instruction renvoie NameError: MyError

Une exception est déclenchée grâce au mot clés **raise**. il suffit alors d'indiquer le nom de l'exception levée, suivie éventuellement d'arguments. la syntaxe générale est la suivante:

**raise MyValueError('Ceci est mon erreur de test')**

Si on souhaite déterminer si une erreur a été levée, mais sans la prendre en charge, il est possible de lever la même erreur dans le bloc except à l'aide de raise. Exemple:


```{r echo = TRUE, warning = FALSE}
try:
    raise MyException('Une exception')
except MyException:
    print('Il y une exception ici')
    raise MyError
```

On peut aussi décider que le programme agira différemment selon l'erreur produite. Dans l'exemple suivant, le programme teste d'abord si l'erreur est de type **ZeroDivisionError** auquel cas il affiche le message division par zéro. Pour un autre type d'erreur; il regarde s'il y a d'autres instructions except qui s'y rapportent. S'il y en a une, il exécute les lignes qui la suivent, sinon, le progamme s'arete et déclenche une erreur.


```{r echo = TRUE, warning = FALSE}
def inverseFunction(x):
    y = 1.0 / x
    return y
    try :
        print ((-2.1) ** 3.1)
        print (inverse (2))
        print (inverse (0))
    except ZeroDivisionError:
        print ("division par zéro")
    except Exception as exc:
        print ("erreur inprévue : ", exc.__class__)
        print ("message", exc)
```

Il est également possible d'associer une variable à l'erreur générale c'est à dire stocker l'erreur dans une variable, afin de la manipuler et d'obtenir des informations plus précises: la variable spécifiée dans la ligne except est alors associée à l'éxception qui a été levée. il est possible d'accéder aux attributs et aux arguments de l'execption concernée. Exemple:

```{r echo = TRUE, warning = FALSE}
try:
    raise Exception('Premier argument', 'Autre argument')
except Exception as error:
    print(type(error))
    print(error.args)
```

## resources

1. [https://docs.python.org/3/tutorial/errors.html](https://docs.python.org/3/tutorial/errors.html "Optional link title").

2. [https://www.codingem.com/try-catch-in-python/](https://www.codingem.com/try-catch-in-python/ "Optional link title").



## références

1. Erich Gamma, Object-Oriented Software Development based on ET++, (in German) (Springer-Verlag, Berlin, 1992).
2. Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides, Design Patterns, Elements of Reusable Object-Oriented Software (Reading, MA: Addison-Wesley, 1995).

![le logo de Framasoft](https://framasoft.org/nav/img/logo.png)



