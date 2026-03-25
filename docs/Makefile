#!/usr/bin/make

DEST?=	tmp
VERSIONMASK?=	0
CONTRIB?=	../contrib
CONTRIB:=	$(abspath $(CONTRIB))
XSLS?=	$(CONTRIB)/xslscript/xslscript.pl

PACKAGES=	freenginx						\
		freenginx-module-auth-spnego				\
		freenginx-module-brotli					\
		freenginx-module-encrypted-session			\
		freenginx-module-geoip					\
		freenginx-module-geoip2					\
		freenginx-module-headers-more				\
		freenginx-module-image-filter				\
		freenginx-module-lua					\
		freenginx-module-ndk					\
		freenginx-module-njs					\
		freenginx-module-passenger				\
		freenginx-module-perl					\
		freenginx-module-rtmp					\
		freenginx-module-set-misc				\
		freenginx-module-subs-filter				\
		freenginx-module-xslt

all:		changes changelogs

changes:	$(DEST)/CHANGES

changelogs:	$(addsuffix .rpm-changelog, $(addprefix $(DEST)/, $(PACKAGES))) \
		$(addsuffix .deb-changelog, $(addprefix $(DEST)/, $(PACKAGES)))

$(XSLS):
	cd $(CONTRIB) && make .xslscript

$(DEST)/CHANGES:		changes.dtd				\
				freenginx.xml				\
				change_log_conf.xml			\
				changes.xslt

	mkdir -p $(DEST)

	xmllint --noout --valid freenginx.xml
	xsltproc --stringparam format generic				\
		-o $@ changes.xslt freenginx.xml

$(DEST)/%.rpm-changelog:	changes.dtd 				\
				%.xml 				\
				change_log_conf.xml 			\
				changes.xslt
	mkdir -p $(DEST)
	xmllint --noout --valid $*.xml
	xsltproc --stringparam pkgname $* --stringparam format rpm	\
		--stringparam versionmask $(VERSIONMASK)		\
		-o $@ changes.xslt $*.xml

$(DEST)/%.deb-changelog:	changes.dtd 				\
				%.xml 				\
				change_log_conf.xml 			\
				changes.xslt
	mkdir -p $(DEST)
	xmllint --noout --valid $*.xml
	xsltproc --stringparam pkgname $* --stringparam format deb	\
		--stringparam versionmask $(VERSIONMASK)		\
		-o $@ changes.xslt $*.xml

changes.xslt:	changes.xsls $(XSLS)
	$(XSLS) -o $@ $<

clean:
	rm -rf $(DEST)
