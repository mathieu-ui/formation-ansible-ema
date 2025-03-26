# Ansible par la pratique (6) – Configuration de base

Ajout dans /etc/hosts :

```bash
192.168.56.20 target01.sandbox.lan target01
192.168.56.30 target02.sandbox.lan target02
192.168.56.40 target03.sandbox.lan target03 
```

> Comme dans 04-Authentification je configure l'authentification SSH

J'installe ansibe avec :

```bash
sudo apt-add-repository ppa:ansible/ansible
sudo apt install -y ansible
```

Je fait le ping avec ansible :

```bash
ansible all -i target01,target02,target03 -m ping
```

![img](./img/Screenshot_20250324_112953.png)

Je crée le fichier de configuration dans le répertoire monprojet :

![img](./img/Screenshot_20250324_113152.png)

Je configure mon inventaire et le path de mes logs :

![img](./img/Screenshot_20250324_113701.png)

Je test ma configuration :

![img](./img/Screenshot_20250324_113757.png)

Les logs sont bien mis dans ~/journal :

![img](./img/Screenshot_20250324_113841.png)

Je modifie mon inventaire :

![img](./img/Screenshot_20250324_114809.png)

Le ping fonctionne toujours :

![img](./img/Screenshot_20250324_114842.png)

Je peux aussi, avec cette configuration afficher le /etc/shadow

![img](./img/Screenshot_20250324_114952.png)
