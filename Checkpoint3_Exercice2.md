# Partie 1 : Gestion des utilisateurs

# Q.2.1.1

* Passer en root avec la commande su -.
* Créer un compte personnel nommé julie avec la commande : adduser julie
* Choisir un mot de passe
* ![365214369-7845d708-39c4-48fd-9b57-2f2e42686ec1](https://github.com/user-attachments/assets/c5b15ea5-4eeb-4f9d-bce6-66f4519ba4e6)

# Q.2.1.2

* Préconisations pour ce compte :
* Mises à jour régulières, installer les composants strictement nécessaires, appliquer le principe de moindre privilège, utiliser un mot de passe fort, appliquer le principe de défense en profondeur et journaliser les activités du systeme et des services en cours d'execution.

# Partie 2 : Configuration de SSH

# Q.2.2.1

* Configurer le fichier /etc/ssh/sshd_config.d/local.conf
* A la ligne PermitRootLogin, mettre no et ajouter la ligne DenyUsers root
* 
