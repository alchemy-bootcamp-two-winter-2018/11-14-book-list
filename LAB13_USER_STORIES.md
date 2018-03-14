13: Middleware
===

## Lab 13 Submission Instructions

- Continue working in the same repositories from the previous class
- Check out a new branch for today's lab assignment, semantically something like `pagejs`.
- Complete your **Feature Tasks for the day**
- Create =Pull Request back to `grading` for each repo
- On Canvas, submit a link to your PR and a link to your deployed application on Heroku. **Make sure to include the following:**
    - A question within the context of today's lab assignment
    - An observation about the lab assignment, or related 'Ah-hah!' moment
    - How long you spent working on this assignment


## Config

### Server

```sh
PORT=3000
ADMIN_PASSPHRASE=pirate
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

Today will add the functionality of removing and updating records from your database through the use of middleware. It will also include the additional feature of an administrator interface, which will only allow modifications to the database when the user is 'authenticated'.

*1. As a user, I want to have buttons in my detail view so that I can easily update or delete a single book with the click of a button.*

- Add two new buttons to appear alongside any book rendered in the detail view: a button for Updating and a button for Deleting.
- Add a new form View for updating an existing record in the database. This should look identical to your Create form, with the exception of any ID and class attributes that identify this form as an update view (as opposed to a create view).
- STRETCH GOAL: Use the existing form and create a new view

*2. As a user, I want to be able to delete a single book so that my list is always current.*

- Add an endpoint for a `DELETE` request to `/api/v1/books/:id`.
  - This should use the provided ID in the URL to delete the given record from the database.
  - The ID provided should only be a number. The handler for this route should not be triggered with a non-numeric value for the ID.
- Add a new method called `Book.delete` to your `Book` model for deletion. This method will interact with your API through the use of AJAX requests.

*3. As a user, I want to be able to update a single book so that my list is accurate and can be modified as needed.*

- Add an endpoint for a `PUT` request to `/api/v1/books/:id`.
  - This should use the provided ID in the URL to update the given record in the database.
  - The ID provided should only be a number. The handler for this route should not be triggered with a non-numeric value for the ID.
  - After a successful update, a response should be sent back to the user in the form of a 200 status code along with the updated object.
    - HINT: use `RETURNING`
- Add a new method called `Book.update` to your `Book` model for updating a single book. This method will interact with your API through the use of AJAX requests.
- Add a new method to your `bookView` object called `initUpdate`.
  - Set up an event listener for form submission to capture the current form state and pass it to the `Book.update` method.
- Add functionality in your `routes.js` file for updating a book.
  - Create a new route in your PageJS route definitions, which will handle callbacks at the `/books/:book_id/update` route.
  - Call the `Book.fetchOne` method and place the fetched Book on `Book.current`. This should return a promise. In the route handler, 
  call the init for the view in the `.then`
- Redeploy your application.

*4. As a user, I want to have admin-only routes so that I can control access to updating and deleting books from my app.*

- Create a User model that will handle the call to the server to verify the admin passphrase login (refer to in-class work)
- Create a new file named `loginView.js` which includes the following:
  - Enclose your code in an IFFE.
  - Define a global variable called `loginView` and assign an empty object literal as its value.
  - Define a method on `loginView` called `init` which shows the admin view and has a form field for entering the passphrase.
- Create a new route in your PageJS route definitions, which will handle the callbacks at the `/login` route.
  - This should handle the view for your passphrase form.
- Redeploy your application.

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

## Credits and Collaborations
<!-- Give credit (and a link) to other people or resources that helped you build this application. -->

-->
```