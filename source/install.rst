Install
=======

#. Install docker by using::
   
    sudo apt install docker.io

#. Once docker is installed, add the current user to the docker group by::

    sudo usermod -aG docker $USER

#. Logout and log back in for the changes to take effect.

#. Now, clone the repository using::

    git clone https://github.com/rbccps-iisc/ideam && cd ideam

#. Once inside the directory, install by using::

    ./install
