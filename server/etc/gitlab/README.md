## Install on Ubuntu 20.04

```bash
# Prepare the configuration files
cd dot/server/etc/gitlab
sudo mkdir /etc/gitlab
sudo ln -sfv "$PWD/gitlab.rb" /etc/gitlab/gitlab.rb # TODO: permission?

# Install GitLab (CN ver)
curl -fsSL https://packages.gitlab.cn/repository/raw/scripts/setup.sh | /bin/bash
sudo sed -i 's/jammy/focal/g' /etc/apt/sources.list.d/gitlab-jh.list # workaround for 22.04...
sudo apt install gitlab-jh

# Get the password of root
sudo cat /etc/gitlab/initial_root_password
```
