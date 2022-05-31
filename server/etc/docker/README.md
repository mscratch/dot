## Install

```bash
# Prepare the repository
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install docker, and compose
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin python3-pip

# Update configurations
sudo ln -sfv "$PWD/daemon.json" /etc/docker/daemon.json
sudo systemctl restart docker
```
