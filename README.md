# nginx102

This demo is self contained, no extra hardware or networking rules required. Requirements are:
* docker, docker-compose
* authorization to build containers
* authorization to forward host ports
* port 8080 open on the host (if you need to use a different port, change docker-compose.yml line 37 before you run "docker-compose up")

Clone this repo and use docker-compose to bring up the environment:

    git clone https://www.github.com/timquinlan/nginx102
    cd nginx102
    docker-compose up

Open a 2nd terminal window and test with curl:

    curl http://localhost:8080/test

From the 2nd terminal window use the ab to do some load testing:

    ab -n 100 -c 10 http://localhost:8080/

Container layout:
                                                              
                       clients ----> reverse_proxy --------------> mirror
                                           |                  
                                  ------------------
                                |                    |
                            upstream1            upstream2
