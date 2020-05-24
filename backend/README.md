# Full Stack Trivia API Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Environment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by navigating to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py. 

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

## Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
psql trivia < trivia.psql
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application. 

## Tasks

One note before you delve into your tasks: for each endpoint you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior. 

1. Use Flask-CORS to enable cross-domain requests and set response headers. 
2. Create an endpoint to handle GET requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories. 
3. Create an endpoint to handle GET requests for all available categories. 
4. Create an endpoint to DELETE question using a question ID. 
5. Create an endpoint to POST a new question, which will require the question and answer text, category, and difficulty score. 
6. Create a POST endpoint to get questions based on category. 
7. Create a POST endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question. 
8. Create a POST endpoint to get questions to play the quiz. This endpoint should take category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions. 
9. Create error handlers for all expected errors including 400, 404, 422 and 500. 


## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```
When running the tests for the first time, you need to omit the dropdb command.


## API REFERENCE

# GET '/categories'
General:
    - Returns a dictionary of category objects and success value.
Sample:
    curl http://127.0.0.1:5000/categories

    {
    "categories": {
        "1": "Science", 
        "2": "Art", 
        "3": "Geography", 
        "4": "History", 
        "5": "Entertainment", 
        "6": "Sports"
    }, 
    "success": true
    }

  
# GET '/questions'
General:
    - Returns a list of question objects, a dictionary of categories, success value, total number of questions, and current categories (which is null)
    - Results are paginated in groups of 10.

Sample:
    curl http://127.0.0.1:5000/questions

    {
    "categories": {
        "1": "Science", 
        "2": "Art", 
        "3": "Geography", 
        "4": "History", 
        "5": "Entertainment", 
        "6": "Sports"
    }, 
    "current_category": null, 
    "questions": [
        {
        "answer": "Apollo 13", 
        "category": 5, 
        "difficulty": 4, 
        "id": 2, 
        "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
        }, 
        {
        "answer": "Tom Cruise", 
        "category": 5, 
        "difficulty": 4, 
        "id": 4, 
        "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
        }, 
        {
        "answer": "Edward Scissorhands", 
        "category": 5, 
        "difficulty": 3, 
        "id": 6, 
        "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
        }, 
        {
        "answer": "Muhammad Ali", 
        "category": 4, 
        "difficulty": 1, 
        "id": 9, 
        "question": "What boxer's original name is Cassius Clay?"
        }, 
        {
        "answer": "Brazil", 
        "category": 6, 
        "difficulty": 3, 
        "id": 10, 
        "question": "Which is the only team to play in every soccer World Cup tournament?"
        }, 
        {
        "answer": "Uruguay", 
        "category": 6, 
        "difficulty": 4, 
        "id": 11, 
        "question": "Which country won the first ever soccer World Cup in 1930?"
        }, 
        {
        "answer": "George Washington Carver", 
        "category": 4, 
        "difficulty": 2, 
        "id": 12, 
        "question": "Who invented Peanut Butter?"
        }, 
        {
        "answer": "Lake Victoria", 
        "category": 3, 
        "difficulty": 2, 
        "id": 13, 
        "question": "What is the largest lake in Africa?"
        }, 
        {
        "answer": "The Palace of Versailles", 
        "category": 3, 
        "difficulty": 3, 
        "id": 14, 
        "question": "In which royal palace would you find the Hall of Mirrors?"
        }, 
        {
        "answer": "Agra", 
        "category": 3, 
        "difficulty": 2, 
        "id": 15, 
        "question": "The Taj Mahal is located in which Indian city?"
        }
    ], 
    "success": true, 
    "total_questions": 23
    }


# DELETE '/questions/<int:question_id>'
General:
    - Deletes the question of the given question ID if it exists. Returns the id of the deleted question and success value.

Sample:
    curl -X DELETE http://127.0.0.1:5000/questions/5

    {
    "deleted": 5, 
    "success": true
    }


# POST '/questions'
This endpoint either creates a new question or return search results based on the provided search term.
1). This endpoint will create a new question if there is no search term included in the request.
General:
    - Creates a new question using the submitted question, answer, difficulty, and category. Returs the id of the created question, success value, the number of total questions, and a question list based on current page number.

Sample:
    curl -X POST http://127.0.0.1:5000/questions -H "Content-Type: application/json" -d '{"question":"When used in the kitchen, sodium bicarbonate is more commonly known as what?","answer":"Baking Soda","difficulty":2,"category":1}'

    {
    "created": 29, 
    "questions": [
        {
        "answer": "Apollo 13", 
        "category": 5, 
        "difficulty": 4, 
        "id": 2, 
        "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
        }, 
        {
        "answer": "Tom Cruise", 
        "category": 5, 
        "difficulty": 4, 
        "id": 4, 
        "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
        }, 
        {
        "answer": "Edward Scissorhands", 
        "category": 5, 
        "difficulty": 3, 
        "id": 6, 
        "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
        }, 
        {
        "answer": "Muhammad Ali", 
        "category": 4, 
        "difficulty": 1, 
        "id": 9, 
        "question": "What boxer's original name is Cassius Clay?"
        }, 
        {
        "answer": "Brazil", 
        "category": 6, 
        "difficulty": 3, 
        "id": 10, 
        "question": "Which is the only team to play in every soccer World Cup tournament?"
        }, 
        {
        "answer": "Uruguay", 
        "category": 6, 
        "difficulty": 4, 
        "id": 11, 
        "question": "Which country won the first ever soccer World Cup in 1930?"
        }, 
        {
        "answer": "George Washington Carver", 
        "category": 4, 
        "difficulty": 2, 
        "id": 12, 
        "question": "Who invented Peanut Butter?"
        }, 
        {
        "answer": "Lake Victoria", 
        "category": 3, 
        "difficulty": 2, 
        "id": 13, 
        "question": "What is the largest lake in Africa?"
        }, 
        {
        "answer": "The Palace of Versailles", 
        "category": 3, 
        "difficulty": 3, 
        "id": 14, 
        "question": "In which royal palace would you find the Hall of Mirrors?"
        }, 
        {
        "answer": "Agra", 
        "category": 3, 
        "difficulty": 2, 
        "id": 15, 
        "question": "The Taj Mahal is located in which Indian city?"
        }
    ], 
    "success": true, 
    "total_questions": 24
    }

2). This endpoint will return search results if there is a search term included in the request.
General:
    - Searches for questions using the search term in JSON request parameters.
    - Returns JSON object with paginated matching questions, success value, and the number of questions that contain the provided search term.

Sample:
    curl -X POST http://127.0.0.1:5000/questions -H "Content-Type: application/json" -d '{"searchTerm": "Mahal"}'

    {
    "questions": [
        {
        "answer": "Agra", 
        "category": 3, 
        "difficulty": 2, 
        "id": 15, 
        "question": "The Taj Mahal is located in which Indian city?"
        }
    ], 
    "success": true, 
    "total_questions": 1
    }


# GET '/categories/<int:category_id>/questions'
General:
    - Returns a list of question objects based on a given category ID, success value, total number of questions, and the provided category ID.

Sample:
    curl http://127.0.0.1:5000/categories/1/questions

    {
    "current_category": 1, 
    "questions": [
        {
        "answer": "The Liver", 
        "category": 1, 
        "difficulty": 4, 
        "id": 20, 
        "question": "What is the heaviest organ in the human body?"
        }, 
        {
        "answer": "Alexander Fleming", 
        "category": 1, 
        "difficulty": 3, 
        "id": 21, 
        "question": "Who discovered penicillin?"
        }, 
        {
        "answer": "Blood", 
        "category": 1, 
        "difficulty": 4, 
        "id": 22, 
        "question": "Hematology is a branch of medicine involving the study of what?"
        }, 
        {
        "answer": "Mars", 
        "category": 1, 
        "difficulty": 3, 
        "id": 28, 
        "question": "Which planet has a moon named Phobos?"
        }, 
        {
        "answer": "Baking Soda", 
        "category": 1, 
        "difficulty": 2, 
        "id": 29, 
        "question": "When used in the kitchen, sodium bicarbonate is more commonly known as what?"
        }
    ], 
    "success": true, 
    "total_questions": 5
    }


# POST '/quizzes'
General:
    - It allows user to play the quiz game. User will be presented a random question. It uses JSON request parameters of category and previous questions. It returns JSON object of a random question that does not exist in previous questions, and success value.

Sample:
    curl http://127.0.0.1:5000/quizzes -X POST -H "Content-Type: application/json" -d '{"previous_questions": [18, 19], "quiz_category": {"type": "Art", "id": "2"}}'

    {
    "question": {
        "answer": "Escher", 
        "category": 2, 
        "difficulty": 1, 
        "id": 16, 
        "question": "Which Dutch graphic artist-initials M C was a creator of optical illusions?"
    }, 
    "success": true
    }


## ERROR HANDLING
Errors are returned as JSON objects in the following format:

{
  "error": 422, 
  "message": "unprocessable", 
  "success": false
}

The API will return 4 error types when requests fail:
    - 400: Bad Request
    - 404: Resource Not Found
    - 422: Unprocessable



