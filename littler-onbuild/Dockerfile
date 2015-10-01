#
# littler + onbuild directives.
#
# the ONBUILD directives first look for
# ./apt_packages.txt, with a package on each line,
# then attempts to apt-get install them.
#
# then looks for ./r_packages.txt, with an R package on each line,
# then attempts to rinstall2 them.
#
# VERSION 0.1
#
# docker build --rm -t shabbychef/littler-onbuild .
#
# Created: 2015.10.01
# Copyright: Steven E. Pav, 2015
# Author: Steven E. Pav
# Comments: Steven E. Pav

#####################################################
# preamble# FOLDUP
FROM shabbychef/littler 
MAINTAINER Steven E. Pav, shabbychef@gmail.com
USER root
# UNFOLD

#####################################################
# onbuild magic# FOLDUP
ONBUILD ADD ./apt_packages.txt /tmp/apt_packages.txt
ONBUILD RUN DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true \
	apt-get install -y --no-install-recommends -q $(cat /tmp/apt_packages.txt);

ONBUILD ADD ./r_packages.txt /tmp/r_packages.txt
ONBUILD RUN /usr/local/bin/install.r $(cat /tmp/r_packages.txt)
# UNFOLD

# everything else inherits from littler

#for vim modeline: (do not edit)
# vim:nu:fdm=marker:fmr=FOLDUP,UNFOLD:cms=#%s:syn=Dockerfile:ft=Dockerfile:fo=croql
