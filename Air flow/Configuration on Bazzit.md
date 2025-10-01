**Install podman and podman-plugins.**
```bash
sudo yum install podman podman-plugins
```

**Enable podman.socket service, then verify its status.**
```bash
systemctl enable -- user podman.socket
```

### Setup Astro Cli / Airflow:

1. Download binaries from [https://github.com/astronomer/astro-cli/releases](https://github.com/astronomer/astro-cli/releases)
2. Extract the astro-cli tar gz in to user home dir ~/bin.
3. Create a project in home directory — ]$ mkdir mytest
4. Initialize astro project

```bash
mkdir projeto_teste_airflow

```
```bash
cd projeto_teste_airflow/
```
```bash
astro dev init
```

**Configure astro to utilize podman**
```bash
astro config set container.binary podman
```

**Export DOCKER_HOST env variable.**

NOTE. You can get socket path using command:
```bash
systemctl status --user podman.socket
```

a common path looks like:
```bash
Listen: run/user/1000/podman/podman.sock
```
than

```bash
export DOCKER_HOST=unix:///<socket path>
```

Start the astro airflow from the projeto_teste_airflow
```bash
astro dev start
```