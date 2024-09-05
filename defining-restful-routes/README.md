<h1>
  <span class="headline">Server Development with Flask</span>
  <span class="subhead">Defining RESTful Routes</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to define and implement RESTful routes in a Flask application, understand the purpose of each route, and apply these conventions to build and structure APIs effectively.

| Lesson                  | Duration |
| ----------------------- | -------- |
| Defining RESTful Routes | 50 min   |

## The Seven RESTful Routes

| **URL Path**           | **Method** | **Name** | **Purpose**                               |
| ---------------------- | ---------- | -------- | ----------------------------------------- |
| `/employees`           | GET        | index    | Show the home page for this collection    |
| `/employees`           | POST       | create   | Add a new record to a collection          |
| `/employees/<id>`      | GET        | show     | Show details of a specific record         |
| `/employees/<id>`      | PUT        | update   | Update details of a specific record       |
| `/employees/<id>`      | DELETE     | delete   | Delete a record                           |
| `/employees/new`       | GET        | new      | Show the form to create a new record      |
| `/employees/<id>/edit` | GET        | edit     | Show the form to update a specific record |

### Why These Seven Routes Are Essential in RESTful APIs

The seven routes outlined in the table above are considered a best practice and a near-universal convention in **RESTful** API development because they represent the full lifecycle of interacting with a resource:

1. **GET /index**: Provides a way to list all resources. For example, in an employee management system, you might want to see a list of all employees. This route allows users to retrieve and view that list.

2. **POST /create**: Enables the creation of a new resource. In the employee management example, this route would allow the addition of a new employee to the system.

3. **GET /show**: Retrieves details about a specific resource. If you need detailed information about a particular employee, this route will provide it by fetching data for that specific employee ID.

4. **PUT /update**: Allows users to update an existing resource. This is crucial for maintaining accurate records. For example, if an employee changes their address or job title, this route would handle the update.

5. **DELETE /delete**: Provides the functionality to remove a resource. If an employee leaves the company, this route would allow the removal of that employee's data from the system.

6. **GET /new**: Typically used in full-stack applications to display a form for creating a new resource. For instance, this route could render a form where a user can input details for a new employee.

7. **GET /edit**: Similar to the "new" route, this one is used to show a form for editing an existing resource. If you need to change an employee's details, this route would bring up the necessary form pre-filled with the current data.

> 💡 Note that the bottom two routes (`/new` and `/edit`) are more relevant for applications with user interfaces, where forms are used to create or edit data. In pure data APIs, these routes are optional but can still be useful for rendering or documentation purposes.

### The Importance of Convention

These seven routes are part of a standard **RESTful architecture** that helps developers quickly understand and interact with APIs, regardless of who built them. By following this convention:

- APIs become predictable, which makes them easier to use and integrate with other systems.

- Developers can spend less time figuring out how to interact with an API and more time focusing on building features.

- Using these standard routes helps ensure that your API can easily grow and adapt as your application evolves.

<img src="./assets/pen-and-paper.png" alt="Pen and Paper" style="width: 300px; height: auto;">

<br>

<div class="activity group-exercise">
  <h2 class="title">2.2 API Routes</h2>
  <span class="minutes">40 min</span>
</div>

In this activity, you will create the seven routes listed in the table below for a restaurant reviews application. These routes won't be fully functional, instead, they will return simple strings that describe the purpose of each route. This will help you understand how to set up basic routes and test them in Flask.

| **URL Path**         | **Method** | **Name** | **Purpose**                             |
| -------------------- | ---------- | -------- | --------------------------------------- |
| `/reviews`           | GET        | index    | Show the home page for this collection  |
| `/reviews`           | POST       | create   | Add a new item to a collection          |
| `/reviews/<id>`      | GET        | show     | Show details of a specific item         |
| `/reviews/<id>`      | PUT        | update   | Update details of a specific item       |
| `/reviews/<id>`      | DELETE     | delete   | Delete an item                          |
| `/reviews/new`       | GET        | new      | Show the form to create a new item      |
| `/reviews/<id>/edit` | GET        | edit     | Show the form to update a specific item |

### Define the Routes

- For each route in the table, create a corresponding function that returns a string describing what the route does.

- Use the Flask `@app.route()` decorator to define each route and specify the appropriate HTTP method `(GET, POST, PUT, DELETE)`.

Example for the `/reviews GET` route:

```python
@app.route('/reviews', methods=['GET'])
def index():
    return "Show the home page for this collection"
```

### Testing Each Route:

- After defining a route, run your Flask server using `python app.py`.

- Test each route by visiting the corresponding URL in your browser or using a tool like Postman or cURL.

#### Example tests:

- **Browser:** Open your browser and go to `http://127.0.0.1:5000/reviews` to see the response for the index route. The browser can be use to test the `GET` routes.

- **Postman:** Use [Postman](https://www.postman.com/) to send `GET`, `POST`, `PUT`, and `DELETE` requests to the routes you've defined, verifying the responses.

- **cURL:** `cURL` is a versatile command-line tool that is available and can be used in most terminal environments across different operating systems, including Windows, macOS, and Linux. You can send `GET`, `POST`, `PUT`, and `DELETE` requests using `cURL` with the following commands:
  - GET
    ```bash
    curl http://127.0.0.1:5000/reviews
    ```
  - POST
    ```bash
    curl -X POST http://127.0.0.1:5000/reviews -d "review=Great food!"
    ```
  - PUT
    ```bash
    curl -X PUT http://127.0.0.1:5000/reviews/1 -d "review=Updated review"
    ```
  - DELETE
    ```bash
    curl -X DELETE http://127.0.0.1:5000/reviews/1
    ```

> Browsers can only test GET requests directly by entering a URL because they are designed to retrieve and display content; other methods like POST, PUT, and DELETE require tools like Postman or cURL.
