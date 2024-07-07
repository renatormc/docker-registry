```bash
mkdir -p .local/certs .local/auth .local/data
```

```bash
openssl req -newkey rsa:4096 -nodes -sha256 -keyout .local/certs/domain.key -x509 -days 365 -out .local/certs/domain.crt

```

# Authentication
```bash
sudo apt-get install apache2-utils
mkdir auth
htpasswd -Bc .local/auth/htpasswd [USERNAME]
```

# Configure Docker to Use Your Secure Registry

```bash
sudo mkdir -p /etc/docker/certs.d/localhost:5000
sudo cp .local/certs/domain.crt /etc/docker/certs.d/localhost:5000/ca.crt
sudo systemctl restart docker

```

```bash
docker tag [IMAGE_NAME] localhost:5000/[IMAGE_NAME]
docker push localhost:5000/[IMAGE_NAME]
```