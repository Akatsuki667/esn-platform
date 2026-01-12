# Configuration Environnement

Mise à jour système : `sudo apt update && sudo apt upgrade`

### Installation outil de versionning (`Git`)

```bash
sudo apt install git -y
git --version
git version 2.43.0 # Output attendu
```

`-y` : Commande assignant la commande `Yes` demander lors du téléchargement de `Git`

### Installation Java 21 (`OpenJDK`)

```bash
sudo apt install openjdk-21-jdk -y
java -version
# Output attendu
openjdk version "21.0.9" 2025-10-21
OpenJDK Runtime Environment (build 21.0.9+10-Ubuntu-124.04)
OpenJDK 64-Bit Server VM (build 21.0.9+10-Ubuntu-124.04, mixed mode, sharing)
```

`-jdk` : Installation __Java Development Kit__ incluant : __JRE__(exécution), `javac`(compilation), Outils de développement(`javadoc`, `jar`...)

__Vérification `javac` - Java Compiler__ 

```bash
javac -version
javac 21.0.9 # Output attendu
```

Permet la compilation du code source __Java__(`.java`) en __bytecode__(`.class`)

### Installation `Node.js 20 LTS` / `npm`

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
node --version
v20.19.6 # Output attendu
npm --version
10.8.2 # Output attendu
```

### Installation `Docker`

Script officiel `Docker`

```bash
# Requête curl récupération script get-docker.sh
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

- Détecte l'OS automatiquement
- Installation de la dernière version stable

Ajout utilisateur au groupe `Docker`.

```bash
sudo usermod -aG docker $USER
```

Rechargement session.

```bash
newgrp docker
```

Vérification version.

```bash
docker --version
Docker version 29.1.4, build 0e6fee6 # Output attendu
```

__Vérification `Docker Compose`__

```bash
docker compose version
Docker Compose version v5.0.1 # Output attendu
```

Installation automatique de `Docker Compose` lors de l'instalaltion de `Docker`

---

### Date : 12 Janvier 2026