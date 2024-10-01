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
    // port can be any number, but usually 3000-something
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
Servers
-
- What servers are used for
  - In the past, servers were just used to serve files back to client's browsers.
  - Nowadays, they're used to quietly exchange large amounts of information back and forth between client and server behind the scenes.
    - Often this happens whilst the server is acting as an API.
    - This is probably done by sending JSON instead of text/HTML.
  - servers often respond in JSON; we can send JS objects in JSON
    ```
    app.get('/whats/up', (req, res) => {
      res.json({
        value: 'not much',
      });
    });
    ```
- how servers receive information
  - Servers can receive information through the URL. This is called the query data:
    ``` 
    app.get('/my/url', (req, res) => {
        const name = req.query.name;
        const age = req.query.age;   
        res.json({
            name: `Name is ${name}`,
            age: `Age is ${age}`,
        });
    });
    ```
  - Servers can also receiving information through the URL called params data
    ```
    app.get('/my/url/:name', (req, res) => {
      const name = req.params.name;
      res.json({
        name: `Name is ${name}`,
      });
    });
    ```
  - alternatively to `app.get`, we can use `app.post` where we send info through a body and not over the URL
    - we can't use this in the browser anymore
    - thus, we need API clients to talk to servers
- ports
  - usually 3000-something, but can be any number
  - we must run only one program per port, otherwise it'll cause error
- HTTP Crud Methods
  - get and post aren't the only type of requests we can send servers
  - the following table shows just some more
    ![image](https://github.com/user-attachments/assets/7f28decf-4774-45e4-88cf-3490bb95d40a)

API (Application Programming Interface)
-
- definition:
  - an interface exposed by a particular piece of software.
  - The most common usage of "API" is for Web APIs
    - a "contract" that a particular service provides.
    - the interface of the service acts as a black box and indicates that for particular endpoints
    - given particular input, the client can expect to receive particular output.
- RESTful API
  - an application program interface (API)
  - uses HTTP requests to GET, PUT, POST and DELETE data
  - These 4 methods describe the "nature" of different API requests.
  - most APIs nowadays are RESTful API
- HTTP requests made by code
  - We don't need an API client to send requests to servers, we can actually send requests via code
  - We can use an npm package sync-request-curl to allow us to programatically send RESTful API requests.
  - `npm install sync-request-curl`
  - We can send them to our previous server
    ```
    import request from 'sync-request-curl';

    const res = request(
        'GET',
        'http://localhost:3001/apple',
        {
            qs: {
                name: 'Hayden',
            }
        }
    );
    
    console.log(JSON.parse(String(res.getBody())));
    ```

Working with jest
-
```
import request from 'sync-request';

function get(route: string, qs: any) {
    const res = request(
        'GET',
        `http://localhost:3001${route}`,
        {
            qs: qs,
        }
    );
    return JSON.parse(String(res.getBody()));
}

describe('Test Apple', () => {
    test('If it returns a name string successfully', () => {
        const bodyObj = get('/apple', {
            name: 'Hayden',
        });
        expect(bodyObj.msg).toBe('Hi Hayden, thanks for sending apple!');
    });
});

describe('Test Orange', () => {
    test('If it returns a name string successfully', () => {
        const res = request(
            'POST',
            'http://localhost:3001/orange',
            {
                json: { name: 'Hayden' },
            }
        );
        const bodyObj = JSON.parse(String(res.getBody()));
        expect(bodyObj.msg).toBe('Hi Hayden, thanks for sending orange!');
    });
});
```
