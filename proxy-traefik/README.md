#


### Activer le socket en rootless pour traefik
```Bash
systemctl --user enable podman.socket
```
- chemin = /home/${USER}/.config/systemd/user/sockets.target.wants/podman.socket

---

### Autoriser le port pour l'accès à l'interface web de traefik
```Bash
sudo firewall-cmd --add-port=8081/tcp
```