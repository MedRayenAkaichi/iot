# Système de vote électronique

Voici un diagramme de séquence représentant les interactions dans le système de vote électronique :

```mermaid
sequenceDiagram
    participant Moderator as Modérateur
    participant Voter as Votant

    Modérateur->>Voter: Se connecte au système
    Voter-->>Modérateur: Confirmation de connexion

    Modérateur->>Voter: Crée une session
    Voter-->>Modérateur: Reçoit le Token

    Voter->>Modérateur: Se connecte avec le Token
    Modérateur-->>Voter: Confirmation d'accès à la session

    Modérateur->>Voter: Crée un vote
    Voter-->>Modérateur: Reçoit les options de vote

    Voter->>Modérateur: Participe au vote (envoie son choix)
    Modérateur-->>Voter: Confirmation de vote reçu

    Modérateur->>Voter: Clôture le vote
    Voter-->>Modérateur: Notification de clôture

    Modérateur->>Voter: Clôture la session
    Voter-->>Modérateur: Notification de session clôturée
