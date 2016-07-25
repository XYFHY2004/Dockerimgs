FROM python:2.7

MAINTAINER xyfhy

# Install Deps
RUN apt-get update -y -qq && \
    apt-get install -y python2.7 python2.7-dev qt4-default libssl-dev libevent-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install SIP
RUN mkdir -p /opt/sip && \
    cd /opt/sip && \
    curl -L -o sip.tar.gz http://sourceforge.net/projects/pyqt/files/sip/sip-4.17/sip-4.17.tar.gz && \
    tar -xf sip.tar.gz && \
    cd /opt/sip/sip-* && \
    python configure.py && \
    make && \
    make install && \
    cd /opt && \
    rm -rf /opt/sip

# Install PyQt4
RUN mkdir -p /opt/pyqt && \
    cd /opt/pyqt && \
    curl -L -o pyqt4.tar.gz http://sourceforge.net/projects/pyqt/files/PyQt4/PyQt-4.11.4/PyQt-x11-gpl-4.11.4.tar.gz && \
    tar -xf pyqt4.tar.gz && \
    cd /opt/pyqt/PyQt* && \
    python configure.py -c --confirm-license --no-designer-plugin -e QtCore -e QtGui -e QtWidgets && \
    make && \
    make install && \
    cd /opt && \
    rm -rf /opt/pyqt

#Install xvfb
#RUN apt-get install xvfb


# Check & Go to Workspace
RUN python -c "import PyQt4" && \
    mkdir -p /opt/workspace

#Copy requirements to workspace
ADD . /opt/workspace
WORKDIR /opt/workspace

# Install python lib
RUN pip install --upgrade pip && \
    pip install -r requirements.txt


