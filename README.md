# Docker Specific Version Installation

```bash
sudo apt-get update
sudo apt-get upgrade
```

1. Install packages to allow `apt` to use a repository over HTTPS:

```bash
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

