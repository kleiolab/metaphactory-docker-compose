
HOW TO START "metaphactory for GraphDB"


Prerequisites:

* Have a GraphDB license in /metaphactory-graphdb/configs/license.file
* Reference the license file in the .env file as value of the env-variable: $GRAPHDB_LICENSE_FILE


1.) Create the network
run the command:

docker network create nginx_proxy_network


2.) Start containers
go to folder ´metaphactory-graphdb/service-template´
run the command

docker-compose up -d


3.) Start using it

* metaphactory: Navigate your browser to http://my-depoloyment-1.localhost:10214/
** Login with admin:admin
* graphDB:  Navigate your browser to http://my-depoloyment-1.localhost:7200/

Enjoy ;-)

