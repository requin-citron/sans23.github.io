---
layout: post
title: ReadTeamVillage CTF 2021 Something, Something, Haystack.
tag: misc
---

**_MISC_**

![](../images/rtv-29/something/chall_something.png)

## **Analyse du chall**

En premier lieu on télécharge le zip de 120 Mo
puis on le unzip. On remarque que le répertoire flag contient énormement de fichiers pas étonnant quand on vois la taille du zip.

![](../images/rtv-29/something/first.png)
![](../images/rtv-29/something/snd.png)

En ouvrant les première images on remarque quelles ont toutes l'air identique.  

![](../images/rtv-29/something/0.jpg)

La question est sont elles toutes vraiment identique ?


## **Résolution**

Pour verifier si les images sont bien toutes identique on va faire une somme MD5 sur chaque une.

    for img in $(ls ./flags); do
      echo "$(md5sum ./flags/$img)"
    done > out.txt

![](../images/rtv-29/something/tree.png)

Plus qu'a vérifier si il n'y a pas une images qui est identique aux autres.

    cat out.txt | grep -v 7045b8920411be26d5b2ae3b44cef3ef


![](../images/rtv-29/something/four.png)

Une images differente sort de plus elle possède une chaine de caractère qui resemble a un flag.
On voit tout de suite qu'il s'agit d'un chiffrement cesar. Tentons un ROT13.

![](../images/rtv-29/something/five.png)

Flag !
