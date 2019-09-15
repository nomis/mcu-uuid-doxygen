.PHONY: build clean pull
.SUFFIXES:
.SECONDARY:

build: git-common git-log git-syslog git-console git-telnetd | pull
	(cat Doxyfile; echo STRIP_FROM_INC_PATH += $(patsubst git-%,$$PWD/mcu-uuid-%/src,$^)) | doxygen -

www: build
	rsync -ac --delete-after --exclude=.snapshots ./html/ ~/www/

mcu-uuid-%:
	git clone -q "https://github.com/nomis/$@"

git-%: mcu-uuid-%
	cd "$<" && git fetch -q && git reset --hard origin/master

pull:
	git pull -q

clean:
	rm -rf html mcu-uuid-*
