---
layout: post
title: OSCP retour d'experience
tag: stress
author: Sans23
---

**_Examen OSCP_**

**TL;DR**

Actuellement en L3 à la faculté de Dijon et trés déçu de la formation quasi inexistante, j'ai voulu profiter de mon temps libre pour passer l'OSCP. Pour se faire, j'ai bloqué 60 jours après les partiels de début janvier.

**Mon Background**

Je suis un étudiant de 20 ans qui vise le métier de pentester/red team. Je participe à de nombreux CTF et des machines (hackthebox.eu). J'ai commencé l'informatique à 17-18 ans. Enfin, je suis trés "bordelique".

**Organisation**

Mon organisation est que je n'ai pas d'organisation et cela m'a bien porté préjudice. Mon seul but était dans un premier temps de faire tout le lab puis de passer l'exam.

**Le Lab**

Le lab était vraiment sympa. J'ai largement progressé sur les machines Windows qu'auparavant j'évitais comme la peste. Il m'a fallu 45 jours pour finir le lab à 100%. A la vue de mon avancement, j'ai pris mon temps. Je n'ai pas bossé dessus tous les jours pour prendre le plus de plaisir quand je le faisais. Malheureusement, j'ai perdu énormement de temps à cause de la post exploitation, certaines machines ou des dépendances plus ou moins claires.

**Examen**

J'ai profité des vaccances de Février pour finir le lab et avancer mon examen afin d'essayer de le valider avant les entretiens pour les écoles supérieures.J'ai donc passé mon examen le samedi 5 mars a 1h du matin.

**La veille**

J'avais un examen partiel de Systèmes et réseaux le matin et toute l'aprés-midi un TP de cette même matière jusqu'a 17h45. Je suis donc rentré chez moi pour dormir avant le jour J.

**Le jour J**

Le reveil sonne a 00h30. Je me connecte sur la plateforme et fais ma vérification d'identité puis c'est parti ! Je commande un Uber eat et je commence. Les modalités de l'examen ont évoluées. J'ai le donc un AD que je dois absolument pwn pour réussir.

**Active Directory**

Il y a trois machines à pirater. Première machine en 30 minutes puis j'upload tous mes outils dessus. Je vais pour attaquer la deuxieme machine, ettttttttttttttt rien !!
Il faut savoir que nous avons un panel pour redémarrer les machines et que redémarrer une machine de l'AD reset toutes les machines de celui ci. De base, les machines sont toutes démarrées. Malheureusement, je n'ai pas eu de chance car la deuxieme machine était éteinte ou plantée. J'ai donc perdu quasiment 1h à tout essayer en vain puis à devoir re rooter la premiere machine.
Mais vous aussi l'avez oublié... Le uber eat !! et oui, j'avais éteint mon teléphone. J'alt tab sur le navigateur. Le pauvre... il attendait depuis un moment devant chez moi. Il y avait un timer sur mon écran (il restait 2 minutes pour récuperer ma commande). Aprés manger, j'attaque la deuxieme machine et le DC dans la foulée à 3h30. J'étais Domain admin. A ce moment là, je prends la confiance et je me suis mis à faire le rapport en me disant que si tout l'examen se passe aussi bien, j'aurais fini d'ici le lever du soleil. Je démarre libre office avec la template fournie par offset mais mon UI plante complètement. Je ne sais pas pourquoi mais libre office faisait exploser mon pc j'ai donc du trouver un plan B.

J'ai récupèré un projet en cpp où j'avais un doxygen setup puis j'ai viré le code, ajouté un fichier markdown en page principale et généré une doc doxygen pour navigateur pour ensuite faire un CTRL+P sur la page et l'exporter en PDF(c'est le plus simple que j'avais en tête).
Ecrire le rapport m'a pris beaucoup beaucoup plus de temps que prévu. J'ai fini le rapport de l'AD a 6h30.

**Machine 1**

Aprés un scan des trois machines restantes, une me semble facile. J'ai donc focus cette box et fini par la rooter à 9h. A ce moment là, je comprends que j'ai peut-être pris trop la confiance de faire le rapport de l'AD ! Je passe donc directement à la deuxième machine.

**Machine 2**

La machine 2 commence bien ! je reussi à avoir un shell non privilègié en moins de 30 minutes mais j'étais complètement bloqué au bout de quelques heures. Je fini par trouver quelque chose d'intéressant et je root la machine à 11h30.
A ce moment là, je sais que j'ai assez de points pour obtenir l'exam  et je fais donc le rapport. Vers 15h, je relis l'exam guide pour être sûr que je n'ai rien oublié.

Et là... la douche froide ! je n'avais pas vu qu'il fallait fournir des preuves intermédiaires pour les machines. Je me dépêche de re rooter les boxs pour refaire les screenshots. Je me rend compte que je n'ai pas rooté une des machines de la façon attendue !  A ce moment là, mon sourire s'effaça directement de ma gueule qui pensait avoir plié l'examen. J'avais peur que ma façon de faire ne soit pas attendue... J'ai donc passé plusieurs heures afin de réussir à avoir un shell user sur cette machine mais je n'arrivais pas à avoir la privesc.

**Machine 3**

Je n'en ai pas parlé au dessus mais j'ai passé plusieurs heures à attaquer la machine et je n'ai rien trouvé. Je suis toujours très frustré de ne rien avoir trouvé. j'ai tout donné et cela n'a pas suffit. je n'ai aucune piste.

**Rapport**

J'ai fait de mon mieux pour faire un rapport qualitatif. J'ai check et recheck et rerecheck mon orthographe et mes tournures de phrases. je mets tous les screens bien comme il faut. Je recheck tout, je l'exporte en PDF et je l'envoie.
J'ai donc envoyé mon rapport à 23h et j'avais terminé pour aller en soirée avec mes copains de prépas. Premier truc que j'ai fais! C'est de manger un saucison!!

**Le Lendemain**

J'etais très très stressé la veille et je n'avais rien mangé mais j'avais bu 4 cannettes de Red bull et 1 de Monster. Je retourne lire mon rapport pour tout recheck et là c'est le drame! J'avais fourni le code source dans des carrés de code en markdown ainsi que certaines commandes. Sur le site généré par doxygen, il y a des petits ascenseurs quand le code dépasse trop sur la droite. Malheureusement, l'exportation en pdf rogne le code sur la droite. J'avais donc une commande ainsi qu'un code d'un outil fait maison qui étaient shortées sur la droite. J'ai donc été dans le mal toute la journée à me dire que j'allais devoir revivre une journée de stress intense.

**Resultat**

Le dimanche, en allant me coucher, aprés avoir appelé mes parents et mes amis pour leur expliquer la situation et mes potentiel doutes sur le résultat, je suis allé checké mes mails. Ce fut un grand soulagement de voir que j'avais une réponse positive. J'ai donc super bien dormi.
