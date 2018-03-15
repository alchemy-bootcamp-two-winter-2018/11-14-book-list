![CF]
===

## Lab 14 Submission Instructions

- Continue working in the same repositories from the previous class
- Check out a new branch for today's lab assignment, semantically something like `pagejs`.
- Complete your **Feature Tasks for the day**
- Create =Pull Request back to `grading` for each repo
- On Canvas, submit a link to your PR and a link to your deployed application on Heroku. **Make sure to include the following:**
  - A question within the context of today's lab assignment
  - An observation about the lab assignment, or related 'Ah-hah!' moment
  - How long you spent working on this assignment

## Resources

- [Google Books API Library](https://console.developers.google.com/apis/library)
- [REST Wiki](https://en.wikipedia.org/wiki/Representational_state_transfer)
- [A Beginner's Guide to HTTP and REST](https://code.tutsplus.com/tutorials/a-beginners-guide-to-http-and-rest--net-16340)
- [API Wiki](https://en.wikipedia.org/wiki/Application_programming_interface)
- [Superagent](https://visionmedia.github.io/superagent/)
- [Book Store Wireframe](./wireframes)

## Config

### Server

```sh
PORT=3000
ADMIN_PASSPHRASE=pirate
<COOL-THING>_API_KEY=<your-key-and-or-secret>
DATABASE_URL=postgres://localhost:5432/todos
CLIENT_URL=http://localhost:8080
#DATABASE_URL=
#PGSSLMODE=require
```

### Client

```html
    <!-- configuration script -->
    <script>
        const isProd = window.location.protocol === 'https:';
        const API_URL = isProd
            ? 'https://super-todos.herokuapp.com/api'
            : 'http://localhost:3000/api';
        
        // Option client side key
        //const COOL_API_KEY=123456

        window.module = {};
    </script>
```



```sh
book_app_week_3
├── project-client
│   ├── scripts
│   │   ├── models
│   │   │   └── thing1.js
│   │   │   └── thing2.js
│   │   ├── vendor
│   │   │   └── <local-scripts>.js
│   │   └── views
│   │       └── <thing1>-view.js
│   │       └── <thing2>-view.js
│   ├── app.js
│   └── styles
│   │   ├── base.css
│   │   ├── fonts
│   │   │   ├── icomoon.eot
│   │   │   ├── icomoon.svg
│   │   │   ├── icomoon.ttf
│   │   │   └── icomoon.woff
│   │   ├── icons.css
│   │   ├── layout.css
│   │   ├── modules.css
│   │   └── reset.css
│   ├── .eslintrc.json
│   ├── .gitignore
│   ├── index.html
│   ├── package-lock.json
│   ├── package.json
│   ├── README.md
└── book-list-server
    ├── load-db
    │   └── drop-tables.js
    │   └── create-tables.js
    │   └── seed-data.js
    │   └── books.json
    ├── .env
    ├── .env.example
    ├── .eslintrc.json
    ├── .gitignore
    ├── db-client.js
    ├── package-lock.json
    ├── package.json
    ├── README.md
    └── server.js
```

## User Stories & Feature Tasks

#### Overview

Today's refactor will implement the use of a 3rd party API, Google Books, which will give users the ability to search by author, title, or ISBN. If the user finds the book they want they will be able to add that book to their persistence layer (database).

*1. As a user, I want to access an external API so that I can incorporate additional information into my app, enhancing its functionality.*

- Login to [Google's API Developer Console](https://console.developers.google.com/) using your Google username and password.
- From the Credentials screen, create a new set of credentials for a web application, specifically giving yourself access to the Google Books API.
- This will provide you with an API Key which you can use for making API calls through your server. You will need to set this as an environment variable in your system and in your deployment application on Heroku (described below).

*2. As a user, I want to use the Google Books API so that I can search for books and add new books to my list.*

- Install and require the `superagent` package from NPM; validate that it's listed as a dependency in your `package.json`.
- Create a global variable reference to the `GOOGLE_API_KEY` that you set as an env variable for use in your new endpoints.
- Add an endpoint for a `GET` request to `/api/v1/books/find` which will proxy a `superagent` request from the client to the Google Books API and return a list of ten books that match the search query.
  - Map over the array of results to build an array of objects that match the `book` model in your database.
  - Send the newly constructed array of objects to your client in the response.
  - STRETCH GOAL: add a placeholder image for missing images
- Add an endpoint for a `PUT` request to `/api/v1/books/import/:isbn` which will proxy a `superagent` request from the client to the Google Books API, save to db.
  - Send the newly constructed book to your client in the response.

*3. As a user, I want a form and designated space for output so that I can search for books and see the results in a single view.*

- Add a new View to `index.html` with a class of `search-view` which contains a form for searching the Google Books API by author, title, or ISBN.
  - The form should contain three individual inputs.
  - Include a button to click when your want to trigger your search.
- Add a new View to `index.html` with a class of `search-view`, which contains a section and unordered list tag.
  - Your `<ul></ul>` should include an `id` attribute for targeting and insertion of dynamic content.

*4. As a user, I want my app to respond when I submit the form so that I can search the Google Books API and receive my results in my app.*

- Add a new view method to `book-view.js` called `bookView.initSearch` which will show the search form view and attach an event listener to the form.
- Add a new client-side route to your `app.js` file which will listen for `/books/search`, and:
  - Call `Book.find`
  - When complete, invoke `bookView.initSearch`.
- Add event listener trigger on `submit`, capturing the form data as an object literal. It will pass put the information into the query string and call `page('/books/search?<querystring>)`

- Add event listener will trigger on `click`, capturing the `data-bookid` value (ISBN) from the button; Call 
`Book.import` with the id and trigger the server importing the book. When finished, navigate to that detail book.


## Documentation

_Your README.md must include:_
```md
# Project Name

**Author**: Your Name Goes Here
**Version**: 1.1.0 (increment the patch/fix version number up if you make more commits past your first submission)

## Overview
<!-- Provide a high level overview of what this application is and why you are building it, beyond the fact that it's an assignment for a Code Fellows 301 class. (i.e. What's your problem domain?) -->

## Getting Started
<!-- What are the steps that a user must take in order to build this app on their own machine and get it running? -->

## Architecture
<!-- Provide a detailed description of the application design. What technologies (languages, libraries, etc) you're using, and any other relevant design information. -->

## Change Log
<!-- Use this are to document the iterative changes made to your application as each feature is successfully implemented. Use time stamps. Here's an examples:

01-01-2001 4:59pm - Application now has a fully-functional express server, with GET and POST routes for the book resource.
-->
```
