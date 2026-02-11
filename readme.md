# Portfolio - Architecture Haute Disponibilité (HA)

Ce dépôt contient le code source de mon portfolio, auto-hébergé sur mon infrastructure personnelle (Home Lab) avec un système de basculement automatique vers le cloud pour garantir une disponibilité à 100%.

## Architecture Technique

Le site repose sur une architecture moderne alliant serveur physique et services Edge :

- **Hébergement Primaire** : Serveur physique Acer Aspire X1430 (4 Go RAM) sous Ubuntu Server.
- **Conteneurisation** : Stack multi-conteneurs gérée de manière déclarative via Docker Compose et Portainer.
- **Reverse Proxy** : Nginx Proxy Manager (NPM) gère le routage interne et les certificats SSL.
- **Exposition Sécurisée** : Cloudflare Tunnel (Zero Trust) permet l'accès externe sans ouverture de ports sur la box internet.

## Monitoring & Observabilité

L'infrastructure est surveillée en permanence pour prévenir les pannes et analyser les performances :

- **Disponibilité** : Uptime Kuma surveille les endpoints HTTP et l'état des services.
- **Métriques & Visualisation** : Netdata pour le monitoring temps réel, couplé à Grafana et Prometheus pour l'analyse historique.
- **Logs & Ressources** : Dozzle pour la consultation des logs en direct et cAdvisor pour les statistiques des conteneurs.
- **Alerting** : Système de notifications automatiques pour anticiper les pannes critiques (Surcharge CPU, RAM, Espace disque).

## Stratégie de Sauvegarde & Résilience (3-2-1)

Une politique de sauvegarde rigoureuse assure la résilience des données et des configurations :

- **Règle 3-2-1** : Maintenance de 3 copies des données (Local, Backup Restic, Cloud) sur 2 supports différents (Disque Acer, Google Drive), dont 1 sauvegarde hors site.
- **Technologie & Transport** : Utilisation de Restic avec chiffrement AES-256 (côté client) et tunnelisation via Rclone vers le stockage distant.
- **Automatisation** : Script Bash (`backup.sh`) orchestré par Cron exécuté quotidiennement à 3h du matin.
- **Optimisation** : Déduplication native pour minimiser l'espace disque et la bande passante.

### Test de Restauration (PRA)

La résilience du système a été validée par un test de restauration granulaire :

- **Simulation** : Suppression volontaire d'un fichier critique (`projects.html`).
- **Restauration** : Récupération via l'ID de snapshot Restic vers le chemin d'origine.
- **Validation** : Vérification de l'intégrité et remise en ligne immédiate du service.

## Laboratoire de Cybersécurité (Bachelor 2)

L'infrastructure sert de bac à sable pour l'apprentissage de la sécurité et des réseaux :

- **Sécurité Défensive** : Mise en place de sauvegardes immuables et chiffrées pour contrer les risques de ransomware.
- **Administration Système** : Gestion fine des permissions Unix, automatisation par scripts et gestion sécurisée des secrets (fichiers `.restic_pw` protégés).
- **Virtualisation & IA** : Déploiement de nodes sous Ubuntu Server pour l'expérimentation de modèles d'IA et de services réseau.

## CI/CD & GitOps

Le déploiement est entièrement automatisé pour garantir la fluidité des mises à jour :

- **GitHub Actions** : Pipeline CI déclenché à chaque `git push` sur la branche `master`.
- **Webhooks Portainer** : Déclenchement automatique du redéploiement sur le serveur local via Webhook.
- **GitOps** : Synchronisation continue garantissant que la production reflète toujours l'état du dépôt GitHub.

## Résilience & Failover (Haute Disponibilité)

Un système de basculement automatique pallie toute indisponibilité du serveur local :

- **Cloudflare Worker** : Script Edge agissant comme load balancer intelligent.
- **Détection de Panne** : Health-checks continus vers le serveur d'origine (`server.edouard-vallet.fr`).
- **Bascule Automatique** : Redirection transparente vers GitHub Pages en cas d'erreur (Timeout/5xx) en moins de 3 secondes.
- **Traçabilité** : Injection du header `X-Served-By` pour identifier la source de réponse (Origin ou Backup).

## Optimisations Spécifiques

- **Gestion des Médias** : Intégration vidéo optimisée via balise `<video>` (`autoplay loop muted`) pour le support universel du format WebM.
- **Accès Distant** : Administration sécurisée possible via SSH/SFTP depuis des terminaux mobiles.