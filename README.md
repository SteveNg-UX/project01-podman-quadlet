# project01-quadlet

---

### Etape 1: Installer le moteur de conteneur Podman + Podman-Compose et les dépendance
- Debian / Ubuntu
```Bash
sudo apt update && sudo apt install git podman podman-compose -y
```
- RedHat / Rocky
```Bash
sudo dnf update && sudo dnf install git podman podman-compose -y
```

---

### Etape 2: Activer le maintient de la session utilisateur active même après déconnexion SSH
```Bash
# Activer le maintient
sudo loginctl enable-linger ${USER}

# Vérifier que l'output est bien : Linger=yes
loginctl show-user ${USER} | grep "Linger"
```

---

### Etape 3: Création d'arborescence pour le fonctionne des déploiement et importer le contenu d'un template dedans
```Bash
# création dossier de travail pour le quadlet
mkdir -p ~/.config/containers/systemd && ls -R ~/.config/ 

# copie de projet dans le dossier de travail
git clone https://gitlab.com/noxumbris/project01-quadlet.git && mv project01-quadlet/template-glpi/* ~/.config/containers/systemd/.
```

---

### Etape 4: Génération des units pour démarrer le pod en tant que service et vérifier que tout soit bien généré
```Bash
systemctl --user daemon-reload && systemctl --user list-unit-files | grep "generated"
```

---

### Etape 5: Démarrage du déploiement et vérifier l'état des units
```Bash
# démarrage du déploiement
systemctl --user start $(systemctl --user list-unit-files | grep "pod.service")
# vérifier l'état du unit
systemctl --user status $(systemctl --user list-unit-files | grep "pod.service")
```

---

### Etape 6: Ouverture de port si le traffic est bloqué
- Debian / Ubuntu
```Bash
PORTS2ALLOW=($(grep "PublishPort" ~/.config/containers/systemd/*.pod | cut -d'=' -f2 | cut -d':' -f1))
sudo apt install ufw -y && sudo ufw enable
for i in "${!PORTS2ALLOW[@]}"; do sudo ufw allow "${PORTS2ALLOW[$i]}/tcp"; done
```
- RedHat / Rocky
```Bash
PORTS2ALLOW=($(grep "PublishPort" ~/.config/containers/systemd/*.pod | cut -d'=' -f2 | cut -d':' -f1))
for i in "${!PORTS2ALLOW[@]}"; do sudo firewall-cmd --add-port="${PORTS2ALLOW[$i]}/tcp" --permanent; done
sudo firewall-cmd --reload
```

---

### Etape 7: Vérifier l'état des containers
```Bash
podman ps
```

---

### Etape 8: Accéder à l'interface web de l'application
accéder à l'interace GLPI via le navigateur http://(ip_hote):(port_pod)