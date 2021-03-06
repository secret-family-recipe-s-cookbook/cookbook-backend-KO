# Secret Family Recipes Cookbook

### PITCH

[![Build Status](https://travis-ci.org/secret-family-recipe-s-cookbook/cookbook-backend-KO.svg?branch=master)](https://travis-ci.org/secret-family-recipe-s-cookbook/cookbook-backend-KO)

Anyone can go out and buy a cookbook these days, but I want a place to store all my secret family recipes, handed down from generation to generation.

API request url : https://lambda-cook-book.herokuapp.com/

### API Specifications. Request And Response Examples

#### Auth User Registration

_Post_ api/auth/register

_Request_ body

```
    {
        "firstname": "jacksin",
        "lastname": "ogbonna",
        "username": "laboo",
        "email": "lackson@yahoo.com",
        "password": "12345",
        "confirmPassword": "12345"
    }
```

_Response_ body

This response is sent if request is successful

```
    {
        "message": "user created successfully",
        "user": {
            "id": 6,
            "firstname": "jacksin",
            "lastname": "ogbonna",
            "username": "laboo",
            "email": "lackson@yahoo.com"
        }
    }
```

If user data input is not complete or does not pass the validations, an array of error messages is returned.
username and email has to be unique.

_Request_ body

```
    {
        "firstname": "",
        "lastname": "",
        "username": "",
        "email": "",
        "password": "5",
        "confirmPassword": ""
    }
```

_Response_ body

```
    {
        "status": 400,
        "error": [
            "firstname must contain only alphabets",
            "firstname must have atleast 2 characters",
            "firstname cannot contain whitespaces",
            "lastname must contain only alphabets",
            "lastname must have atleast 2 characters",
            "lastname cannot contain whitespaces",
            "lastname must have atleast 2 characters",
            "lastname cannot contain whitespaces",
            "Please input a valid email address",
            "password must have atleast 5 characters",
            "password cannot contain whitespaces",
            "Password confirmation does not match password"
            ]
    }
```

#### Auth User Login

_Post_ api/auth/login

The usernameoremail object key can take either the username or email as an input.

_Request_ body

```
    {
        "usernameoremail": "laboo",
        "password": "12345"
    }
```

_Response_ body

This response is sent if request is successful

```
    {
        "message": "Welcome laboo",
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NiwidXNlcm5hbWUiOiJsYWJvbyIsImVtYWlsIjoibGFja3NvbkB5YWhvby5jb20iLCJpYXQiOjE1NjQ0ODQzNjMsImV4cCI6MTU2NDU3MDc2M30.gVRACnwYjHAL_ke3gBoIXkzjAem2zNIICPNaAJNsWWI"
    }
```

If the request is not successful a _400_ status and error message is returned

```
    {
        "message": "Invalid details, please input a username or email"
    }
```

#### Add Recipe

_Post_ api/recipes

tittle, ingredients, directions and description cannot be left empty

_Request_ body

```
        {

            "recipe_image": " ",
            "title": "cream carroy salado",
            "description": "cream pie salad is a pie made with salad and garnished with cream. hmm so delicicious",
            "ingredients": "lettuces, cream, flour,sugar, carrot",
            "directions": "grate lettuce and carrot, pour cream in a pot and steam",
            "Notes": " ",
            "source": " ",
            "bio": " ",
            "source_image": " ",
        }
```

_Response_ body

This response is sent if request is successful

```
    {
    "message": "recipe created successfully",
    "recipe": [
        {
            "id": 2,
            "recipe_image": null,
            "title": "cream carroy salado",
            "description": "cream pie salad is a pie made with salad and garnished with cream. hmm so delicicious",
            "ingredients": "lettuces, cream, flour,sugar, carrot",
            "directions": "grate lettuce and carrot, pour cream in a pot and steam",
            "Notes": null,
            "source": null,
            "bio": null,
            "source_image": null,
            "user_id": 1
        }
    ]
}
```

If the request is not successful a _400_ status and error message is returned

#### Get all Recipes

_GET_ api/recipes

Returns all the recipes that have been created. user has to be logged in to access this route

_Response_ body

This response is sent if request is successful

```
   {
    "data": [
        {
            "id": 1,
            "recipe_image": null,
            "title": "cream carroy salado",
            "description": "cream pie salad is a pie made with salad and garnished with cream. hmm so delicicious",
            "ingredients": "lettuces, cream, flour,sugar, carrot",
            "directions": "grate lettuce and carrot, pour cream in a pot and steam",
            "Notes": null,
            "source": null,
            "bio": null,
            "source_image": null,
            "user_id": 1
        }
    ]
}
```

It returns a 404 if no recipe has been created

#### Get a Recipes

_GET_ api/recipes/:id

Returns the recipe with the given id. user has to be logged in to access this route

_Response_ body

This response is sent if request is successful

```
   {
    "data":
        {
            "id": 1,
            "recipe_image": null,
            "title": "cream carroy salado",
            "description": "cream pie salad is a pie made with salad and garnished with cream. hmm so delicicious",
            "ingredients": "lettuces, cream, flour,sugar, carrot",
            "directions": "grate lettuce and carrot, pour cream in a pot and steam",
            "notes": null,
            "source": null,
            "bio": null,
            "source_image": null,
            "user_id": 1
        }
}
```

It returns a 404 if the recipe does not exist.

#### Delete a Recipe

_DELETE_ api/recipes/:id

Deletes the recipe with the given id. user has to be logged in to access this route. the user has to be the one who created the recipe

_Response_ body

This response is sent if request is successful

```
   {
    message: 'recipe has been deleted',
    "data": 1
   }
```

It returns a 404 if the recipe does not exist.

It returns a _403_ if the user trying to delete the route did not create the route

```

{ error:
    'You cannot delete this recipe'
 }

```

_UPDATE_ api/recipes/:id

Deletes the recipe with the given id. user has to be logged in to access this route. the user has to be the one who created the recipe

_Request_ body

This response is sent if request is successful

```
   {
            "recipe_image": " ",
            "title": "cream carroy gelato",
            "description": "cream pie salad is a pie made with salad and garnished with cream. hmm so delicicious",
            "ingredients": "lettuces, cream, flour,sugar, carrot",
            "directions": "grate lettuce and carrot, pour cream in a pot and steam",
            "Notes": " ",
            "source": " ",
            "bio": " ",
            "source_image": "image-two",
        }
```

_Response_ body

This response is sent if request is successful

```
   {
            "recipe_image": " ",
            "title": "cream carroy gelato",
            "description": "cream pie salad is a pie made with salad and garnished with cream. hmm so delicicious",
            "ingredients": "lettuces, cream, flour,sugar, carrot",
            "directions": "grate lettuce and carrot, pour cream in a pot and steam",
            "Notes": " ",
            "source": " ",
            "bio": " ",
            "source_image": "image-two",
        }
```

It returns a 404 if the recipe does not exist.

It returns a _403_ if the user trying to edit the recipe did not create the route

```

{ error: 'You cannot edit this recipe' }

```
