# Issues

## Current Issues

### Fedora 33

**Firefox keeps on on asking for "Please enter the password for the PKCS\#11 token PIV\_II" with a yubikey installed**

* [https://bugzilla.redhat.com/show\_bug.cgi?id=1892137](https://bugzilla.redhat.com/show_bug.cgi?id=1892137)
* [https://bugzilla.redhat.com/show\_bug.cgi?id=1742881](https://bugzilla.redhat.com/show_bug.cgi?id=1742881)

Since I don't use a smart card, my temporary solution is to remove `opensc`.

```bash
sudo dnf remove -y opensc
```

**Docker does not support nftables**

Starting with Fedora 32, `firewalld` [now defaults to nftables instead of iptables](https://fedoraproject.org/wiki/Changes/firewalld_default_to_nftables).

* [https://fedoramagazine.org/docker-and-fedora-32/](https://fedoramagazine.org/docker-and-fedora-32/)

To allow Docker to have network access, two commands are needed.

```text
sudo firewall-cmd --permanent --zone=trusted --add-interface=docker0
sudo firewall-cmd --permanent --zone=FedoraWorkstation --add-masquerade
```

## Old Issues

### Fedora 31

**Docker does not support cgroupsV2**

{% hint style="success" %}
**Update:** Docker 20.10 supports cgroup v2
{% endhint %}

* [https://github.com/docker/for-linux/issues/665\#issuecomment-548845458](https://github.com/docker/for-linux/issues/665#issuecomment-548845458)

Fedora 31 switched to using cgroupsV2 by default, which is not yet supported by container runtimes. To disable, run the following:

```text
sudo dnf install -y grubby
sudo grubby --update-kernel=ALL --args="systemd.unified_cgroup_hierarchy=0"
# Then Reboot
```

**Tss2\_Tcti\_Device\_Init\(\) Failed to open device file /dev/tpm0: No such file or directory**

* [https://bugzilla.redhat.com/show\_bug.cgi?id=1769215](https://bugzilla.redhat.com/show_bug.cgi?id=1769215)

Since I do not have a TPM device, I can safely remove `tpm2-abrmd`.

```text
sudo dnf remove -y tpm2-abrmd
```

