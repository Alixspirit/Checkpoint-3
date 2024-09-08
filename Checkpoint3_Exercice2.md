# Partie 1 : Gestion des utilisateurs

# Q.2.1.1

* Passer en root avec la commande su -.
* Créer un compte personnel nommé julie avec la commande : adduser julie et choisir un mot de passe.
* ![365214369-7845d708-39c4-48fd-9b57-2f2e42686ec1](https://github.com/user-attachments/assets/c5b15ea5-4eeb-4f9d-bce6-66f4519ba4e6)

# Q.2.1.2

* Préconisations pour ce compte :
* Mises à jour régulières, installer les composants strictement nécessaires, appliquer le principe de moindre privilège, utiliser un mot de passe fort, appliquer le principe de défense en profondeur et journaliser les activités du systeme et des services en cours d'execution.

# Partie 2 : Configuration de SSH

# Q.2.2.1

* Passer en root : su - et configurer le fichier local.conf avec la commande : nano /etc/ssh/sshd_config.d/local.conf
* A la ligne PermitRootLogin, mettre no et ajouter la ligne DenyUsers root
* ![365370073-7bdbc47f-75b3-480b-a622-46def35cb0db](https://github.com/user-attachments/assets/7dc94078-479f-4eca-917b-a68e3e74ff16)

# Q.2.2.2

* En root, dans le fichier /etc/ssh/sshd_config.d/local.conf, ajouter la ligne : AllowUsers julie
* ![365371691-c26a0d87-2f90-457d-9b74-20a28f13858d](https://github.com/user-attachments/assets/abf41046-c3e4-4c75-a8ad-29a1678b8869)

# Q.2.2.3

* En root, dans le fichier /etc/ssh/sshd_config.d/local.conf, ajouter les ligne :
* PasswordAuthentication no
* ChallengeResponseAuthentication no
* ![365372246-2e5b984f-8905-44e2-a035-df48df6ebf50](https://github.com/user-attachments/assets/4f525f34-7eba-4f79-a707-652a613dd4e7)

# Partie 3 : Analyse du stockage

# Q.2.3.1 

* Les systemes de fichiers montés sont tmpfs, udev, /dev/md0p1 et /dev/mapper/cp3--vg-root.
* ![365374206-fd2afe44-b52a-4668-937d-e2127782ba48](https://github.com/user-attachments/assets/091e2803-c117-4ea1-b035-2843f39082e2)

# Q.2.3.2

* Les types de systemes de stockage utilisés :
* /dev/mapper/cp3--vg-root : LVM
* /dev/md0p1 : partition

# Q.2.3.3

* Pour ajouter un disque de 8 Go, aller dans Virtualbox, aller dans Configuration dans la VM Checkpoint3-SRVLX01, aller dans Stockage, cliquer sur Controlleur SATA, cliquer sur Ajoute un disque dur et lui donner 8 Go. Avac la commande lsblk, on peut voir un nouveau disque sdb.
* ![365376099-3a79a192-85b2-4522-a90f-adfee6f1d5e8](https://github.com/user-attachments/assets/b0ed9d31-488a-4fd0-96b9-97522de6adb9)
* Partitionner le disque sdb. Créer une partition et modifier son type avec la commande fdisk /dev/sdb. Cette commande ouvre l'utilitaire de partitionnement. Entrer les commandes n pour ajouter une partition, p pour créer une partition primaire, t et FD pour modifier son type en RAID Linux auto.
* 










