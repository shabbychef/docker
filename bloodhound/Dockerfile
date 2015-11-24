# TITLE
#
# VERSION 0.1
# 
# stolen from https://github.com/tonigi/docker_bloodhound/blob/master/Dockerfile
#
# docker build --rm -t shabbychef/bloodhound .
#
# SVN: $Id$
# Created: 2015.11.24
# Copyright: Steven E. Pav, 2015
# Author: Steven E. Pav
# Comments: Steven E. Pav

#####################################################
# preamble# FOLDUP
FROM ubuntu:14.04
MAINTAINER Steven E. Pav, shabbychef@gmail.com
USER root
# UNFOLD

#####################################################
# update ubuntu, install packages, and so on
RUN (apt-get update -qq; \
 apt-get update --fix-missing ; \
 DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true \
  apt-get install -y --no-install-recommends -q python python-pip python-virtualenv wget postgresql python-dev libpq-dev ; \
 apt-get clean -q -y ; \
 mkdir -p /tmp/build ; \
 cd /tmp/build && wget -O- http://www.carfab.com/apachesoftware/bloodhound/apache-bloodhound-0.8.tar.gz | tar -xvzf- ; \
 mkdir -p /opt/bloodhound; \
 virtualenv /opt/bloodhound/bhenv; \
 cd apache-bloodhound-0.8/installer; \
 . /opt/bloodhound/bhenv/bin/activate; \
 pip install -r requirements.txt; \
 python bloodhound_setup.py --environments_directory=/opt/bloodhound/environments --default-product-prefix=DEF -d sqlite --admin-user=admin --admin-password=admin 

# fsck, follow directions from here: 
# https://issues.apache.org/bloodhound/wiki/BloodhoundInstall
# bleah
RUN echo "#! /bin/bash\n\
#\n\
virtualenv /opt/bloodhound/bhenv/ \n\
. /opt/bloodhound/bhenv/bin/activate \n\
tracd --port=8080 /opt/bloodhound/environments/main\n" > /opt/bloodhound/runhound.sh

EXPOSE 8080

# always use array syntax:
ENTRYPOINT ["/bin/bash"]
# ENTRYPOINT and CMD are better together:
CMD ["/opt/bloodhound/runhound.sh"]

#for vim modeline: (do not edit)
# vim:nu:fdm=marker:fmr=FOLDUP,UNFOLD:cms=#%s:syn=Dockerfile:ft=Dockerfile:fo=croql
