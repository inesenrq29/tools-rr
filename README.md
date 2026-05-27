# Installation des tools Ressources Relationnelles

Ce document explique comment installer, configurer et lancer les outils nécessaires au fonctionnement local de l’application Ressources Relationnelles.

Le dossier `tools-rr` contient l’environnement technique utilisé par le projet, notamment les services Docker nécessaires au lancement local de l’application.

## Prérequis

Avant de lancer les tools, il est nécessaire d’avoir installé :

- Docker Desktop
- Docker Compose
- Git

Il faut également s’assurer que Docker Desktop est bien lancé avant d’exécuter les commandes.

## Rôle du dossier tools

Le dossier `tools` permet de lancer les services techniques nécessaires à l’application Ressources Relationnelles en local.

Il permet principalement de démarrer la base de données utilisée par le back-end.

## Lancer les tools

Se placer dans le dossier `tools` :

```bash
cd tools
```

Lancer les conteneurs Docker :

```bash
docker compose up -d
```

## Vérifier que les conteneurs sont lancés

Pour afficher les conteneurs actifs :

```bash
docker ps
```

Ou depuis le dossier `tools` :

```bash
docker compose ps
```

Le conteneur de base de données doit apparaître avec le statut `running`.

## Utilisation avec le back-end

Avant de lancer le back-end Ressources Relationnelles, les tools doivent être démarrés.

Ordre recommandé :

1. Lancer Docker Desktop
2. Se placer dans le dossier `tools`
3. Lancer les conteneurs :

```bash
docker compose up -d
```

4. Lancer le back-end Ressources Relationnelles avec le profil local
5. Lancer le front-end ou l’application mobile si nécessaire




## Mettre à jour les sous-modules back et front

Si le back ou le front ont été mis à jour, il faut mettre à jour les sous-modules Git du projet.

Depuis la racine du projet, lancer d’abord :

```bash
git submodule update --init --recursive
```

Puis :

```bash
git submodule update --remote --merge
```

La première commande initialise et récupère les sous-modules si nécessaire.

La deuxième commande récupère les dernières modifications disponibles sur les branches suivies par les sous-modules.

Si le projet tools a été mis à jour avec une nouvelle version du back-end ou du front-end, récupérer les dernières modifications avec :

```bash
git pull
```
Puis mettre à jour les sous-modules 

## Arrêter les tools

Pour arrêter les conteneurs sans supprimer les données :

```bash
docker compose stop
```

Cette commande arrête les services, mais conserve les conteneurs et les données.

## Relancer les tools

Pour relancer les conteneurs arrêtés :

```bash
docker compose start
```

## Arrêter et supprimer les conteneurs

Pour arrêter et supprimer les conteneurs :

```bash
docker compose down
```

Cette commande supprime les conteneurs, mais ne supprime pas forcément les volumes Docker selon la configuration utilisée.

## Réinitialiser complètement la base de données

Si une réinitialisation complète est nécessaire, il est possible de supprimer les conteneurs et les volumes associés :

```bash
docker compose down -v
```

Attention : cette commande supprime les données stockées dans les volumes Docker. La base sera donc recréée au prochain lancement.

Ensuite, relancer les tools :

```bash
docker compose up -d
```

## Consulter les logs

Pour consulter les logs des services :

```bash
docker compose logs
```

Pour suivre les logs en temps réel :

```bash
docker compose logs -f
```

## Problèmes fréquents

### Docker n’est pas lancé

Si la commande suivante échoue :

```bash
docker compose up -d
```

Il faut vérifier que Docker Desktop est bien ouvert et démarré.

### Le port 3306 est déjà utilisé

Si une erreur indique que le port `3306` est déjà utilisé, cela signifie probablement qu’une autre base MariaDB tourne déjà sur la machine.

Il faut alors :

- arrêter l’autre service MariaDB ;
- ou modifier le port exposé dans le fichier `docker-compose.yml`.


