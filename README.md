# Elm Todos Project

As part of a team effort to learn Elm and implement it into our stack, we're working on a todo-list application for training. To help with this, I have created this project, which includes an API that everyone can use for storing their wishlist data.

## Terms

To avoid any confusion, here are a list of the terms that I'll use as parts of the todo list.

- **_List / Todolist_** - _A named list of items. Lists also have a name and a darkmode._
- **_Item_** - _A singular item that belongs to a list. An item has a task, description, and a complete flag._
- **_Task_** - _The action to be done (to do) that belongs to a single item id. For example, for a todo item, the given task might be to "take the dog out."_
- **_Description_** - _A more detailed explanation of a task belonging to a single itemId._
- **_Complete_** - _A flag that indicated whether or not the todo list item has been marked as completed._

## How To Use The API

As of 02/05/2021, the API is running on our `playground05` box. Otherwise, scroll down to the bottom to read about setting up a container running the API.

##### `/api/list/:listOwner` | `POST`

You'll need to run this first in order to create a todo list with an owner.

    Request Body: null
    Response Body: {}

##### `/api/list/:listOwner` | `GET`

Once a list has been created, you can obtain its ID and other details from this endpoint. You'll need to ID for all other actions relating to lists and their items.

    Request Body: null
    Response Body:
        {
            "_id": string,
            "owner": string,
            "isDark": bool
        }


##### `/api/list/darkmode/:listId` | `PUT`

This is an absolute necessity if you want your app to be worth anything. If you don't have dark mode why are you even a web developer?

    Request Body:
        {
            "isDark": true
        }
    Response Body:
        {
            "_id": string,
            "owner": string,
            "isDark": bool
        }


##### `/api/items/:listId` | `GET`

After obtaining your listId from `/api/list/:listOwner` you can use this endpoint to get all of the items on the list.

    Request Body: null
    Response Body:
        [
            {
                "_id": string,
                "task": string,
                "description": string
                "complete": boolean,
                "listId": string,
                "__v": int
            },
            ...
        ]


##### `/api/item/:listId` | `POST`

To add an item to the given `listId`, use this endpoint with a body containing the todo task and description.

    Request Body:
            {
                "task": string,
                "description": string -- optional
            },
    Response Body: null


##### `/api/item/:itemId` | `PUT`

With a given `itemId`, you can update the task or description using this endpoint given a `task` and `description` in the request body. Alternatively, you can give it a `complete` flag in the request body to change that.

Updating the Task and Description:

    Request Body:
            {
                "task": string,
                "description": string -- optional
            },
    Response Body: null

Updating the Completed status

    Request Body:
            {
                "complete": boolean
            },
    Response Body: null


##### `/api/item/:itemId` | `DELETE`

This deleted the item associated with the given `itemId`.

    Request Body: null
    Response Body: null

## Setup

Follow these steps to setup a new instance of the API server:
--- 1. Clone the branch `git clone https://github.com/abshierjoel/elm-todo.git`
--- 2. Build the Docker container: `docker build -t abshierjoel/todos .`
--- 3. Run the Docker container with internal port 8080: `docker run -d abshierjoel/todos -p [PORT]:8080`

_Dockerization of the Elm App isn't done yet. It may be accessible from the container, just unstable._
