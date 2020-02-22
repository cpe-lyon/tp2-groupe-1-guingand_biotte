
# TP2-Bash

## Exercie 1 : Variables d’environnement
1. History se trouve dans : /cpe/.bash_history
2. La variable d'environnement $HOME permet de revenir au dossier perso
3. $LANG stocke la langue
     $PWD stocke le chemin de /var/
     $OLDPWD équivalent de $HOME
     $SHELL stocke le chemin /bon/bash
     $_ stocke le dernier argument mit dans une commande
4. MY_VAR="abcdef"
	echo $MY_VAR
5. bash exécuté sans argument démarre une nouvelle session, $MY_VAR n'existe plus car nous ne somme pas dans la même session. Quand nous faisons exit on reviens à la session précédente.
6. export MY_VAR="abc", $MY_VAR devient une variable d'environnement, et lors d'une nouvelle session $MY_VAR est bien accessible.
7. export NOMS="BIOTTE GUINGAND", echo $NOMS la variable existe bien.
8. echo "Bonjour à vous deux," $NOMS
9. La commande unset va supprimer la variable et donc vider la case mémoire alors que mettre une valeur null conserve la variable dans la mémoire
10. echo "\$HOME = "$HOME


### Programmation BASH
echo "$PATH = $PATH:~/script" >> .bashrc

## Exercie 2 : Contrôle de mot de passe
```bash
                                    
#! /bin/bash
PASSWORD='test'
read -s -p 'Saisissez le mot de passe: ' pswd
if [ "$pswd" = "$PASSWORD" ]; then
        echo "OK"       
else
        echo "false"
fi
```
## Exercie 3 : Expressions rationnelles
```bash
#! /bin/bash

function is_number
{
        re='^[+-]?[0-9]+([.][0-9]+)?$'
        if ! [[ $1 =~ $re ]] ; then
                return 1
        else
                return 0
        fi
}
is_number $1
if [ $? = 0 ] ; then
        echo 'nombre entier'
else
        echo 'erreur'
fi
```
##  Exercice 4 : Contrôle d’utilisateur
```bash
#!/bin/bash
if [ -z "$1" ] ; then
        echo "Utilisation : $0 nom_utilisateur"
else
ret=$(grep $1 /etc/passwd | cut -d: -f1)
        if [ $ret = $1 ] ; then
                echo "L'utilisateur existe"
        else
                echo "L'utilisateur n'existe pas"
        fi
fi
```
## Exercice 5 : Factorielle
```bash
#!/bin/bash

let "var=$1"
let "bcl=1"
let "bclmax=var-1"
for bcl in $(seq 1 $bclmax); do
        let "var *= bcl"
done
echo $var
```
## Exercice 6 : Le juste prix

````bash
Perdu=1
MAXIMUM=1000
MINIMUM=1
rep=0
essai=1
Rand=$((MINIMUM+RANDOM*(1+MAXIMUM-MINIMUM)/32767))

while [ $Perdu == 1 ]
do
	echo Entrez votre prix
	read rep
	if [ $rep  -gt  $Rand ]
		then
			echo  "Prix trop élevé"
		elif [ $rep  -lt  $Rand ]
		then
			echo  "Prix trop petit"
		else
			echo  "Bravo Juste prix ! "
			Perdu=0
			echo  $essai  " essais"
	fi
let "essai++"
done
````