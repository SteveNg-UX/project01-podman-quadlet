# project01-quadlet

### Etape :
1. Installer le moteur de conteneur Podman + Podman-Compose
2. Activer le maintient de la session utilisateur active même après déconnexion SSH
3. Création d'arborescence pour le fonctionne des déploiement
4. Copier/Coller le/les templates dans le dossier de l'arborescence créé précédemment

---

### Etape 1: Installer le moteur de conteneur Podman + Podman-Compose

---

### Etape 2: Activer le maintient de la session utilisateur active même après déconnexion SSH
```Bash
# Activer le maintient
sudo loginctl enable-linger ${USER}
# Vérifier que l'output est bien : Linger=yes
loginctl show-user ${USER} | grep "Linger"
```

---

### Etape 3: Création d'arborescence pour le fonctionne des déploiement
```Bash
mkdir -p ~/.config/containers/systemd && ls -R ~/.config/ 
```

---

### Etape 4. Copier/Coller le/les templates dans le dossier de l'arborescence créé précédemment
```Bash
git clone https://gitlab.com/noxumbris/project01-quadlet.git ~/.config/containers/systemd/.
```