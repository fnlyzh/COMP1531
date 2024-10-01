Introduction
-
- web servers are fundamental part of web-based full stack software
- definitions
  - `network`: a group of interconnected computers that can communicate
  - `internet`: a global infrastructure for networking computers around the entire world together
  - `world wide web`: a system of documents and resources linked together, accessible via URLs
- network protocols
  - communication over networks must have a certain "structure" so everyone can understand
  - humans do this all the time - waving, handshakes, clapping. Standard operation procedure that structures how we share info
  - different "structures" (`protocols`) are used for different types of communication
  - HTTP (Hypertext Transfer Protocol)
    - an example of one of the protocols
    - it is the protocol of the web
    - the primary protocol you use to access URLs in your web browser
    - Protocol for sending and receiving HTML documents (nowadays much more)
    - Web browsers are applications to request and receive HTTP.
- NodeJS Express Server
  - a very popular npm library exists to allow you to run your own HTTP server with NodeJS
  - it's called Express Server
  - code:
    ```
    // import the express library
    import express from 'express';

    // creates instance of a server and define the port to run on
    // a port is basically a road in and out of the computer's network
    // there are often 65,000-ish ports
    const app = express();
    const port = 3000;

    // quirk of express required to interpret data of requests
    app.use(express.text());

    // when URL/ is accessed, call this function
    app.get('/hello', (req, res) => {
        res.send('Hello!');
    });
    
    app.get('/whats/up', (req, res) => {
        res.send(JSON.stringify({
            value: 'not much',
        }));
    });

    // starts the server (on a particular port)
    // basically, runs an infinite loop so the program runs forever constantly,
    // waiting for new people to access it via a certain URL
    app.listen(port, () => {
        console.log(`Listening on port ${port}`);
    });
    ```
