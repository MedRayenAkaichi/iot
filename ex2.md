sequenceDiagram
    actor Moderator as Modérateur
    actor Voter as Votant
    participant MQTT as Système MQTT

    %% Connexion du modérateur
    Moderator->>MQTT: Connexion au système
    MQTT-->>Moderator: Confirmation de connexion

    %% Création d'une session
    Moderator->>MQTT: Créer une session (génération du Token)
    MQTT-->>Moderator: Token généré et partagé

    %% Connexion d'un votant
    Voter->>MQTT: Connexion au système
    MQTT-->>Voter: Confirmation de connexion

    %% Participation du votant à la session
    Voter->>MQTT: Rejoindre la session (avec le Token)
    MQTT-->>Voter: Confirmation de participation
    MQTT-->>Moderator: Mise à jour du tableau de bord (votant connecté)

    %% Création d'un vote
    Moderator->>MQTT: Création d'un vote (sujet et options)
    MQTT-->>Moderator: Confirmation de création du vote
    MQTT-->>Voter: Notification d'un nouveau vote

    %% Participation au vote
    Voter->>MQTT: Envoi de son choix
    MQTT-->>Moderator: Mise à jour des résultats en temps réel

    %% Déconnexion détectée
    MQTT-->>Moderator: Alerte - Votant déconnecté (si inactivité > 3s)

    %% Clôture du vote
    Moderator->>MQTT: Clôture du vote
    MQTT-->>Moderator: Confirmation de clôture du vote

    %% Clôture de la session
    Moderator->>MQTT: Clôture de la session
    MQTT-->>Moderator: Confirmation de clôture de la session
    MQTT-->>Voter: Notification de clôture de session
