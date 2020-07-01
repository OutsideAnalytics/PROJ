SUBDIRS	=	include src man data cmake
DIST_SUBDIRS = include src man data cmake test

EXTRA_DIST = CMakeLists.txt CITATION README.md

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = proj.pc

AUTOMAKE_OPTIONS =	dist-zip
ACLOCAL_AMFLAGS =	-I m4

check-local:
	cd test; $(MAKE) check

all-local: README

README: README.md
	fgrep -v "[![" $< > $@

clean-local:
	$(RM) README


# -------- Outside Analytics Additions -------
buildchk:
	@if [[ ! -n $$VERSION ]] || [[ ! -n $$RELEASE ]]; \
	then \
	  echo "Usage: make rpm \"VERSION=x.y.z\" \"RELEASE=n\""; \
	  exit 1; \
	fi

rpm: buildchk
	@mkdir -p rpmbuild/{BUILD,BUILDROOT,RPMS,SOURCES,SPECS,SRPMS}
	@if [[ -n `git tag --list ${VERSION}` ]]; \
	then \
	  echo "Extracting git archive for tag: ${VERSION}"; \
	  git archive --format tar.gz \
	              --output=rpmbuild/SOURCES/proj-${VERSION}.tar.gz \
	              --prefix=proj-${VERSION}/ \
	              ${VERSION}; \
	else \
	  echo "Extracting git archive for HEAD (tag not found for: ${VERSION})"; \
	  git archive --format tar.gz \
	              --output=rpmbuild/SOURCES/proj-${VERSION}.tar.gz \
	              --prefix=proj-${VERSION}/ \
	              HEAD; \
	fi
	sed -e 's,xVERSIONx,${VERSION},' \
	    -e 's,xRELEASEx,${RELEASE},' \
	    proj6.spec >| rpmbuild/SPECS/proj6.spec
	cd rpmbuild/SPECS; \
	  rpmbuild --define "_topdir $$PWD/.." -ba proj6.spec
	@echo "Makefile.rpm done. Result in: $$PWD/rpmbuild/RPMS/x86_64"

