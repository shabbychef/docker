#
# GNU Make + useful CLI utils around make.
#
# VERSION 0.1
#
# docker build --rm -t shabbychef/maker .
#
# Created: 2015.10.14
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
 DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true apt-get install -y --no-install-recommends -q make wget perl gzip unzip; \
 apt-get clean )

VOLUME ["/opt/make"]
WORKDIR /opt/make

#####################################################
# entry and cmd# FOLDUP
# always use array syntax:

ENTRYPOINT ["/usr/bin/make"]

# ENTRYPOINT and CMD are better together:
CMD ["help"]
# UNFOLD

#for vim modeline: (do not edit)
# vim:nu:fdm=marker:fmr=FOLDUP,UNFOLD:cms=#%s:syn=Dockerfile:ft=Dockerfile:fo=croql
