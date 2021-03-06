# Prepare Fresh Install

To Do:

* [ ] Learn how to use SELinux instead of disabling it.

### Download & Install OS

[https://getfedora.org/en/workstation/download/](https://getfedora.org/en/workstation/download/)

### Upgrade

```bash
# First, some DNF optimizations:
echo 'max_parallel_downloads=10' | sudo tee -a /etc/dnf/dnf.conf
echo 'fastestmirror=True' | sudo tee -a /etc/dnf/dnf.conf

# Upgrade:
sudo dnf upgrade -y
```

### Disable SELinux

{% hint style="warning" %}
This is not ideal, but I disable it because I don't know how to use it.
{% endhint %}

```bash
sudo sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/selinux/config
```

### Install [Etckeeper](http://etckeeper.branchable.com/)

> etckeeper is a collection of tools to let `/etc` be stored in a git, mercurial, bazaar or darcs repository. This lets you use git to review or revert changes that were made to `/etc`. Or even push the repository elsewhere for backups or cherry-picking configuration changes.
>
> It hooks into package managers like apt to automatically commit changes made to /etc during package upgrades. It tracks file metadata that git does not normally support, but that is important for /etc, such as the permissions of `/etc/shadow`.

```bash
sudo dnf install -y etckeeper etckeeper-dnf
sudo etckeeper init
```

### 



