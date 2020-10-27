# Zip Pal 
### A pen pal app (api)
#### [Hosted Live on Vercel](https://zippal.vercel.app/)

Description: [....]
 
---

#### Tech Stack & Dependencies
 ##### Node.js 
  * [Express](http://expressjs.com/)
   * [Cors](https://github.com/expressjs/cors#readme)
  * [Helmet](https://helmetjs.github.io/)
 ##### PostgreSQL 
  * [pg](https://github.com/brianc/node-postgres) 
  * [Knex](https://knexjs.org/)
  * [Postgrator](https://github.com/rickbergfalk/postgrator#readme)
 ##### _Testing_
  * [Chai](http://chaijs.com/)
  * [Mocha](https://mochajs.org/)
  * [Supertest](https://github.com/visionmedia/supertest#readme)
 ##### _Logging_
  * [Morgan](https://github.com/expressjs/morgan#readme)
  * [Winston](https://github.com/winstonjs/winston#readme)
 ##### _Authorization & Authentication_
  * [Bcrypt.js](https://github.com/dcodeIO/bcrypt.js#readme)
  * [JWT](https://github.com/auth0/node-jsonwebtoken#readme)
  * [xss](https://github.com/leizongmin/js-xss) 

---
## API Documentation
---

We use this codebase to access our datatables with user, conversation, and message data on the database _server hosted by heroku_.

We also use this codebase to confirm user credentials with the help of _JWT_ for authentication and _bcrypt_ to hash user passwords. 

With the exception of _registration and login_ all endpoints require _JWT_ .

### API Overview

```text
/api
.
├── /auth/token
│   └── POST
│       └── /
│   └── PUT
│       └── /
├── /users
│   └── GET
│       ├── /
│       └── /profile
│   └── POST
│       └── /
│   └── PATCH
│       └── /
├── /conversation
│   └── GET
│       ├── /
│       └── /find/:currentConversationIds
│   └── POST
│       └── /
│   └── PATCH
│       └── /:conversation_id/deactivate
├── /message
│   └── POST
│       └── /
│   └── PATCH
│       ├── /:message_id/save
│       ├── /:message_id/send
│       └── /:message_id/read
```
--- 

### [/api/auth] Auth Endpoints 

#### [/token] POST 
    Generating intial token upon successful login
```js
// req.body
{
  username: String,
  password: String
}

// res.body
{
  authToken: String
}
```
#### [/token] PUT 
    Refreshing token
```js
// req.header
Authorization: Bearer ${token}

// res.body
{
  authToken: ${token}
}
```
---

### [/api/user] User Endpoints 

#### [/] GET 
    Request User's data
```js
// req.header
Authorization: Bearer ${token}

// res.body
{
  username: String,
  display_name: String,
  active_conversations: String,
  bio: String,
  active_conversations: Number,
  location: String,
  fa_icon: String
}

```

#### [/profile] GET
    Request User's profile data, serialized with xss (for react-context) 
```js
// req.header
Authorization: Bearer ${token}

// res.body
{
  id: String,
  display_name: xss(String),
  username: xss(String),
  location: xss(String),
  bio: xss(String),
  active_conversations: Number,
  fa_icon: String
}
```

#### [/] POST

#### [/] PATCH
