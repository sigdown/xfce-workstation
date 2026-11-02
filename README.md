# xfce-workstation

## Solve chicken and egg problem

First of all, create sudo user for remote administation to solve chicken and egg problem.

1. Generate SSH key.

```bash
ssh-keygen -t ed25519 -C "xfce-workstation"
```

2. Connect as root to create sudo user.

```bash
ssh root@<machine_ip>

adduser deb-adm

usermod -aG sudo deb-adm

su -- deb-adm

cd ~
```

3. Create `~/.ssh` directory and add your public key.

```bash
mkdir -p ~/.ssh && cd ~/.ssh

vi authorized_keys # you can use nano
```

4. Remove sudo password if you have one

```bash
sudo EDITOR=vi visudo
```

Now sudo user is ready.

5. Add your server to hosts.yaml

```bash
cp .env.example .env

vi env

set -a

source .env

set +a
```

## Using Ansible

1. Roll Ansible playbook

```bash
ansible-playbook playbooks/site.yaml
```