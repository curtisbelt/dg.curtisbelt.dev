# Bug Workarounds

* Remove opensc \(Fedora 33\)
  * See [https://bugzilla.redhat.com/show\_bug.cgi?id=1742881](https://bugzilla.redhat.com/show_bug.cgi?id=1742881) and [https://bugzilla.redhat.com/show\_bug.cgi?id=1892137](https://bugzilla.redhat.com/show_bug.cgi?id=1892137)
  * sudo dnf remove -y opensc
* Fedora 31 switched to using cgroupsV2 by default, which is not yet supported by container runtimes. To disable, run the followinghttps://github.com/docker/for-linux/issues/665\#issuecomment-548845458
  * sudo dnf install -y grubby
  * sudo grubby --update-kernel=ALL --args="systemd.unified\_cgroup\_hierarchy=0"
* \(Fedora &lt;=31\) Remove tpm2-abrmd as I do not have a TPM device \([https://en.wikipedia.org/wiki/Trusted\_Platform\_Module](https://en.wikipedia.org/wiki/Trusted_Platform_Module)\) and the daemon keeps retrying \([https://bugzilla.redhat.com/show\_bug.cgi?id=1769215](https://bugzilla.redhat.com/show_bug.cgi?id=1769215)\)
  * sudo dnf remove -y tpm2-abrmd

