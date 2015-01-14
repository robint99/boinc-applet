SUBDIRS =

applet_SCRIPTS = boinc_applet.py boinc_client.py rpc.py about_win.py \
		 status_win.py prefs_win.py
appletdir = $(libexecdir)

APPLET_LOCATION = $(libexecdir)/boinc_applet.py

appletsdir       = $(datadir)/mate-panel/applets
applets_in_files = org.mate.panel.BoincMonitorApplet.mate-panel-applet.in 
applets_DATA     = $(applets_in_files:.mate-panel-applet.in=.mate-panel-applet)

do_substitution = $(AM_V_GEN)sed \
		  -e 's,[@]pythondir[@],$(pythondir),g' \
		  -e 's,[@]PACKAGE[@],$(PACKAGE),g' \
		  -e 's,[@]VERSION[@],$(VERSION),g' \
		  -e 's,[@]LOCATION[@],$(appletdir),g'

#$(applets_in_files): $(applets_in_files).in Makefile
#	$(AM_V_GEN)sed \
#		-e "s|\@LOCATION\@|$(appletdir)|" \
#		-e "s|\@pythondir\@|$(pythondir)|" \
#	  	-e "s|\@PACKAGE\@|$(PACKAGE)|" \
#	  	-e "s|\@VERSION\@|$(VERSION)|" \
#		$< > $@

%.mate-panel-applet: %.mate-panel-applet.in Makefile
	$(AM_V_GEN)sed \
		-e "s|\@LOCATION\@|$(appletdir)|" \
		-e "s|\@pythondir\@|$(pythondir)|" \
	  	-e "s|\@PACKAGE\@|$(PACKAGE)|" \
	  	-e "s|\@VERSION\@|$(VERSION)|" \
		$< > $@

servicedir       = $(datadir)/dbus-1/services
service_in_files = org.mate.panel.applet.BoincMonitorAppletFactory.service.in
service_DATA     = $(service_in_files:.service.in=.service)

imagedir	 = $(libexecdir)
image_DATA	 = sahsl.png \
		   sahsd.png

gsettings_SCHEMAS = org.mate.panel.applet.BoincMonitor.gschema.xml
@GSETTINGS_RULES@

org.mate.panel.applet.BoincMonitorAppletFactory.service: $(service_in_files)
	$(AM_V_GEN)sed \
		-e "s|\@LOCATION\@|$(APPLET_LOCATION)|" \
		$< > $@

boinc_applet.py: boinc_applet.in Makefile
	$(do_substitution) < $(srcdir)/boinc_applet.in > boinc_applet.py
	chmod +x boinc_applet.py

boinc_client.py: boinc_client.in Makefile
	$(do_substitution) < $(srcdir)/boinc_client.in > boinc_client.py
	chmod +x boinc_client.py

rpc.py: rpc.in Makefile
	$(do_substitution) < $(srcdir)/rpc.in > rpc.py
	chmod +x rpc.py


about_win.py: about_win.in Makefile
	$(do_substitution) < $(srcdir)/about_win.in > about_win.py
	chmod +x about_win.py

status_win.py: status_win.in Makefile
	$(do_substitution) < $(srcdir)/status_win.in > status_win.py
	chmod +x status_win.py

prefs_win.py: prefs_win.in Makefile
	$(do_substitution) < $(srcdir)/prefs_win.in > prefs_win.py
	chmod +x prefs_win.py

applet_PYTHON = \
		     boinc_applet.py \
		     boinc_client.py \
		     rpc.py \
		     about_win.py \
		     status_win.py \
		     prefs_win.py

install-data-hook:
# TODO: find a better way of coping with this
#  move the .mate-panel-applet file to /usr/share/mate-panel/applets since it doesn't seem to work
# in /usr/local/share/mate-panel/applets
	mv $(appletsdir)/org.mate.panel.BoincMonitorApplet.mate-panel-applet /usr/share/mate-panel/applets/

CLEANFILES = $(applet_SCRIPTS)
EXTRA_DIST = $(srcdir)/boinc_applet.in \
	     $(srcdir)/ boinc_client.in \
	     $(srcdir)/rpc.in \
	     $(srcdir)/about_win.in \
	     status_win.in \
	     prefs_win.in \
	     $(image_DATA) \
	     $(srcdir)/org.mate.panel.applet.BoincMonitor.gschema.xml \
	     $(applets_in_files) \
	     $(service_in_files)

#boincappletdir = $(pythondir)/boincapplet
