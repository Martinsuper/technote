## ubuntu 免 sudo执行

```bash
sudo gpasswd -a ${USER} docker
newgrp docker
# sudo service docker restart
```

