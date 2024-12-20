# MERN-Book-Sarch

## Description Of Module
As a code writer I also want to be able to refactor code to make the code function to its full potential. In this module we were tasked in refactoring the starting code and add files to properly make the code work. The end point was to be able to have a full working Book Search website that a user can roam through

## User Story
```md
AS AN avid reader
I WANT to search for new books to read
SO THAT I can keep a list of books to purchase
```

## Reafctored Code 

### Back-End
* `auth.js`: Update the auth middleware function to work with the GraphQL API.

* `server.js`: Implement the Apollo Server and apply it to the Express server as middleware.

* `Schemas` directory:

  * `index.js`: Export your typeDefs and resolvers.

  * `resolvers.js`: Define the query and mutation functionality to work with the Mongoose models.
  *   **Hint**: Use the functionality in the `user-controller.js` as a guide.

  * `typeDefs.js`: Define the necessary `Query` and `Mutation` types:

    * `Query` type:

      * `me`: Which returns a `User` type.
  
    * `Mutation` type:

      * `login`: Accepts an email and password as parameters; returns an `Auth` type.

      * `addUser`: Accepts a username, email, and password as parameters; returns an `Auth` type.

      * `saveBook`: Accepts a book author's array, description, title, bookId, image, and link as parameters; returns a `User` type. (Look into creating what's known as an `input` type to handle all of these parameters!)

      * `removeBook`: Accepts a book's `bookId` as a parameter; returns a `User` type.

    * `User` type:

      * `_id`

      * `username`

      * `email`

      * `bookCount`

      * `savedBooks` (This will be an array of the `Book` type.)

    * `Book` type:

      * `bookId` (Not the `_id`, but the book's `id` value returned from Google's Book API.)

      * `authors` (An array of strings, as there may be more than one author.)

      * `description`

      * `title`

      * `image`

      * `link`

    * `Auth` type:

      * `token`

      * `user` (References the `User` type.)


### Front-End
You'll need to create the following front-end files:

* `queries.js`: This will hold the query `GET_ME`, which will execute the `me` query set up using Apollo Server.

* `mutations.js`:

  * `LOGIN_USER` will execute the `loginUser` mutation set up using Apollo Server.

  * `ADD_USER` will execute the `addUser` mutation.

  * `SAVE_BOOK` will execute the `saveBook` mutation.

  * `REMOVE_BOOK` will execute the `removeBook` mutation.

Additionally, you’ll need to complete the following tasks in each of these front-end files:

* `App.jsx`: Create an Apollo Provider to make every request work with the Apollo Server.
 
* `SearchBooks.jsx`:

  * Use the Apollo `useMutation()` Hook to execute the `SAVE_BOOK` mutation in the `handleSaveBook()` function instead of the `saveBook()` function imported from the `API` file.

  * Make sure you keep the logic for saving the book's ID to state in the `try...catch` block!

* `SavedBooks.jsx`:

  * Remove the `useEffect()` Hook that sets the state for `UserData`.

  * Instead, use the `useQuery()` Hook to execute the `GET_ME` query on load and save it to a variable named `userData`.

  * Use the `useMutation()` Hook to execute the `REMOVE_BOOK` mutation in the `handleDeleteBook()` function instead of the `deleteBook()` function that's imported from `API` file. (Make sure you keep the `removeBookId()` function in place!)

* `SignupForm.jsx`: Replace the `addUser()` functionality imported from the `API` file with the `ADD_USER` mutation functionality.

* `LoginForm.jsx`: Replace the `loginUser()` functionality imported from the `API` file with the `LOGIN_USER` mutation functionality.
