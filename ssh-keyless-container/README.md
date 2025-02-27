# SSH keyless authentication Ubuntu SSH server

<h2>First build the container</h2>

```bash
docker build -t ssh-demo .
```

<h2>Now run the container either in the background with "-d" or like below to show STOUT and SSH logs</h2>

```bash
docker run --rm -it -p 2222:22 --name dw-ssh ssh-demo
```