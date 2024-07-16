ansible-role-cni
================

Ansible role to install [CNI - Container Network Interface](https://github.com/containernetworking/plugins). [CNI](https://www.cni.dev/) (Container Network Interface), a Cloud Native Computing Foundation project, consists of a specification and libraries for writing plugins to configure network interfaces in Linux containers, along with a number of supported plugins. CNI concerns itself only with network connectivity of containers and removing allocated resources when the container is deleted. Because of this focus, CNI has a wide range of support and the specification is simple to implement.

Changelog
---------

**Change history:**

See full [CHANGELOG](https://github.com/githubixx/ansible-role-cni/blob/master/CHANGELOG.md)

**Recent changes:**

## 0.7.0+1.4.0

- add Ubuntu `24.04` support

## 0.6.0+1.4.0

- update `cni_version` to `1.4.0`

## 0.5.1+1.3.0

- adjust unarchive directory mode
- add sub path to `cni_tmp_directory` value to avoid change of permissions of parent directory. If `cni_tmp_directory` was set to `/tmp` the `unarchive` operation changed the mode of that directory. Adding a static sub path to `cni_tmp_directory` avoids the problem.

## 0.5.0+1.3.0

- update `cni_version` to `1.3.0`
- add Molecule verify step
- remove Ubuntu `18.04` support (reached EOL)
- add Ubuntu `22.04` support
- add `dummy` and `tap` CNI binaries
- rename Molecule `kvm` scenario to `default` / move `memory` + `cpus` options to boxes

Role Variables
--------------

```yaml
# CNI plugin version
cni_version: "1.4.0"

# CNI binary directory
cni_bin_directory: "/opt/cni/bin"

# CNI configuration directory
cni_conf_directory: "/etc/cni/net.d"

# Directory to store the archive
cni_tmp_directory: "{{ lookup('env', 'TMPDIR') | default('/tmp', true) }}"

# Owner/group of "CNI" files/directories. If the variables are not set
# the resulting binary will be owned by the current user.
cni_owner: "root"
cni_group: "root"

# Specifies the permissions of the "CNI" binaries
cni_binary_mode: "0755"

# Operating system
# Possible options: "linux", "windows"
cni_os: "linux"

# Processor architecture "CNI" should run on.
# Other possible values: "arm", "arm64", "mips64le", "ppc64le", "s390x"
cni_arch: "amd64"

# Name of the archive file name
cni_archive: "cni-plugins-{{ cni_os }}-{{ cni_arch }}-v{{ cni_version }}.tgz"

# The CNI download URL (normally no need to change it)
cni_url: "https://github.com/containernetworking/plugins/releases/download/v{{ cni_version }}/{{ cni_archive }}"

# Restart "kubelet" service after "CNI" binaries or configuration have changed.
# This handler expects a systemd service called "kubelet.service".
cni_restart_kubelet: false
```

TODO
----

- Distribute CNI network configuration files (for [Cilium](https://cilium.io/) this is not needed as CNI files are created by Cilium)

Example Playbook
----------------

```yaml
- hosts: your-host
  roles:
    - githubixx.cni
```

Testing
-------

This role has a small test setup that is created using [Molecule](https://github.com/ansible-community/molecule), libvirt (vagrant-libvirt) and QEMU/KVM. Please see my blog post [Testing Ansible roles with Molecule, libvirt (vagrant-libvirt) and QEMU/KVM](https://www.tauceti.blog/posts/testing-ansible-roles-with-molecule-libvirt-vagrant-qemu-kvm/) how to setup. The test configuration is [here](https://github.com/githubixx/ansible-role-cni/tree/master/molecule/kvm).

Afterwards molecule can be executed:

```bash
molecule converge
```

This will setup a few virtual machines (VM) with different supported Linux operating systems and installs `CNI`.

To run a few tests:

```bash
molecule verify
```

To clean up run

```bash
molecule destroy
```

License
-------

GNU GENERAL PUBLIC LICENSE Version 3

Author Information
------------------

[http://www.tauceti.blog](http://www.tauceti.blog)
