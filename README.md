# LABS 11-14

## Overview
This week, you and your partner(s) will implement a basic full stack application for a book list which will render books from a PostgreSQL database.

## Submission Instructions

- You and your pair should create a GH Organization with two repos: 
    - your frontend code
    - your backend code
- Make sure you're both contributors to both repos.
- **It is essential that you create a `grading` branch in both repos before beginning any work.** You will not do any work on this branch, but it will be the target of your PR's for grading.
- Do your work on a feature branch, ie `display-books`. (The name does **not** need to be the same across repos.)
- Merge to master when ready to deploy.
- When you're done: create a Pull Request (PR) back to the `grading` branch of your frontend or server repo.
- **In Canvas**
    - submit a link to your deployed frontend repo's latest PR
    - submit a link to your deployed backend repo latest PR

## Resources
- [Book List Wireframes](./wireframes)
- [Book List Data](./data)
- [Heroku Node Deployment Tutorial](https://devcenter.heroku.com/categories/nodejs)
- [GH-Pages Deployment](https://pages.github.com/)
- [Express API Docs](http://expressjs.com/en/4x/api.html)

## Configuration

```sh
book_app_week_3
├── project-client
│   ├── scripts
│   │   ├── models
│   │   │   └── thing1.js
│   │   │   └── thing2.js
│   │   └── views
│   │       └── <thing1>-view.js
│   │       └── <thing2>-view.js
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
    ├── .eslintrc.json
    ├── .gitignore
    ├── db-client.js
    ├── package-lock.json
    ├── package.json
    ├── README.md
    └── server.js
```
