<!--
Copyright (C) 2021-2025 Robert Wimmer
SPDX-License-Identifier: GPL-3.0-or-later
-->

# Changelog

## 0.9.1+1.6.2

- update `cni_version` to `1.6.2`

## 0.9.0+1.6.1

- update `cni_version` to `1.6.1`

## 0.8.0+1.5.1

- update `cni_version` to `1.5.1`

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

## 0.4.0+1.2.0

- update `cni_version` to `1.2.0`
- fix Molecule `converge.yml`

## 0.3.0+1.1.1

- fix various `ansible-lint' issues
- add Github release action to push new release to Ansible Galaxy

## 0.2.0+1.1.1

- update `cni_version` to `1.1.1`
- add `CHANGELOG`

## 0.1.0+1.0.1

- initial commit
