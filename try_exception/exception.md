
Salut les amis, aujourd'hui nous allons parler des **extensions** en python. Oui des **extensions** car, même si une instruction est syntaxiquement correcte, elle peut générer une erreur lors de son exécution **(exemple la division par 0, accés a un fichier qui n'existe pas, etc).** Les erreurs détectées durant l'exécution sont appelées des exceptions et ne sont pas toujours fatales: nous appredrendrons ici à comment les traiter dans vos programmes. Tout au long de ce tutoriel nous allons:

  1. montrer l'utilisation des blocs try-except, 
  2. l'uttilisation des clauses *else* et *finally* dans une exception
  3. montrer comment un uttilisateur peut déclencher une exception

  

## Utilisation des blocs try-exception

Lors de l'appel d'une fonction, l'interpreteur Python peut rencontrer des qu'il n'est pas en mesure d'executer. Dans ces cas, il jette une exception et renvoie un message d'erreur. Par exemple, soit l'instruction définie comme suit:

 `val = int(input('Veuillez saisir un nombre entier'))`

Dans cette instruction on demande à l'utilisateur de saisir un nombre entier. Et supponsons un seul instant qu'il saisisse des chaînes de caractères contenant des valeurs alphabétiques ou des caractéres spéciaux; eh bien **Python** enverra un message d'erreur de type *«ValueError: could not
convert string to int… »* car la fonction **int()** ne permet de convertir que des chaînes constituer des valeurs en chiffres. Dans cette situation, on est face à une exception. Si cette exception n'est pas gérée par le programme dont l'instruction fait partie, le resultat est l'arrêt du programme avec affichage d'un message d'erreur. 

Mais, le langage python offre les possibilité au programmeur de contrôler les instructions pouvant générer des exceptions et de définir ses propres traitements d'erreur. Ces traitements sont basés sur l'utilisation **« try »** et **« except »**  qui figurent également parmi les *33* mots réservés de python. Les instructions susceptibles de générer des exceptions sont placées à l'interieur d'un bloc **try »** et les instructions à exécuter en cas d'exceptions sont définies à l'intérieur d'un bloc **except »**. 

un bloc **try** doit être accompagné d'au moins un bloc except. Plusieurs blocs except peuvent être associés à un même bloc **tru**. Ainsi, un ensemble **try-except** s'ecrira de la forme:

try:

    instructions

except ErrorType1:

    instructions si ErrorType1

except ErrorType2:

    instructions si ErrorType2

except (ErrorType3, ErrorType4)

    instructions si autre erreur



**_NB:_** il existe 03 manières d'ecrire la ligne except:
 1. En indiquant le nom de l'erreur concernée. exemple: except Error:
 2. En indiquant un tuple contenant plusieurs erreur. Exemple: except (Error1, ..., Errorn):
 3. En n'indiquant rien. Exemple: except:
 

**_Petit exemple_**: Demandons à l'utilisateur de saisir des valeurs et lui redemander une nouvelle fois la saisie afin qu'il entre une nouvelle valeur convenable.


```{r echo = TRUE, warning = FALSE}
try:
    val = float(input('Veuillez saisir un nombre :'))
except ValueError:
    print('La nouvellee entrée n'est pas valide')
    val = float(input('Veuillez recommencez s'il vous plais:'))
```
 
```
try:
    val = float(input('Veuillez saisir un nombre :'))
except ValueError:
    print('La nouvellee entrée n'est pas valide')
    val = float(input('Veuillez recommencez s'il vous plais:'))
```


![le logo de Framasoft](https://framasoft.org/nav/img/logo.png)