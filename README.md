# docs

Documentation on the system structure and how everything works.

## General structure

Key components of the general structure are the *gamemaster*  and *boardservice*. Both of these components are microservices able to scale up, which means that each component sits behind a specific API gateway (denoted with a domain and a dotted line).

![l12u_structure](./.github/assets/l12u_structure.png)

The client (with their browser) now sends a request to the gamemaster on entering the page to fetch all information on *what boards are available?*, *what games are running?* and specifically on *how to reach each boardservice?*.
The gamemaster itself stores the information on each board and game in a seperate Redis database, so that the data survives a restart of a microservice.

If the client now wants to create a game or join a running game, they send a request to the boardservice they are interested in and if successful, they create a websocket connection with it, to make the game experience smooth and to allow multiplayer interactions.