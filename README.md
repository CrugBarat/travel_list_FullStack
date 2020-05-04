# Travel List

A Travel List app, which uses a HTTP RESTful API as a data source:

**Programming Language**: JavaScript

**Front-end Web Framework**: Vue

**Back-end Web Framework**: Express

**Db**: MongoDb

**API Client**: Insomnia

**Middleware**: Body Parser

**Markup/Styling**: HTML5/CSS3

The app can add a chosen country to a travel list. The countries and flags are sourced from a REST API. The list is stored in a MongoDb database. The app uses RESTful routes to add and update countries in the Db.  

This exercise was tasked to me by CodeClan, Glasgow where I studied towards a PDA Level 8 in Professional Software Development. The exercise brief can be found below.

---

# Brief

You have been given a travel app which allows users to add countries to a favourites list. Currently the countries in the bucket list are not persisted. When the server restarts the data is lost! You have been asked to save users bucket list countries to a database and allow the users to mark countries as being visited.

**MVP**

- Code the POST and PUT routes in the createRouter file in the server. Test these using insomnia
- Modify the client code to save the country name, flag and visited (false initially) to the database when user adds a country to the Bucket list

**Extensions**

- Add a way for the user to update the country as being visited
- Only show the Visit button if country has not been visited
- Highlight that a country has been visited in the list in some way

---

# Setup

- Download/Clone files

- If required, download and install [Node](https://nodejs.org/en/)

- In each of the client and server directories, in Terminal:

```
npm install
```

- In client directory, in Terminal:

```
npm run serve
```

- In server directory, in Terminal:

```
npm run server:dev
```

- Click the link below to open project in browser

[LocalHost](http://localhost:8080/): http://localhost:8080/
