### Update package lists and install essential packages
```bash
sudo apt update
sudo apt install -y curl openssl iptables build-essential protobuf-compiler git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev tar clang bsdmainutils ncdu unzip libleveldb-dev libclang-dev ninja-build
```

### Remove conflicting Docker packages (if any)
```bash
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt remove -y $pkg || true; done
```

### Install Docker prerequisites
```bash
sudo apt install -y ca-certificates curl gnupg software-properties-common
```

### Add Docker’s GPG key
```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

### Add Docker repository
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Install Docker
```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Start and enable Docker service
```bash
sudo systemctl start docker
sudo systemctl enable docker
```

### Add current user to Docker group
```bash
sudo usermod -aG docker $USER
echo "Log out and back in, or run 'newgrp docker' to apply group changes."
```

### Verify Docker installation
```bash
docker run hello-world
```

### Pull the Succinct Prover CPU Docker image
```bash
docker pull public.ecr.aws/succinct-labs/spn-node:latest-cpu
```
