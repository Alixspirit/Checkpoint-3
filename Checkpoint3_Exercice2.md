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
* PasswordAuthentication no et ChallengeResponseAuthentication no
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

* Ajouter un disque de 8 Go. Avac la commande lsblk, on peut voir un nouveau disque sdb.
* ![365376099-3a79a192-85b2-4522-a90f-adfee6f1d5e8](https://github.com/user-attachments/assets/b0ed9d31-488a-4fd0-96b9-97522de6adb9)
* Il faut partitionner le disque sdb. En root, créer une partition et modifier son type avec la commande : fdisk /dev/sdb. Cette commande ouvre l'utilitaire de partitionnement. Entrer les commandes n pour ajouter une partition, p pour créer une partition primaire, t et FD pour modifier son type en RAID Linux auto.
* Pour réparer le volume RAID, ajouter la partition sdb1 avec la commande : mdadm --manage /dev/md0 --add /dev/sdb1.
* ![365427790-8f6999e2-d2ae-4b78-a208-63a3b92a04d2](https://github.com/user-attachments/assets/efef56c6-fec8-4bd2-962e-6fe1112f8075)
* Vérifier l'état du RAID avec la commande : mdadm --detail /dev/md0
* ![365428040-d3d0efae-0a5f-45cc-af23-0f6f07118ebd](https://github.com/user-attachments/assets/c09d02d5-0925-40bf-b540-b060bf676cbd)

# Q.2.3.4

* Ajouter un disque de 2 Go, aller dans Virtualbox, aller dans Configuration dans la VM Checkpoint3-SRVLX01, aller dans Stockage, cliquer sur Controlleur SATA, cliquer sur Ajoute un disque dur et lui donner 2 Go. Avac la commande lsblk, on peut voir un nouveau disque sdc.
* Créer un volume physique avec la commande : pvcreate /dev/sdc. Créer un groupe de volume avec la commande : vgcreate mvg /dev/sdc.
* Créer un volume logique avec la commande : lvcreate -n LVM -L 2g mvg. Le resultat dit que le volume de groupe a un espace insuffisant.
* ![365433855-0ca0ee11-1207-4bc2-b546-369c1cd72f05](https://github.com/user-attachments/assets/7edde64f-62be-42f8-b6be-b06f54c43884)
* Donc ajouter un nouveau disque de 2 Go. On peut voir le disque sdd avec la commande lsblk.
* Créer un volume physique avec la commande : pvcreate /dev/sdd et l'ajouter au groupe de volume mvg avec la commande : vgextend mvg /dev/sdd.
* Création du systeme de fichier ext4 avec la commande : mkfs -t ext4 /dev/mvg/LVM.
* ![365435421-b9c0c31e-54ae-416b-99a4-b80fb191a26f](https://github.com/user-attachments/assets/b615c3c4-4c7e-4875-a634-4504ed0b8548)
* Créer le dossier mnt avec la commande : mkdir mnt et monter le volume logique LVM dans ce dossier avec la commande : mount /dev/mvg/LVM /mnt.
* Vérifier que le volume LVM est monté avec la commande : df -h
* ![365436097-3b65d411-460f-4e38-9761-f37042ca3695](https://github.com/user-attachments/assets/b8c58111-da18-426c-8ec9-7d5cc2c3173f)








