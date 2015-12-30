#
# IB TWS
#
# VERSION 0.1
#
# docker build --rm -t shabbychef/ibtws .
#
# c.f. http://fabiorehm.com/blog/2014/09/11/running-gui-apps-with-docker/
#
# docker run -it --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix:rw shabbychef/ibtws 
# docker run -it --rm --net=host -e DISPLAY=$DISPLAY -v $HOME/.Xauthority:/home/ibtrader/.Xauthority -v /tmp/.X11-unix:/tmp/.X11-unix:rw shabbychef/ibtws 
# xhost + 
# docker run -it --rm --net=host -e DISPLAY=$DISPLAY -v $HOME/.Xauthority:/home/ibtrader/.Xauthority -v /tmp/.X11-unix:/tmp/.X11-unix:rw --entrypoint=/bin/bash shabbychef/ibtws '-i'
#
# then 
#
# java -cp jts.jar:total.2013.jar -Xmx2048M -XX:MaxPermSize=512M jclient.LoginFrame .
#
# Created: 2015.10.25
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
 DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true apt-get install -y --no-install-recommends -q wget default-jre default-jdk; \
 apt-get clean ; \
 mkdir -p /opt/ibtws ; \
 wget --progress=dot:giga -O /opt/ibtws/ib.jar 'https://download2.interactivebrokers.com/download/unixmacosx_latest.jar' ; \
 cd /opt/ibtws ; \
 /usr/bin/jar xf ib.jar ; \
 chmod +x /opt/ibtws/IBJts )

ADD runtws.sh /opt/ibtws/IBJts/

# c.f. http://fabiorehm.com/blog/2014/09/11/running-gui-apps-with-docker/
# set these to your very own uid and gid, btw.

ENV dev_uid 1000
ENV dev_gid 1000
USER root

RUN (groupadd -g ${dev_gid} ibtrader; \
  useradd --home-dir /home/ibtrader --create-home --no-user-group --gid ${dev_gid} --uid ${dev_uid} --shell /bin/bash ibtrader ; \
	echo "ibtrader ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/ibtrader ; \
	chmod 0440 /etc/sudoers.d/ibtrader ; \
	chmod +x /opt/ibtws/IBJts/runtws.sh )

ENV HOME /home/ibtrader

#VOLUME ["/opt/ibtws"]
WORKDIR /opt/ibtws/IBJts

USER ibtrader

#####################################################
# entry and cmd# FOLDUP
# always use array syntax:

#ENTRYPOINT ["/usr/bin/java"]
#CMD ['-cp jts.jar:total.2013.jar -Xmx2048M -XX:MaxPermSize=512M jclient.LoginFrame .']

ENTRYPOINT ["/opt/ibtws/IBJts/runtws.sh"]
CMD ['-cp','jts.jar:total.2013.jar','-Xmx2048M','-XX:MaxPermSize=512M']
# UNFOLD

#for vim modeline: (do not edit)
# vim:nu:fdm=marker:fmr=FOLDUP,UNFOLD:cms=#%s:syn=Dockerfile:ft=Dockerfile:fo=croql
