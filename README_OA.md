# Outside Analytics RPM build instructions
git clone https://github.com/OutsideAnalytics/deneir_PROJ.git
cd deneir_PROJ
checkout oa-build
./autogen.sh
./configure
make rpm "VERSION=6.2.1" "RELEASE=0"
# rpm in ./rpmbuild/RPMS/x86_64
