# Tutorial on basic SSH and Jupyter Notebook

## Setup your SSH access

Please go through the following procedure to set up your SSH access to
your group servers.

1. Generate your SSH key-pair by `ssh-keygen -t rsa -b 4096`. For more,
   refer to https://docs.gitlab.com/ee/ssh/.

2. Contact your server admin and send him/her your SSH pub key
   `~/.ssh/id_rsa.pub`, to set up your SSH pub key for authentication.
   (**WARNING**: DO NOT send your private key `~/.ssh/id_rsa` and keep
   it safe!)

3. Edit `~/.ssh/config` to configure your SSH connection for convenience
   (not necessary, but help you to avoid typing the long IPs every
   time). For other servers, refer to Section *Available servers*.

   ```
   Host YOUR_SERVER_ID
       Hostname YOUR_SERVER_IP
       User YOUR_SERVER_USER
       Port YOUR_SERVER_PORT
   ```

   where `YOUR_SERVER_ID` is any name you choose, e.g. `mylab`;
   `YOUR_SERVER_IP` is the global IP or domain name your server;
   `YOUR_SERVER_USER` is the login user on your server; and
   `YOUR_SERVER_PORT` is the port number your server set to offer SSH
   (or TCP) service.

   For example:
   ```
   Host mylab
       HostName 41hz592037.wicp.vip
       Port 55811
       User lab8888    
   ```
   
4. Once you got confirmed with key setup from your admin, you now
   can access SSH server by `ssh YOUR_SERVER_ID`.

> **Warning**: The insecure login via password to SSH servers
> will be completely invalidated soon!

## How to run and connect to Jupyter Notebook on a remote SSH server

1. SSH connect to remote server by `ssh YOUR_SERVER_ID` and insert your password (if you don't use your SSH key authentication).

2. On remote server, run the jupyter notebook web sever by `jupyter notebook --no-browser`. If you like to use different jupyter notebook process on the server, set a different port by `jupyter notebook --port=XXXX --no-browser` (When in connection, use your own port number).

3. On your local machine, run `ssh -NL 8080:localhost:8888
YOUR_SERVER_ID` to build up a SSH tunneling to remote server. If you change your own port number, change `8888` to yours.

4. Use the URL `localhost:8080` in your web browser (local machine) to
   access the Jupyter Notebook on the remote server.

> **Note**: Variable `YOUR_SERVER_ID` can be the specific URLs of SSH
> servers (in next section), or any identifier names specified by your
> `~/.ssh/config`.

> **Tips**: You may add one more `&` at the end of the above commands in
> `Step 2,3` to bring them to the background. It allows the command to
> keep running even when you log out or kill your terminal. To bring
> them to foreground (i.e. the normal running), use `fg`; to list the
> commands running in background, use `bg`.

> **Note**: If you have altered the port number in your Jupyter config
> file (in `~/.jupyter/`), e.g., `1224`, you choose replace the 1st
> `8888` in Step 3 with `1224`.

> **Note**: If you do not specify the port number when starting Jupyter notebook and there have been some Jupyter notebook processes running in the background, the next Jupyter process will use the port number incremented by 1. For example, you have two Jupyter processes running, which by default use `8888`and `8889`, your new Jupyter process will use port `8890` by default. To check how many Jupyter processes in background, use `ps aux | grep jupyter`.

### A demo to use an SSH server

Suppose that `~/.ssh/config` has configured `mylab` (see `config` given in Section *Available servers* for every specific server).

In terminals,

1. (local machine) `ssh mylab`
2. (remote server) `jupyter notebook --port=8888 --no-browser &`
3. (local machine) `ssh -NL 8080:localhost:8888 mylab &`
4. (local machine) web browser to open the URL: `localhost:8080`
5. done! enjoy your Jupyter notebook :)

> **Tips**: You may set aliases in your `~/.bashrc` to accelerate
> your start every time. For example, in remote server, add `alias
> jp="jupyter notebook --no-browser"`; in local machine, add `alias
> jp="ssh -NL 8080:localhost:8888 mylab &"`. Now you can just type `jp`
> twice (one in ssh-ed terminal, one in local, and you have Jupyter
> Notebook in your local web browser to work with.

### Alternative using 花生壳

> **Warning**: The HTTP redirection in 花生壳 has been turned off.

The operations to setup ssh and access servers (step 1, 2) will be the
same. The difference is that `step 3,4` can be replaced by an automatic
HTTP redirection service by 花生壳. In the console of 花生壳, let the
HTTP map to `127.0.0.1:8888`, i.e. `localhost:8888` the default IP and
port used by Jupyter notebook. Now once you run the Jupyter notebook on
your server, you can open it via you local web browser using the URL
provided by 花生壳.

Procedure:

1. ssh your server (`ssh mylab`) and start Jupyter notebook (`jp`);
2. open in web browser using the domain name from 花生壳.

Pros: It is easy to set and use.

Cons:

1. You have to alter 花生壳 console HTTP mapping configuration every time, whenever you like to use Jupyter notebook with a different port number (rather than 8888).

2. All users will use the same Jupyter notebook process, which may freeze everyone whenever something happens in someone's codes.

3. **IMPORTANT**: It is NOT safe at all on the Internet when you just use a  password! Note that someone can access your server via your Jupyter notebook!!

In a word, DON'T use 花生壳 http direct mapping for Jupyter notebook, use SSH tunnel instead.

```bash
jupyter notebook --port=1234 --no-browser
ssh -NL 8080:localhost:1234 i38944o710.goho.co

```

