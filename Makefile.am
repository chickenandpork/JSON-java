nodist_java_JAVA = CDL.java Cookie.java CookieList.java HTTP.java HTTPTokener.java JSONArray.java JSONException.java JSONML.java JSONObject.java JSONString.java JSONStringer.java JSONTokener.java JSONWriter.java Kim.java Property.java XML.java XMLTokener.java
nodist_java_JAVA += zip/BitInputStream.java zip/BitOutputStream.java zip/BitReader.java zip/BitWriter.java zip/Huff.java zip/JSONzip.java zip/Keep.java zip/MapKeep.java zip/None.java zip/PostMortem.java zip/TrieKeep.java zip/Unzipper.java zip/Zipper.java
nodist_java_DATA = $(subdir).jar
javadir = $(pkgdir)

EXTRA_DIST = $(nodist_java_JAVA)
CONFIG_CLEAN_FILES = $(subdir).jar

JAVAROOT = bld
BUILT_SOURCES = javaroot.stamp

javaroot.stamp: $(nodist_java_JAVA)
	mkdir -p $(JAVAROOT) && touch $@

AM_JAVACFLAGS= @JAVAC_FLAGS@ -cp $(JAVAROOT)

$(subdir).jar: classjava.stamp
	awk -v BUILDTOP="bld" '/^package / {gsub (";$$",""); gsub ("\\.","/",$$2); SUBS[$$2]=$$2 } END { FIRST=0; for (n in SUBS) { if (0 == FIRST++) printf "jar cvf $@"; printf " -C %s %s",BUILDTOP,n }; printf "\n"; }' $(nodist_java_JAVA) | $(SHELL)
	touch $(notdir $(subdir)).class

clean-local:
	CLASSES=`for i in $(nodist_java_JAVA); do awk -v FILE="$$i" '/^package / {gsub (";$$",""); gsub (".java",".class",FILE); gsub ("\\\\.","/",$$2); printf "%s/%s\n",$$2,FILE}' $(srcdir)/$$i; done`; (cd $(top_builddir)/ && rm -f $$CLASSES)
	
