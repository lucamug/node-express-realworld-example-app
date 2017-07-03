# ![Node/Express/Mongoose Example App](https://cdn.rawgit.com/gothinkster/node-express-realworld-example-app/df9b9991/project-logo.png)

> ### Example Node (Express + Mongoose) codebase containing real world examples (CRUD, auth, advanced patterns, etc) that adheres to the [RealWorld](https://github.com/gothinkster/realworld-example-apps) API spec.

<a href="https://thinkster.io/tutorials/node-json-api" target="_blank"><img width="454" src="https://raw.githubusercontent.com/gothinkster/realworld/master/media/learn-btn-hr.png" /></a>

Ported  to glitch from [gothinkster/node-express-realworld-example-app](https://github.com/gothinkster/node-express-realworld-example-app)

# Getting started

"Remix" this project by clicking in the top left menu.

Glitch automatically starts running this code as soon as you open it!

The only piece you need to provide is a MongoDB instance, but don't worry! 

You can easily create a free instance and database over at [mLab](https://mlab.com) 

Once you do that, edit the `.env` file, and drop in the 
MongoDB URI you created at mLab. It should look something like this:

```
# Environment Config
# note: .env is a shell file so there can't be spaces around =
# reference these in your code with process.env.SECRET

# store your secrets and config variables in here
# only invited collaborators will be able to see your .env values
NODE_ENV=production
SECRET=c494aab3-af14-4797-86cc-78a2307e999f
MADE_WITH=💖

# Quickly spin up a free hosted MongoDB instance at https://mlab.com
# And set "MONGODB_URI" on the following line
MONGODB_URI=mongodb://mongouser:mongopass@ds092481.mlab.com:31415/databasename
```

Check the logs to make sure everything worked correctly, and you have a working
API to test your changes available here:

  **https://<your-glitch-name>.glitch.me/api** 

# Code Overview

## Dependencies

- [expressjs](https://github.com/expressjs/express) - The server for handling and routing HTTP requests
- [express-jwt](https://github.com/auth0/express-jwt) - Middleware for validating JWTs for authentication
- [jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) - For generating JWTs used by authentication
- [mongoose](https://github.com/Automattic/mongoose) - For modeling and mapping MongoDB data to javascript 
- [mongoose-unique-validator](https://github.com/blakehaswell/mongoose-unique-validator) - For handling unique validation errors in Mongoose. Mongoose only handles validation at the document level, so a unique index across a collection will throw an excpetion at the driver level. The `mongoose-unique-validator` plugin helps us by formatting the error like a normal mongoose `ValidationError`.
- [passport](https://github.com/jaredhanson/passport) - For handling user authentication
- [slug](https://github.com/dodo/node-slug) - For encoding titles into a URL-friendly format

## Application Structure

- `app.js` - The entry point to our application. This file defines our express server and connects it to MongoDB using mongoose. It also requires the routes and models we'll be using in the application.
- `config/` - This folder contains configuration for passport as well as a central location for configuration/environment variables.
- `routes/` - This folder contains the route definitions for our API. They contain
- `models/` - This folder contains the schema definitions for our Mongoose models.

## Error Handling

In `routes/api/index.js`, we define a error-handling middleware for handling Mongoose's `ValidationError`. This middleware will respond with a 422 status code and format the response to have [error messages the clients can understand](https://github.com/gothinkster/realworld/blob/master/API.md#errors-and-status-codes)

## Authentication

Requests are authenticated using the `Authorization` header with a valid JWT. We define two express middlewares in `routes/auth.js` that can be used to authenticate requests. The `required` middleware configures the `express-jwt` middleware using our application's secret and will return a 401 status code if the request cannot be authenticated. The payload of the JWT can then be accessed from `req.payload` in the endpoint. The `optional` middleware configures the `express-jwt` in the same way as `required`, but will *not* return a 401 status code if the request cannot be authenticated.


<br />

[![Brought to you by Thinkster](https://raw.githubusercontent.com/gothinkster/realworld/master/media/end.png)](https://thinkster.io)
