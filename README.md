# Wanbli

An small framework for creating simple JSON REST applications for the Dictu programming language.

Wanbli aims to be as simple as possible. Responses are assumed to be JSON but if it's just a single string returned, the string is returned. Any other datatype gets JSON encoded.

## Getting Started

Import the framework:

```js
from "wanbli.du" import Wanbli;
```

Initialize the framework by calling the `Wanbli` function. It takes the listening address and port.

```js
const wanbli = Wanbli("0.0.0.0", 8080);
```

## Setup a Controller

Wanbli uses classes, methods, and annotations to drive primary functionality. The example below shows how a class can be configure to handle requests.

```js
@Controller("/api/v1/widget")
class Widget {
    init() {
        this.dataStore = {};
    }

    @Post
    new(request) {
        this.dataStore = this.dataStore.merge(request.body);
        return [this.dataStore];
    }

    @Put
    update(request) {
        this.dataStore = this.dataStore.merge(request.body);
        return [this.dataStore];
    }

    @Get
    retrieve(request) {
        if (request.query.exists("id")) {
            const key = request.query.get("id");
            return {
                key: this.dataStore.get(key)
            };
        }
        
        return {};
    }

    @Get
    @Path("/all")
    all(request) {
        return this.dataStore;
    }
}
```

## Middleware

Wanbli comes with a number of middlewares and allows users to easily create custom middlwares.

## Contributions

* File Issue with details of the problem, feature request, etc.
* Submit a pull request and include details of what problem or feature the code is solving or implementing.
