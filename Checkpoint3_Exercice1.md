# Partie 1 : Gestion des utilisateurs

# Q.1.1.1 :
* Dans le gestionnaire de serveurs, cliquer sur tools et selectionner Active Directory Users and Computers.
* Aller dans TSSR.LAN, LabUsers et selectionner DirectionDesRessourcesHumaines.
* Faire un clique droit sur l'utilisateur Kelly.Rhameur et selectionner Copy
* Entrer le nom et le prénom : Lionel Lemarchand et le mot de passe : @!90Xo/Yl67#. Cocher la case : User must change password at next logon. Puis cliquer sur next et finish.
* ![365169143-716ad4b7-da8b-489f-8b35-a9988e0c401a](https://github.com/user-attachments/assets/2fff09e2-e4ee-4f2e-916a-56e0c0381c30)

# Q.1.1.2
* Clique droit sur TSSR.LAN, aller dans New et cliquer sur organizational unit.
* ![365084842-34be8742-e571-411d-819d-0b9d74a461ca](https://github.com/user-attachments/assets/7f875c95-1eac-4ac5-ba0c-915c8dfdd65c)
* Nommer l'unité d'organisation DeactivatedUsers, faire un clique droit sur le compte de kelly.rhameur, aller dans all tasks et cliquer sur move. Cliquer sur l'ou DeactivatedUsers et sur ok.
* ![365088466-ea162d45-66cf-4bdf-9d8e-6d6fdcec167b](https://github.com/user-attachments/assets/e299eb5e-ea96-41a9-af28-1152a8c3f729)
* Faire un clique droit sur le compte de kelly.rhameur et cliquer sur disable account.

# Q.1.1.3
* Aller dans le dossier DirectionDesRessourcesHumaines, clique droit sur le groupe GrpUsersDirectionDesRessourcesHumaines, aller dans propriété, cliquer sur add et ajouter le compte lionel.lemarchand, cliquer sur remove et sur le compte kelly.rhameur pour le supprimer.
* ![365090712-4b501dbd-03dc-41da-8288-f20264774324](https://github.com/user-attachments/assets/249b845d-e70c-4841-b680-89309317b8a1)

# Q.1.1.4
* Clique droit sur le compte kelly.rhameur et cliquer sur rename. Ajouter -ARCHIVE a la fin du nom.
* ![365095009-b1bbda9b-7f78-44d0-9728-c84b1c96dbc2](https://github.com/user-attachments/assets/b46539a9-4a09-4991-ba5b-9ae7dc9d13f0)

# Partie 2 : Restriction utilisateurs

# Q.1.2.1 
* Clique droit sur l'utilisateur gabriel.gulh, cliquer sur propriété, aller dans l'onglet account, cliquer sur logon hours et autoriser la connexion du lundi au vendredi de 7h a 17h.
* ![365104634-114ab4a0-8da4-43e5-a697-fc7a2900676f](https://github.com/user-attachments/assets/203b9d5a-36fc-47f1-897d-614a8785d00d)

# Q.1.2.2
* Clique droit sur l'utilisateur gabriel.gulh, cliquer sur propriété, aller dans l'onglet account, cliquer sur log on to, selectionner the following computers et mettre CLIENT2.
* ![365106201-10181d71-d0cd-4fcc-84e6-593ad429d241](https://github.com/user-attachments/assets/c31551d2-204b-41e5-861a-5ca22f2b5d12)

# Q.1.2.3
* Créer une GPO nommée strategie de mots de passe et la lier a LabUsers. Clique droit sur LabUsers et cliquer sur edit.
* ![365123686-e5feed14-d390-4f9c-b79f-31e07193a097](https://github.com/user-attachments/assets/c8136dca-2901-4c54-af2b-93a4b40dcdbd)
* La fenetre group policy management editor s'ouvre.
* Aller dans computer configuration, windows settings, security settings, account policies, password policy.
* Dans maximum password age, mettre 15 jours
* Dans minimum password age, mettre 1 jour
* Dans minimum password length, mettre 12 caracteres
* Dans minimum password length audit, mettre 12 caracteres
* Dans password must meet complexity requirements, selectionner enabled
* Dans relax minimum password length limits, selectionner disabled
* Dans store passwords using reversible encryption, selectionner enabled
* ![365128348-a577b738-47cb-432f-93b5-cb11fc03767f](https://github.com/user-attachments/assets/8f4006cf-e41b-40f5-938c-b0f8a87fc061)

# Lecteurs reseaux

# Q.1.3.1
* Faire un clique droit sur TSSR.LAN et cliquer sur create a gpo in this domain and link it here. La nommer drive-mount.
* Faire un clique droit sur la gpo drive-mount et cliquer sur edit.
* La fenetre group policy management editor s'ouvre.
* Aller dans user configuration, preferences, windows settings, drive maps.
* ![365160853-a0e62d88-3570-45e0-8e08-6fd01c8603e2](https://github.com/user-attachments/assets/b105189b-8340-463c-b4eb-495752e652dd)
* Faire un clique droit sur drive maps et cliquer sur new.
* Une fenetre new drive properties s'ouvre.
* Dans action, selectionner update
* Dans drive letter, selectionner existing et le lecteur E
* Cliquer sur appliquer et sur ok
* Faire la meme chose pour le lecteur F
* ![365165937-29b262b9-a0bc-4cd8-987c-cbee4cc8ed49](https://github.com/user-attachments/assets/4f52c58d-cdc9-44b3-a189-85826638e740)







