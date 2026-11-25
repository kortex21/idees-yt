# idee-yt — Chaîne YouTube de tutos informatiques

> Statut : exploration (mode détente). Rien de décidé, Nextcloud et l'infra restent prioritaires.
> Dernière mise à jour : 2026-11-25

## Fonctionnement

- Ce README est la **source de vérité** du projet ; signalé en début de chat
- Claude le met à jour, commit et pousse à chaque avancée
- Rôle de Claude : co-auteur des scripts + « débutant » qui pose les questions bêtes (Q/R, zones d'impro)

## Concept

- Tutos Linux / Gentoo / autohébergement, par un passionné qui n'en a pas fait son métier
- Format **questions-réponses** : un « débutant » (joué par Claude) pose des questions bêtes, je réponds
  - règle en partie la gêne face caméra : on répond à quelqu'un au lieu de faire un monologue
  - script établi à l'avance, avec des **zones d'impro** pour Claude (relances, questions pièges, fausses idées de débutant à démonter)
  - options techniques : vocal en direct (vivant, mais moins maîtrisé) ou synthèse vocale + montage (plus sûr)
  - **transparence** : annoncer que le débutant est une IA ; vérifier les règles YouTube sur les contenus générés par IA
- Pas d'obligation de montrer sa tête : screencast + voix possible
- Accroche possible : « Un Gentooiste répond aux questions bêtes d'une IA »

## Ton

- Sarcasme, ironie, dérision, et surtout **autodérision**
- Matière à bêtisier :
  - « On lance la compilation de Firefox… on se retrouve au prochain épisode »
  - IA : « Pourquoi pas Ubuntu ? » → regard caméra, 3 s de silence
  - Le kill-switch monté avec une autre IA sans le comprendre
    - moi : « Je te kill-switch de suite ou j'attends ? »
    - IA : « Vas-y, de toute façon tu ne sais pas comment il marche. »

## Épisodes envisagés

### Épisode 0 / 1 — « La Genèse d'un Gentooiste »

Mes déboires sur Gentoo, et surtout pourquoi je me suis accroché.

Phrase d'intro : **« Je veux être le maçon de mon OS. »**

Frise (découpage en « jours », comme la Genèse, pas au sens littéral) :
- **Jour 0** : 30 ans sous Windows — quitté parce que trop « embarqué », je ne voulais pas d'un OS tout fait
- **Jour 1** : Ubuntu
- **Jour 2** : distro-hopping
- **Jour 3** (~1 mois sous Linux) : découverte de Gentoo, ça me botte, je bloque, je réessaie, je rebloque
- **Jour 4** (~2 semaines plus tard) : révélation Arch — accès « jusqu'à la culasse » ; 5 ans sous Arch, serveurs de prod en rolling release, tout le monde me conspue ; en parallèle, nouvelles tentatives Gentoo
- **Jour 5** (2016) : 2 semaines sous Funtoo, puis Gentoo avec kernel perso → ça boote enfin
- Ensuite : casser, réinstaller, recasser… jusqu'à comprendre tous les mécanismes (sur de vieux PC, petits procs, 4 Go de RAM) → d'où l'appétence pour btrfs (snapshots)

Philosophie à placer : **« On produit sur les distros qu'on maîtrise. »**
- Contre-argument attendu : ça ne marche que tant qu'on est seul à maintenir
- Réponse : la documentation (Git, single source of truth) pour que d'autres puissent reprendre

À éclaircir :
- [ ] « 30 ans sous Windows » : mon âge au moment du switch, ou 30 ans d'utilisation ?
- [ ] Qu'est-ce que Gentoo m'a apporté qu'Arch ne pouvait pas me donner ?

### Installation Gentoo en questions-réponses

Base issue de la répétition du 2026-11-25. Points à intégrer au script :
- Live : on ne peut pas installer un OS sur le disque utilisé par l'OS lancé ; le live tourne depuis la clé / en RAM
- Montage : tout est fichier sous Linux ; monter = brancher le contenu d'une partition dans l'arborescence (analogie : installer une porte vers une pièce fermée) ; `/mnt/gentoo` = future racine `/` du chroot
- Ordre correct : partitions / subvolumes btrfs → montage → **téléchargement et extraction du stage3** → `make.conf` → montage de `/proc`, `/sys`, `/dev`, `/run` → chroot
- Stage3 : système de base minimal déjà compilé, avec les outils pour compiler le reste (stage1/2 : plus proposés officiellement ; LFS pour ceux qui veulent creuser)
- `make.conf` : réglages globaux de Portage — punchline : « make.conf trop permissif, autant installer une Ubuntu »
  - nommer les **USE flags** + exemple concret (`USE="-X"` sur un serveur)
  - distinguer `make.conf` (global) et `/etc/portage/package.*` (par paquet)
  - nuance : on maîtrise les dépendances *optionnelles*
  - ebuild = la recette (script) de compilation, pas le paquet
- Question en suspens : « Pas de Bluetooth, sauf pour un seul logiciel : je fais comment ? »

### Kill-switch nftables (« je découvre avec vous »)

- Je ne le maîtrise pas encore → l'apprendre d'abord (mode prof), puis le réexpliquer
- Prérequis de toute façon pour la migration de belafreux

## Pistes de monétisation liées

- **VPS / labs pour les viewers** sur un dédié OVH, pour appliquer les tutos
  - vient après l'audience (des années)
  - vérifier : IP additionnelles sur l'offre choisie, droit de revente
  - risques : abus des débutants (piratage, spam, minage), blacklist d'IP, obligations légales d'hébergeur ; jamais sur phoenix
  - alternatives : **labs jetables** réinitialisés après chaque tuto ; **affiliation** Hetzner / OVH
- Blog tiré de docs-infra comme point de départ ou vitrine

## Todo

- [ ] Écrire ensemble le script de l'épisode « La Genèse »
- [ ] Écrire le script « Installation Gentoo en Q/R »
- [ ] Apprendre le kill-switch nftables
- [ ] Vérifier les règles YouTube sur les contenus IA
