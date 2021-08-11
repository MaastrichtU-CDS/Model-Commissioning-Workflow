FROM registry.gitlab.com/um-cds/fair/tools/docker-graphdb:9.3.3

ADD ./graphdb_template/data/repositories /opt/graphdb/home/data/repositories

CMD ["-Dgraphdb.home=/opt/graphdb/home -Dorg.xml.sax.driver=com.sun.org.apache.xerces.internal.parsers.SAXParser -Djdk.xml.entityExpansionLimit=1000000 -Dgraphdb.workbench.cors.enable=true -Dgraphdb.workbench.cors.origin=*"]
