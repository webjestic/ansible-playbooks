# mac-dev-playbook

https://www.talkingquickly.co.uk/2021/01/macos-setup-with-ansible/

https://github.com/TalkingQuickly/ansible-osx-setup

https://docs.ansible.com/ansible/latest/collections/community/general/index.html

https://developer.apple.com/download/all/?q=XCode

`gem which cocoapods`

`/usr/bin/xcodebuild -version`

---
## Requirements

### [Homebrew](https://brew.sh/)

```bash
# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### [Ansible](https://www.ansible.com/)

```bash
# Install Ansible
brew install ansible

# Use Galaxy to install Roles and Collections https://galaxy.ansible.com/community/general
ansible-galaxy collection install community.general

```

---

## Commands
```bash
# Playbook commands
ansible-playbook --version
ansible-playbook -i inventory playbooks/osx_m1_dev/main.yml --syntax-check
ansible-playbook -i inventory playbooks/osx_m1_dev/main.yml --ask-become-pass
ansible-playbook -i inventory playbooks/osx_m1_dev/main.yml --ask-vault-pass
ansible-playbook -i inventory playbooks/osx_m1_dev/main.yml --ask-sudo-pass

# Galaxy commands
ansible-galaxy --version
ansible-galaxy install -r requirements.yml # install your custom requirements
ansible-galaxy collection list
ansible-galaxy collection install community.general --upgrade

# Vault commands
ansible-vault --version
ansible-vault encrypt vault-secrets.yml # myvault
ansible-vault view vault-secrets.yml
ansible-vault decrypt vault-secrets.yml

# Vault use in Playbooks
vars_files:
  - vault-secrets.yml
tasks:
  - name: Pull from repo
    git: https://username:{{ git_password }}@github.com/username/reponame.git

```
---

## Homebrew

Homebrew ideally is the primary source for installing software on our mac. Therefore, it is important 
to understand the different types of software that can be installed with Homebrew.

- Tap - Taps are git repos that can be installed. Repos are added as a tap, and then installed. </br>
(`brew tap heroku/brew && brew install heroku`)
Homebrew taps installed through Ansible are done with the [Homebrew Tap Module](https://docs.ansible.com/ansible/latest/collections/community/general/homebrew_tap_module.html#ansible-collections-community-general-homebrew-tap-module)

- Cask - A cask is a UI style Application, such as Firefox</br>
(`brew install --cask firefox`)
Homebrew casks installed through Ansible are done with the [Homebrew Cask Module](https://docs.ansible.com/ansible/latest/collections/community/general/homebrew_cask_module.html#ansible-collections-community-general-homebrew-cask-module)

- Package - A package is often a terminal application, such as wget</br>
(`brew install wget`)</br>
Homebrew packages are installed through Ansible are done with the [Homebrew Module](https://docs.ansible.com/ansible/latest/collections/community/general/homebrew_module.html#ansible-collections-community-general-homebrew-module)

---
## What Get's Installed

- zsh + oh-my-zsh
- openssl
- gupnp (gpg)

- openjdk

- nvm
- node
- npm

- xcode

- fvm
- flutter
- cocoapods

- VS Studio Code
- Android Studio

- redis
- redis insight

- mongo
- mongo-cli
- mongo-compass

- kubectl
- doctl

- docker
- postman

## Created Folders
```
~
└── Documents
    └── Dev
        ├── certs
        ├── code
        ├── keys
        ├── lib
        └── sandbox
```
