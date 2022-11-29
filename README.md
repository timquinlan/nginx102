# nginx102
Example files for my talk at Ohio Linuxfest 2022.

This demo is self contained, no extra hardware or networking rules required. Requirements are:
* docker, docker-compose
* authorization to build containers
* authorization to forward host ports
* port 8080 open on the host (if you need to use a different port, change docker-compose.yml line 37 before you run "docker-compose up")

Clone this repo and use docker-compose to bring up the environment:

    git clone https://www.github.com/timquinlan/nginx102
    cd nginx102
    docker-compose up

Please review the slides and recording for full info (coming soon)

# Test cases

Open a 2nd terminal window to run the tests

Basic static page:

    curl http://localhost:8080/

Load balacing, notice which upstream server is responding by looking at docker-compose output:

    curl http://localhost:8080/lbs

Weighted Load balacing, enable weighted round robin and notice which upstream server is responding by looking at docker-compose output:

    curl http://localhost:8080/lbs

Load testing, notice difference when rate limits are in effect:

    ab -n 100 -c 10 http://localhost:8080/lbs

Persistance, enable ip_hash and notice which upstream server is responding by looking at docker-compose output:

    curl http://localhost:8080/lbs

Mirroring, check for mirrored requests in docker-compose output:

    curl http://localhost:8080/mirror

NJS content handler

    curl http://localhost:8080/njs

NJS body filter

    curl http://localhost:8080/njslower

# Container layout:
                                                              
                       clients ----> reverse_proxy 
                                           |
                                           |--------------> mirror
                                           |                  
                                  ------------------
                                |                    |
                            upstream1            upstream2



