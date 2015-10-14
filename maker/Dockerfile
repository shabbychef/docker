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
# update ubuntu# FOLDUP
RUN (apt-get update -qq; \
	apt-get update --fix-missing)
# UNFOLD

#####################################################
# get package dependencies# FOLDUP
RUN (DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true \
	apt-get install -y --no-install-recommends -q make wget perl gzip ; \
	apt-get clean )
# UNFOLD

#####################################################
# entry and cmd# FOLDUP
USER root

# always use array syntax:
ENTRYPOINT ["/usr/bin/make"]

# ENTRYPOINT and CMD are better together:
CMD ["help"]
# UNFOLD

#for vim modeline: (do not edit)
# vim:nu:fdm=marker:fmr=FOLDUP,UNFOLD:cms=#%s:syn=Dockerfile:ft=Dockerfile:fo=croql
