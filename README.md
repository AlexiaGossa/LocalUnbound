LocalUnbound
============
Un résolveur local pour les requêtes DNS

Vous ne souhaitez pas utiliser le resolveur de votre Fournisseur d'accès Internet (FAI) ? ni celui d'un autre opérateur comme Quad9, CloudFlare ou Google ? Vous souhaitez maitriser vous-même cette partie d'Internet sans DNS menteur ?

Dans ce petit projet pour Windows mais très facilement transposable pour d'autres systèmes, votre ordinateur va résoudre tout seul l'ensemble des requêtes DNS vous permettant de naviguer sur internet.

## Etape 1 - Télécharger Unbound et l'installer

a) Il faut télécharger le fichier d'installation de Unbound nommé "unbound setup" via le lien ci-dessous
https://www.nlnetlabs.nl/projects/unbound/download/


b) Installer le binaire Unbound



## Etape 2 - Configurer Unbound

a) Télécharger le fichier suivant
https://www.internic.net/domain/named.root

b) Renommer ce fichier en `root.hints`

c) Copier le fichier `root.hint`s dans `C:\Program Files\Unbound\root.hints`

d) Récupérer le fichier `service-box-internet.conf` présent dans ce petit projet

e) Renommer ce fichier en `service.conf`

e) Remplacer `C:\Program Files\Unbound\service.conf` part le fichier précédemment renommé.

f) Ouvrir les services Windows : On appuie `Windows` + `R` (ou Démarrer => Exécuter) et saisir `services.msc`

g) Arrêter le service `Unbound DNS validator`

h) Démarrer le service `Unbound DNS validator`

## Etape 3 - Finir la configuration de l'ordinateur

Il faut maintenant modifier la configuration réseau de la machine.

a) On ouvre le panneau des connexions réseau

On appuie sur `Windows` + `R` pour ouvrir la fenêtre Exécuter (ou bien Démarrer => Exécuter).

On saisie `ncpa.cpl`.

b) On modifie la configuration de notre carte réseau utilisée

On fait `clic-droit` sur la carte réseau Ethernet (Wifi ou réseau filaire) puis `Propriétés`.

On sélectionne, sans décocher, la ligne `Protocole Internet Version 4 (TCP/IPv4)`.

On clique sur le bouton `Propriétés`.

Dans la partie basse de la fenêtre, on sélectionne l'option nommée `Utiliser l'adresse de serveur DNS suivante`

On saisie dans le `Serveur DNS préféré` => 127.0.0.1

On laisse vide la `Serveur DNS auxiliaire`

On clique sur `OK`

c) Il est souvent plus pratique de redémarrer l'ordinateur

## Etape 4 - C'est terminé, on teste ?

a) Pour vérifier le bon fonctionnement de notre DNS ?

On démarre une ligne de commande.

On saisie la commande suivante `nslookup github.com`

Voici un exemple de réponse donnée :
> Serveur :   localhost
> 
> Address:  127.0.0.1
> 
> 
> Réponse ne faisant pas autorité :
> 
> Nom :    github.com
> 
> Address:  140.82.121.3
> 

b) Désormais votre ordinateur s'occupe de la résolution DNS !

Si vous souhaitez augmenter les performances de résolution DNS, vous devez modifier le fichier `service.conf` présent dans `C:\Program Files\Unbound\`

A noter que je mets également à disposition le fichier `service-box-internet-big.conf` proposant de meilleures performances au prix d'une consommation de ressources plus importantes.
