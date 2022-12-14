# TP 2 - Bash

## Exercice 1 - Variable d’environnement :

1. bash trouve les commandes tapées par l’utilisateur comme l’indique la commande `echo $PATH`Dans les dossiers 
    
    `/home/tp/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/usr/lib/jvm/java-17-oracle/bin:/usr/lib/jvm/java-17-oracle/db/bin` 
    
    bash trouve les commandes tapées par l’utilisateur comme l’indique la commande `echo $PATH`
    
2. La variable `PWD=/home/tp` permet de nous ramener dans le répertoire personnel lorsqu'elle est utilisée sans argument.
3. `LANG` : défini la langue du système d'exploitation
    
    `PWD` : défini le chemin du répertoire personnel
    
    `OLDPWD` : défini l'ancien chemin du répertoire personnel
    
    `SHELL` : défini le système d'exploitation sur lequel on se trouve
    
4. Création variable locale avec la commande `MY_VAR='Bonjour’`
    
    On vérifie que la variable existe avec la commande `echo $MY_VAR`
    
    ![Capture d’écran de 2022-10-25 09-57-56.png](assets/Capture_dcran_de_2022-10-25_09-57-56.png)
    
5. La commande `bash` supprime les variables locales, donc `MY_VAR` n’existe plus.
6. On crée la variable d’environnement `MY_VAR` avec la commande `export MY_VAR=toto`
    
    Cette fois la commande `bash` ne supprime pas `MY_VAR` car c’est une variable environnement, il faut utiliser la commande `unset` pour la supprimer.
    
7. On crée la variable NOM qui contient nom et prénom, `export NOM='Matias Chatelet-Ferrety’`. On peut afficher sa valeur avec un `echo $NOM` 
8. La commande `echo "Bonjour à vous, $NOM!”` permet d’afficher :
    
    ![Capture d’écran de 2022-10-25 10-35-23.png](assets/Capture_dcran_de_2022-10-25_10-35-23.png)
    
9. Mettre une variable à vide ne va pas supprimer la variable contrairement à la commande `unset` qui supprime définitivement une variable d’environnement
10. La commande `echo '$HOME = '"$HOME”` permet d’afficher la phrase :
    
    ![Capture d’écran de 2022-10-25 10-48-25.png](assets/Capture_dcran_de_2022-10-25_10-48-25.png)
    

## Exercice 2 - Contrôle de mot de passe :

```bash
#!/bin/bash

PASSWORD="CPE"

echo  "Saisissez votre mot de passe:"

read -s pass

if [ $pass = $PASSWORD ]
then
	echo "Mot de passe correct"
else
	echo "Mot de passe incorrect"
fi
```

## Exercice 3 - Expressions rationnelles :

```bash
#!/bin/bash

function is_number()
{
re='^[+-]?[0-9]+([.][0-9]+)?$'
if ! [[ $1 =~ $re ]] ; then
return 1
else
return 0
fi
}

is_number $1

if [ $? = 0 ];
then
  echo "$1 est un nombre"
else
  echo "$1 n'est pas un nombre"
fi
```

## Exercice 4 - Contrôle d’utilisateur :

```bash
#!/bin/bash

function controle_user()
{
  if [ -z $1 ];then
    echo "Utilisation : $0 nom_utilisateur"
  elif [ $USER = $1 ];then
    echo "Utilisateur existant"
  else
    echo "Utilisateur non-existant"
  fi
}
```

## Exercice 5 - Factorielle :

```bash
#!/bin/bash

function factorielle()
{
  compteur=$1
  factorielle=1
  while [ $compteur -gt 0 ]
  do 
    factorielle=$(($factorielle*$compteur))
    compteur=$(($compteur - 1))
  done
  echo "La factorielle de $1 est $factorielle"
}

factorielle $1
```

## Exercice 6 - Juste prix :

```bash
#!/bin/bash

nombre=$(($RANDOM% 1000))
i=0
read usernumber
while [ $nombre != $usernumber ]
do
  let i++
  if [ $nombre -lt $usernumber ];then
    echo "C'est moins"
  else
    echo "C'est plus"
  fi
  read usernumber
done
echo "C'est gagné en $i coups"
```

## Exercice 7 - Statistique :

1.

```bash
#!/bin/bash
 
error=0
max=0
min=0
moyenne=0

function is_number()
{
re='^[+-]?[0-9]+([.][0-9]+)?$'
if ! [[ $1 =~ $re ]] ; then
        return 1
else
        return 0
fi
}

function max(){
        if [ $1 -gt $2 ]; then
                max=$1
        elif [ $3 -gt $1 ]; then
                max=$3
        else
                max=$2
        fi
}

function min(){
        if [ $1 -lt $2 ]; then
                min=$1
        elif [ $3 -gt $1 ]; then
                min=$3
        else
                min=$2
        fi
}

function moyenne(){
        moyenne=$((( $1 + $2 + $3 ) / 3 ))
}

min $1 $2 $3
max $1 $2 $3
moyenne $1 $2 $3

while (("$#"));
do
        is_number $1
        if [ $? = 1 ] || [ $1 -gt 100 ] || [ $1 -lt -100 ]; then
                echo "Veuillez saisir des nombres compris entre 100 et -100"
                exit
        fi
        shift
done

echo "Le minimum est $min"
echo "Le maximum est $max"
echo "La moyenne est $moyenne"
```

2.

```bash

```

3.

```bash

```
