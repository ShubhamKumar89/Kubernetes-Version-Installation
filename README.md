# Docker Specific Version Installation

1. Install packages to allow `apt` to use a repository over HTTPS:

```bash
# update packages
sudo apt-get update
sudo apt-get upgrade

sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

2. Add Docker’s official GPG key:

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

3. Use the following command to set up the repository:

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  ```

4. Update the `apt` package index:

```bash
sudo apt-get update
```

If you receive a GPG error while running `apt-get update`, then try granting read permission for the Docker public key file before updating the package index:

```bash
sudo chmod a+r /etc/apt/keyrings/docker.gpg
sudo apt-get update
```

5. To install a specific version of Docker Engine, start by list the available versions in the repository:

```bash
apt-cache madison docker-ce | awk '{ print $3 }'
```

![image](https://user-images.githubusercontent.com/97805339/205437394-b95522a2-0957-415f-8b0a-81bdabf0104a.png)

6. Select the desired version and install:

```bash
VERSION_STRING=5:20.10.0~3-0~ubuntu-focal

# Install Docker Engine, containerd, and Docker Compose
sudo apt-get install docker-ce=$VERSION_STRING docker-ce-cli=$VERSION_STRING containerd.io docker-compose-plugin
```

7. Check the installed docker version:

```bash
docker version
```

![image](https://user-images.githubusercontent.com/97805339/205437653-5c061a78-30ce-4d0a-9913-50af6be0a79d.png)

#### Run docker without `sudo`:

```
sudo usermod -aG docker ${USER}
su - ${USER}
sudo chmod 666 /var/run/docker.sock
```
