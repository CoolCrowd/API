# Specification

## Endpoints

Method  | URI	 											    | Description                                                     |
-------:|:------------------------------------------------------|:----------------------------------------------------------------|
GET		| /														| Lists all endpoints, used for checking authentication.
PUT		| /experiments											| Creates a new experiment.
GET		| /experiments/**{id}**									| Lists all properties of a given experiment.
PATCH 	| /experiments/**{id}**									| Edits the given properties of an experiment.
DELETE  | /experiments/**{id}**									| Deletes an experiment and all results permanently.
POST 	| /experiments/**{id}**/start							| Starts an experiment which must already be configured.
POST 	| /experiments/**{id}**/stop							| Stops accepting new creative answers of to an experiment.
GET 	| /experiments/**{id}**/answers							| Lists all creative answers to an experiment.
GET 	| /experiments/**{id}**/answers/**{answer}**			| Shows a specific creative answer to an experiment.
GET 	| /experiments/**{id}**/answers/worker/**{worker}**		| Lists all creative answers of a given worker.
GET 	| /experiments/**{id}**/ratings							| Lists all ratings... TODO: Doesn't work, must be answer specific!
GET 	| /experiments/**{id}**/ratings/**{rating}**			| TODO: Doesn't work, must be answer specific!
GET 	| /experiments/**{id}**/ratings/worker/**{worker}**		| List all ratings of a given worker. Does that even make sense?

## Authentication

A user is identified by a username and password combination. These are checked on every request against a hash (probably slow).

> **Warning**: This is a critical area and wrong attempts should be rate limited. Additionally, access to the server should be restricted for improved security. This can be achieved by binding the server to localhost only and dropping or rejecting all traffic to port 80 / 443 (or any other port that is used to serve the API). These can then be access by using an SSH tunnel (port forwarding).

## Authorization

Once authenticated, a user is authorized for all endpoints, there is no further access restriction. Scoped access is out of scope and can be implemented later.
