<h1>
  <span class="headline">Server Development with Flask</span>
  <span class="subhead">Creating a Basic Flask Server</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to create a basic Flask server, define and handle routes, and respond to HTTP requests using Python.

| Lesson                        | Duration |
| ----------------------------- | -------- |
| Creating a Basic Flask Server | 30 min   |

## Setting Up Your First Flask Server

Lets review the code you would use to create a simple Flask server:

```python
from flask import Flask  # Import the Flask class to create an app

# Create an instance of the Flask class
app = Flask(__name__)

# Define the first route, the home route
@app.route('/')
def index():
    return 'Hello, World!'  # Define the function that responds to the above route

# Start the server listening for requests
if __name__ == '__main__':
    app.run()
```

## What's in the box?

### App Instance:

- `app = Flask(__name__)` creates an instance of the Flask class. This `app` object is the central part of your application. The argument `__name__` helps Flask determine the root path for your application, allowing it to locate resources like templates and static files.

- Using `__name__` ensures that Flask has the correct path depending on how the app is run. It’s a special variable in Python that represents the name of the module.

### Defining Routes:

- The `@app.route('/')` decorator is used to create a route. In Flask, a route maps a URL to a Python function. This route is associated with the root URL (`/`), which is typically the home page of your web application.

- The `index()` function is defined to handle requests to this route. When someone visits the home page, the function is triggered, and the string `'Hello, World!'` is returned as the response. This response is then sent back to the client (e.g., a web browser), which displays it on the screen.

### Starting the Server:

- The `if __name__ == '__main__':` block is a standard Python idiom used to check if the script is being run directly or being imported elsewhere as a module. If it’s run directly, the Flask application will start.

- The `app.run()` method starts Flask’s built-in development server. This server will listen for incoming requests on the default port 5000. Flask provides this simple server for testing purposes, making it easy to see your application in action during development.

- You can modify `app.run()` to change the behavior of the server, such as enabling debug mode (`app.run(debug=True)`) or changing the port (`app.run(port=8080)`).

## Guided Walk-Through: Running a Flask Application 15 min TKTK

Let's run through starting up a Flask server together.

### Running Your Flask Server

1. **Navigate to Your Starter Code Directory:**

   Open your terminal or command prompt, and navigate to the directory where your `app.py` file is located.

2. **Start the Flask Server:**

   To start your Flask server, run the following command in your terminal:

   ```bash
   python app.py
   ```

   > **Note:** Depending on how Python is installed on your system, you may need to use `python3` instead of `python`.
   >
   > ```bash
   > python3 app.py
   > ```

3. **Access the Server:**

   Once the server is running, you can access it by opening your web browser and going to [http://localhost:5000](http://localhost:5000). This is the default address where Flask serves your application.

4. **Stop the Server:**

   To stop the server, simply return to your terminal and press `Ctrl+C`. This will terminate the running Flask process.

Note the elements of the server's output, especially when a request is made from the browser and logged in the server.

## Discussion: HTTP Requests and Methods TKTK

Our Flask application's goal is to respond to HTTP requests from users.

Before we go further, **_what are the properties of an HTTP request?_**

<details>
<summary>✅ Click to see the answer: </summary>
<hr>

<p>URL: Specifies the address of the resource being requested, including the path and optional query parameters (e.g., /products?category=shoes).</p>

<p>HTTP Methods:</p>

<ul>
<li>GET: Retrieves information from the server without altering it.</li>
<li>POST: Sends data to create a new resource.</li>
<li>PUT: Updates an existing resource.</li>
<li>DELETE: Removes a resource.</li>
</ul>

</details>

## Creating Routes in Flask

In Flask, a **route** is a mapping between a URL and a function in your code. When a user makes a request to a specific URL, Flask uses the route to determine which function should handle the request and what content should be returned. Routes are essential for defining the different endpoints your application will expose.

Here's a basic example:

```python
@app.route("/products", methods=["GET"])
def index():
    return {"response_code": 200, "data": "Hello from the products index"}
```

### Breaking Down the Route

- **`@app.route("/products")`**: This line defines the route. It tells Flask that when a user makes a GET request to the `/products` URL, the `index` function should be executed.

- **`methods=["GET"]`**: This specifies that the route only responds to GET requests. Flask supports various HTTP methods, such as GET, POST, PUT, DELETE, etc. By specifying the method, you're telling Flask how the route should be accessed.

- **`return { "response_code": 200, "data": "Hello from the products index" }`**: This is the response that will be sent back to the client. Flask automatically converts the Python dictionary into a JSON response, which is a common format for data exchange in APIs.

### Understanding the URL Path

- The URL path provided in `@app.route("/products")` determines where the route is accessible. In this case, `/products` means that if a user visits `"www.yourdomain.com/products"`, they will trigger the `index` function.

- All routes in Flask start with `/`, which is the root of the application. For example, the home page of your site might be defined as `@app.route("/")`.

## Creating Dynamic Routes in Flask

Dynamic routes allow you to capture values from the URL and use them within your function. This is particularly useful when working with resources that have unique identifiers, such as individual products in an e-commerce application.

Here's how you can create a dynamic route:

```python
@app.route("/products/<product_id>", methods=["GET"])
def get_product(product_id):
    return {"response_code": 200, "data": f"Product details for {product_id}"}
```

### How Dynamic Routes Work

- **`@app.route("/products/<product_id>")`**: The `<product_id>` part of the route is a placeholder. Flask captures whatever value is in this position in the URL and passes it as an argument to the `get_product` function.

- **`def get_product(product_id)`**: The captured value is passed as the `product_id` parameter to the function. This allows you to use the `product_id` inside your function to determine the appropriate response.

### Example Use Cases

- If a user visits `/products/123`, the `get_product` function will receive `123` as the `product_id`.

- If a user visits `/products/abcd1234`, the function will receive `abcd1234` as the `product_id`.

This approach is fundamental in RESTful APIs, where you often need to handle resources identified by unique IDs. For example:

- **GET** `/products/123`: Retrieve details for the product with ID 123.

- **DELETE** `/products/123`: Delete the product with ID 123.

Dynamic routes allow you to build flexible endpoints that cater to a wide range of user interactions with your application.
