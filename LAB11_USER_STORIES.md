# User Stories & Feature Tasks

#### LAB 11: Production Deployment w/ Heroku

Today's portion of the application involves storing book objects in a database. The client can make a request to the server for retrieval of all books, which will then be rendered as a list in the browser.

### Build and deploy a backend

1. As a developer, I want to seed my local development database with books so I have data to test my development application with.
    - Follow the instructions in `SERVER.md` from class lecture for setting up the db.
    - Specifics of this lab
        - Your `books` table should include a `id` as the primary key plus the following properties: `author`, `title`, `isbn`, `image_url`, and `description`
        - Use the provided JSON data to seed your data
1. As a developer, I want the client to have the ability to request all resources from the database through a RESTful endpoint.
    - Create a new endpoint at `GET /api/v1/books` which will retrieve an array of book objects from the database, limited to only the `book_id`, `title`, `author`, and `image_url`.
    - STRETCH GOAL: Create a new endpoint that will retrieve a single book based on its `id`.

1. As a developer, I want to deploy the backend API to a hosting service (like heroku) so that other developers may build their own frontend interfaces for this application.
    - Follow the instructions in `SERVER.md` for deploying to heroku

### Build and deploy a frontend

1. As a user, I want to display all of my books at once so that I can see everything in a single view.
    - Create a Book model in `scripts/models/book.js` following the guidelines in `CLIENT.md` from the
    class lecture
    - Create a View container in your index.html file (for example, a `<section>`) for the following content:
        - List of all available books by author and title.
        - Include on the page the count of books that are in the DB.
        - STRETCH GOAL: Create an About View for displaying content about you and your application.
1. As a user, I want my books to be rendered dynamically so that I can view all of the books in my list.
    - Follow instructions in `CLIENT.md` for creating `bookView.js`
    - STRETCH GOAL: Add a form for adding a book. See in class example for how to manage loading the
    book into the UI
1. As a user, I want a simple, clean looking UI so that my application is easy to navigate.
    - Style your site using a **mobile-only** approach. Use the provided wireframes as a general guideline for the _minimum styling requirements_, while adding your own personal taste and color palette.
    - Ensure the proper use of SMACCS principles.
    - STRETCH GOAL: Include icon fonts from a source such as Icomoon or FontAwesome for the social media icons you choose to include in the application.
1. As a user, I want to host my app on a reliable, scalable application hosting service (like gh-pages) so that I can access my mobile app when I'm on the go and share it with others.
    - Follow instructions in `CLIENT.md` from class lecture
