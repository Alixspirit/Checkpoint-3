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
* Il faut partitionner le disque sdb. En root, créer une partition et modifier son type avec la commande : fdisk /dev/sdb.
* Pour réparer le volume RAID, ajouter la partition sdb1 avec la commande : mdadm --manage /dev/md0 --add /dev/sdb1.
* ![365427790-8f6999e2-d2ae-4b78-a208-63a3b92a04d2](https://github.com/user-attachments/assets/efef56c6-fec8-4bd2-962e-6fe1112f8075)
* Vérifier l'état du RAID avec la commande : mdadm --detail /dev/md0
* ![365428040-d3d0efae-0a5f-45cc-af23-0f6f07118ebd](https://github.com/user-attachments/assets/c09d02d5-0925-40bf-b540-b060bf676cbd)

# Q.2.3.4

* Ajouter un disque de 2 Go. Avac la commande lsblk, on peut voir un nouveau disque sdc.
* En root, créer un volume physique avec la commande : pvcreate /dev/sdc. Créer un groupe de volume avec la commande : vgcreate mvg /dev/sdc.
* Créer un volume logique avec la commande : lvcreate -n LVM -L 2g mvg. Le resultat dit que le volume de groupe a un espace insuffisant.
* ![365433855-0ca0ee11-1207-4bc2-b546-369c1cd72f05](https://github.com/user-attachments/assets/7edde64f-62be-42f8-b6be-b06f54c43884)
* Ajouter un nouveau disque de 2 Go. On peut voir le disque sdd avec la commande lsblk.
* Créer un volume physique avec la commande : pvcreate /dev/sdd et l'ajouter au groupe de volume mvg avec la commande : vgextend mvg /dev/sdd.
* Création du systeme de fichier ext4 avec la commande : mkfs -t ext4 /dev/mvg/LVM.
* ![365435421-b9c0c31e-54ae-416b-99a4-b80fb191a26f](https://github.com/user-attachments/assets/b615c3c4-4c7e-4875-a634-4504ed0b8548)
* Monter le volume logique LVM dans le dossier /var/lib/bareos/storage avec la commande : mount /dev/mvg/LVM /var/lib/bareos/storage.
* Vérifier que le volume LVM est monté avec la commande : df -h
* ![365436966-ac671ee5-df90-48de-a76f-8620527a2400](https://github.com/user-attachments/assets/a39b72b8-76a9-4ed4-abc9-c2f23478f244)

# Q.2.3.5

* Il reste 1,8 Go.

# Partie 4 : Sauvegardes

# Q.2.4.1

* Bareos-dir permet la gestion des sauvegardes, des restaurations, des differentes ressources necessaire pour les sauvegardes et restauration, des jobs de sauvegardes et de restauration, des notifications en cas d'erreurs ou de success et des fichiers de configuration. Il communique avec les deamon bareos-sd pour la gestion du stockage,
bareos-fd pour la gestion des fichiers et bareos-bconsole pour l'interface en ligne de commande.
* Bareos-sd collecte les données a sauvegarder, assure la sécurité et l'intégrité des données et gere les attributs de fichiers. Il envoie les données collectées a bareos-sd lors de l'initialisation d'un job de sauvegarde et il permet la restauration des données lors d'une restauration.
* Bareos-fd permet la gestion du stockage des données sauvegardées, des volumes de stockage, de l'espace disponible, des erreurs et des notofications. Il stocke les données de manière fiable et securisée et permet la protection des données sensible en utilisant le chiffrement.

# Partie 5 : Filtrage et analyse réseau

# Q.2.5.1

* Les regles appliquée autorisent les paquets ipv6 contenant l'entete next header de type ipv6-icmp, les paquets ipv4 utilisant le protocole ICMP, le port 22, les paquets entrant sur l'interface reseau lo et les paquets dont l'état de suivi de connexion est marqué comme etablished ou related. Les regles interdisent les paquets dont l'état de suivi de connexion est marqué comme invalid.
* ![365444567-ce398e41-2d03-4e79-bd30-780b1316ebf3](https://github.com/user-attachments/assets/0d3c29b0-f4c7-4dcf-bfea-a8b9462c1ff5)

# Q.2.5.2

* Les types de communications autorisées sont les ping ipv4 et ipv6, la communication interne entre les processus d'une meme machine, les communications légitimes, les messages de diagnostic et de controle et les connexions ssh.

# Q.2.5.3

* Les types de communications interdites sont les connexions non authorisées et inconnues.

# Q.2.5.4

* Ajout des règles sur nftables :





