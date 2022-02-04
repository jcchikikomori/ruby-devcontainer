# ruby-vscode-container

VSCode's Development Container template for VSCode

## Features
- It has VSCode's Ruby extension pack
- Solargraph
- Rubocop
- Supports Apple Silicon machines

## Requirements

### Visual Studio Code

Including the following extensions:

- [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)
- [Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Your Git Config

```shell
$ cat ~/.gitconfig
```

```shell
[user]
	name = Your Full Name
	email = sample@gmail.com
[pull]
	ff = only
```

Put it in the `.devcontainer/secrets/` directory

### Your SSH keys

```shell
$ ls -lah ~/.ssh
total 80
drwxr-xr-x   8 redacted  staff   256B Feb  1 20:54 .
drwxr-x---+ 48 redacted  staff   1.5K Feb  2 09:09 ..
-rw-------@  1 redacted  staff   1.8K Jan 31 23:02 id_rsa
-rw-r--r--@  1 redacted  staff   424B Jan 31 23:02 id_rsa.pub
-rw-------   1 redacted  staff   9.2K Jan 31 23:06 known_hosts
```

Put it in the `.devcontainer/secrets/` directory

It should be like this

```shell
$ ls -lah .devcontainer/secrets/
total 80
drwxr-xr-x   8 redacted  staff   256B Feb  1 20:54 .
drwxr-x---+ 48 redacted  staff   1.5K Feb  2 09:09 ..
-rw-------@  1 redacted  staff   1.8K Jan 31 23:02 id_rsa_shared
-rw-r--r--@  1 redacted  staff   424B Jan 31 23:02 id_rsa_shared.pub
```

### Your ENV file

Copy the `example.env` into `.devcontainer/secrets/.env`

### Your database YML

- Copy the `config/database.example.yml` into `.devcontainer/secrets/database.yml`
- Since PostgreSQL on Docker requires password, edit your `.devcontainer/secrets/database.yml` like this

```yml
default: &default
  adapter: postgresql
  encoding: unicode
  # Docker internal host
  host: 172.17.0.5
  min_messages: WARNING
  username: postgres
  password: postgres
  # For details on connection pooling, see rails configuration guide
  # http://guides.rubyonrails.org/configuring.html#database-pooling
  pool: 5
```

## Docker Requirements

- Running `postgresql` container exposed with port 5432
- Running `redis` container exposed with port 6379
- [Optional] Running `portainer` container. [More details](https://docs.portainer.io/v/ce-2.11/start/install/server/docker)

## Caveats/Conditions

### Windows' WSL

Setting up your development container under WSL is just easy,
as long as you are using the official Ubuntu distro installed from Windows Store.
Also, install this following [extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) for your VSCode

### MacOS (Intel CPUs)

Same as Windows' WSL

### MacOS (Apple Silicon / M1 / M2)

Same as MacOS (Intel), but this one has a different CPU architecture, so experiment on your own

## Setup

1. Open the current project directory
2. Press Ctrl+P or Command+P
3. Type `> Remote Containers: Rebuild and Reopen in Container` then enter
<br>NOTE: This command includes the `>` character
4. And wait for the magic happening...