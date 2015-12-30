# TITLE
#
# VERSION 0.1
# 
# stolen from https://github.com/jmmills/docker-trac/blob/master/Dockerfile
#
# docker build --rm -t shabbychef/trac .
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
RUN (rm -rf /var/lib/apt/lists/* ; \
 apt-get clean -y ; \
 apt-get update -y -qq; \
 apt-get update --fix-missing ; \
 DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true \
  apt-get install -y --no-install-recommends -q \
  pwgen git-core trac trac-git trac-accountmanager trac-customfieldadmin \
  trac-authopenid trac-wikiprint trac-wysiwyg trac-announcer trac-graphviz \
  trac-bitten trac-roadmap python-flup ; \
 apt-get clean -q -y ; \
 mkdir -p /opt/trac /tmp/build )

ADD https://raw.githubusercontent.com/jmmills/docker-trac/master/set_trac_user_password.py /usr/local/bin/
ADD https://raw.githubusercontent.com/jmmills/docker-trac/master/setup_trac_config.sh /opt/trac/
ADD https://raw.githubusercontent.com/jmmills/docker-trac/master/setup_trac.sh /opt/trac/
ADD https://raw.githubusercontent.com/jmmills/docker-trac/master/run.sh /opt/trac/

ADD https://raw.githubusercontent.com/jmmills/docker-trac/master/trac_logo.png /var/www/

RUN ( chmod 755 /usr/local/bin/set_trac_user_password.py ; \
	chmod 700 /opt/trac/*.sh )

EXPOSE 80

# always use array syntax:
ENTRYPOINT ["/opt/trac/run.sh"]
# ENTRYPOINT and CMD are better together:
CMD []

#for vim modeline: (do not edit)
# vim:nu:fdm=marker:fmr=FOLDUP,UNFOLD:cms=#%s:syn=Dockerfile:ft=Dockerfile:fo=croql
