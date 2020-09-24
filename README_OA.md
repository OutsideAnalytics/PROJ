# Contents
PROJ build for Outside Analytics Deneir.

# RPM Build Instructions
## RedHat 8
```
git clone https://github.com/OutsideAnalytics/deneir_PROJ.git
cd deneir_PROJ
checkout oa-build
./autogen.sh
./configure
make rpm "VERSION=6.2.1" "RELEASE=0"
cd rpmbuild/RPMS/x86_64
dnf install oa-proj6-6.2.1-2.el8.x86_64.rpm

```
Notes:
* If a git tag exists that matches the VERSION number, then that tag is built, otherwise
the HEAD of the current branch is built.
* The ./configure step is required to generate the makefiles for the RPM build. 
* The RPM produced is in *deneir_PROJ/rpmbuild/RPMS/x86_64/*

# Dependency lists
## RedHat 8
Base Image: _registry.access.redhat.com/ubi8/ubi_

### RedHat 8 packages
```
sqlite     3.26.0
```
