sequenceDiagram
    participant Modérateur
    participant Système
    participant Votant

    %% 1. Connexion du modérateur au système
    Modérateur->>Système: Connexion (MQTT CONNECT)
    Système-->>Modérateur: Connexion acceptée (CONNACK)

    %% 2. Création de la session et partage du Token
    Modérateur->>Système: Création de session (CREATE_SESSION + Token)
    Système-->>Modérateur: Session créée (SESSION_ACK)
    Modérateur->>Votant: Partage du Token (Token distribué hors MQTT)

    %% 3. Connexion du votant au système
    Votant->>Système: Connexion (MQTT CONNECT)
    Système-->>Votant: Connexion acceptée (CONNACK)

    %% 4. Votant rejoint la session
    Votant->>Système: Rejoindre session (JOIN_SESSION + Token)
    Système-->>Modérateur: Notification de nouveau votant (NEW_PARTICIPANT)
    Système-->>Votant: Confirmation d'accès à la session (SESSION_JOINED)

    %% 5. Création d'un vote par le modérateur
    Modérateur->>Système: Création du vote (CREATE_VOTE + Sujet + Options)
    Système-->>Votant: Notification du vote actif (NEW_VOTE + Sujet + Options)

    %% 6. Participation au vote par le votant
    Votant->>Système: Participation au vote (VOTE + Option choisie)
    Système-->>Modérateur: Mise à jour des résultats (VOTE_UPDATE)

    %% 7. Clôture du vote par le modérateur
    Modérateur->>Système: Clôture du vote (CLOSE_VOTE)
    Système-->>Votant: Notification de clôture (VOTE_CLOSED)
    Système-->>Modérateur: Résultats finaux (FINAL_RESULTS)

    %% 8. Clôture de la session par le modérateur
    Modérateur->>Système: Clôture de session (CLOSE_SESSION)
    Système-->>Votant: Notification de fin de session (SESSION_CLOSED)
    Système-->>Modérateur: Confirmation de clôture (SESSION_TERMINATED)
