# Tempest Docker Image

Tempest Docker Image to take with you on an USB stick for those environments
where there isn't even the Iternet available. The image
is published both on Docker Hub and a portable image file is
published on GitHub Releases. The portable image file is 
created with `docker export`.

The following versions/tags are available:

|   Version   |  Docker Hub  |  Raw Image  |
|  ---------  |  ----------- | ----------  |
|  master     |  latest      | link        |


## Importing from Raw Image
Note: This is only required if you're using the Raw Image.
The following steps can be used to import the downloaded Raw Image .tar.gz image file:

    gzip -d tempest.tar.gz
    docker load -i tempest.tar
    docker tag $imgid samos123/tempest


## Running tempest

Create a tempest home directory which will be mounted by the container:

    mkdir tempest-home

Run the tempest container by mounting the created tempest home directory
and executing bash inside the container:

    docker run -v tempest-home:/thome -it samos123/tempest bash

Inside the tempst home initialize a new tempest configuration

    tempest init

You will now have etc/tempest.conf and etc/tempest.conf.sample inside
your tempest home. You should configure etc/tempest.conf to match your needs.
After you've done so can run tempest tests with:

    ostestr --regex '(?!.*\[.*\bslow\b.*\])(^tempest\.(api|scenario))'

For configuration please visit: [Tempest Configuration Documentation](http://docs.openstack.org/developer/tempest/configuration.html).