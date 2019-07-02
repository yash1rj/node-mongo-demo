----
## Connecting to the Database
MongoDB, by default, runs on port 27017. We connect to the database by telling it the location of the database and the name of the database.

In our app.js file after the line for the port and before the app.use line, enter the following two lines to get access to mongoose and to connect to the database. For the database, I am going to use “node-mongo-demo”.

----
## Creating a Database Schema
Once the user enters data in the input field and clicks the add button, we want the contents of the input field to be stored in the database. In order to know the format of the data in the database, we need to have a Schema.

We will need a very simple Schema that has only two fields. I am going to call the field firstName and lastName. The data stored in both fields will be a String.

After connecting to the database in our app.js we need to define our Schema.

Once we have built our Schema, we need to create a model from it. I am going to call my model “User”.

----
## Creating a RESTful API
Now that we have a connection to our database, we need to create the mechanism by which data will be added to the database. This is done through our REST API. We will need to create an endpoint that will be used to send data to our server. Once the server receives this data then it will store the data in the database.

An endpoint is a route that our server will be listening to to get data from the browser. We already have one route that we have created already in the application and that is the route that is listening at the endpoint “/” which is the homepage of our application.

----
## Building a CRUD endpoint
The form in our index.html file uses a post method to call this endpoint. We will now create this endpoint.

In our previous endpoint we used a “GET” http verb to display the index.html file. We are going to do something very similar but instead of using “GET”, we are going to use “POST”.

----
## Express Middleware
To fill out the contents of our endpoint, we want to store the firstName and lastName entered by the user into the database. The values for firstName and lastName are in the body of the request that we send to the server. We want to capture that data, convert it to JSON and store it into the database.

Express.js version 4 removed all middleware. To parse the data in the body we will need to add middleware into our application to provide this functionality. We will be using the body-parser module.

Once the module is installed, we will need to require this module and configure it. The configuration will allow us to pass the data for firstName and lastName in the body to the server. It can also convert that data into JSON format. This will be handy because we can take this formatted data and save it directly into our database.

To add the body-parser middleware to our application and configure it, we can add the following lines directly after the line that sets our port.

----
## Saving data to database
Mongoose provides a save function that will take a JSON object and store it in the database. Our body-parser middleware, will convert the user’s input into the JSON format for us.

To save the data into the database, we need to create a new instance of our model that we created early. We will pass into this instance to the user’s input. Once we have it then we just need to enter the command “save”.

Mongoose will return a promise on a save to the database. A promise is what is returned when the save to the database completes. This save will either finish successfully or it will fail. A promise provides two methods that will handle both of these scenarios.

If this save to the database was successful it will return to the `.then` segment of the promise. In this case we want to send text back the user to let them know the data was saved to the database.

If it fails it will return to the `.catch` segment of the promise. In this case, we want to send text back to the user telling them the data was not saved to the database. It is best practice to also change the statusCode that is returned from the default 200 to a 400. A 400 statusCode signifies that the operation failed.

----
## Testing our code
Go to your terminal and enter the command node app.js to start our server. Open up the browser and navigate to the URL “http://localhost:3000”. We will see our index.html file displayed to you.

> Mongo should be running

Enter first name and last name in the input fields and then click the “Add Name” button. We should get back text that says the name has been saved to the database.
