---
layout: post
title: Comment modifier Initramfs afin de récupérer les identifiants LUKS
tag: luks
author: Sans23
---

**_Modifier la partition de boot pour récupérer la passphrase luks_**

# **TL;DR**

Actuellement dans un train arrêté sur la voie depuis plus 1h et sans réseau j'ai voulu trouver un moyen de récupérer la passphrase d'une partition luks.

# **Concept**

Notre but est de récupérer la passphrase luks d’une partition. Le bruteforce de partition luks est trés lent cela rend les attaques par dictionnaire inefficace. Il nous reste le social engineering, où il est possible d’utiliser un keylogger hardware afin derécupérer la passphrase via un réseau wifi ou bluetooth. Il est aussi possible de le faire de manière software, il s'agit de la méthode que nous mettrons en pratique.


# **Theorie**

Grandement inspiré de cette [article](https://yassine.tioual.com/posts/backdoor-initramfs-and-make-your-rootkit-persistent/)

![](../images/initramfs_luks/boot_process.png)

le démarrage de linux ce résume en 5 étape:

1. Le programme de la carte-mère qui va initialiser le hardware
2. Le bootloader qui va venir chercher sur le disque le kernel et l'exécuter
3. Le kernel va initialiser toutes ses fonctions
4. L'archive initramfs va être décompressée en ram et un script va venir monter tous le fs.
5. Systemd reprend la main et viens démarrer ses services.

Le kernel ainsi que la l'archive initramfs est disponible dans /boot

Dans la suite de l'article nous allons utiliser debian.

## **Comprendre initramfs**

initramfs est une archive compressée contenue dans /boot qui possède un système de fichiers qui sera chargé en ram. Un script situé dans /init est exécuté et viendra monter les partitions dans un nouveau répertoire root et finira par exécuter un chroot dedans puis à exécuter systemd.

Il est possible d’analyser le contenu de cette archive en l’extrayant. L’algorithme de compression peut varier en fonction des distributions, il faut donc utiliser la commande file pour pouvoir le déterminer. Il en résultera une archive cpio.

```
mkdir -p work && cd work
cp /boot/initrd.img-5.10.0-10-amd64 ./initrd.img-5.10.0-10-amd64.gz
gunzip ./initrd.img-5.10.0-10-amd64.gz
cpio -idv < ./initrd.img-5.10.0-10-amd64
```



## **mise en pratique**

En navigant dans le système de fichiers on trouve très vite le script en charge de la partion luks.

> ./scripts/local-top/cryptroot

![](../images/initramfs_luks/default.png)

run_keyscript va appeler le binaire askpass qui va récupérer le mot passe, puis il va être copier sur la sortie standard, enfin, la passpharse est envoyé à unlock_mapping.

![](../images/initramfs_luks/modified.png)

La modification ci-dessus permet de stocker la passphrase sur le système de fichiers dans /.init, cela nous sera utile prochainement.

Par défaut les partions sont montés en read-only. Donc il faut modifier le script init pour désactiver le RO et il faut aussi rajouter une crontab permettant d’envoyer le password sur le réseau.

Pour cela rendez-vous dans
> ./init

![](../images/initramfs_luks/readonly.png)
![](../images/initramfs_luks/ro.png)

Il faut donc modifier la variables readonly en lui assignant **n** pour pouvoir modifier par la suite le système de fichiers.

Nous allons rajouter une commande juste avant le chroot sur le nouveau système de fichiers pour ajouter une ligne dans la crontab et ainsi récupérer la passphrase une fois la machine bootée.

![](../images/initramfs_luks/init_modified.png)

Une fois les modifications terminées nous avons besoin de recompresser notre archive et s'en servir pour remplacer l'archive légitime.

```
find . | cpio -oH newc | gzip > /boot/initrd.img-5.10.0-10-amd64
```

Il ne reste plus qu'à attendre que quelqu'un boot l'ordinateur et tape la passphrase.

![](../images/initramfs_luks/finish.png)

```
echo -n 43686576616c6f506b54506172746965 | xxd -r -p
```
