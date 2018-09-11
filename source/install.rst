Install
=======

Prerequisites
^^^^^^^^^^^^^

#. Install Docker ::

    sudo apt-get install docker

#. Add permission to user ::

    sudo usermod -a -G docker $USER

#. Add DNS to the file /etc/docker/daemon.json. If it does not exist, create one ::

    {"dns": ["8.8.8.8", "8.8.4.4"]}

#. Add DNS in /etc/default/docker file ::

    DOCKER_OPTS="--dns 8.8.8.8 --dns 8.8.4.4"

#. Restart Docker ::

    service docker restart

#. Install python ::

    sudo apt-get install python

#. Install python-pip and pass-lib ::
    sudo apt install python-pip
    pip install passlib

#. Install git ::

    sudo apt-get install git


CDX Installation
^^^^^^^^^^^^^^^^

#. Clone CDX git repo ::

    git clone https://github.com/rbccps-iisc/ideam.git

CDX installation has a configuration file (ideam.conf), which details about the ports used by different services and also allows the user to configure the passwords that needs to be used for certain services during installation. By default, the password field in the config file is set to ?, which indicates the system to generate password during run-time ::

    cd ideam/
    vim ideam.conf
    make necessary changes

#. Install CDX ::

    cd ideam/
    ./install

