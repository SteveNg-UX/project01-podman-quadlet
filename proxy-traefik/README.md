#


### Activer le socket en rootless pour traefik
```Bash
systemctl --user enable podman.socket
```
- chemin = /run/user/${USER}/podman/podman.sock:/var/run/docker.sock

---

### Autoriser le port pour l'accès à l'interface web de traefik
```Bash
sudo firewall-cmd --add-port=8081/tcp
```

---

### Charger les units
```Bash
systemctl --user daemon-reload && systemctl --user list-unit-files | grep "generated"
```

---

### Lancer les unit
```Bash
systemctl --user start project01.pod
```