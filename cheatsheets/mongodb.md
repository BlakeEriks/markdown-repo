# MongoDB

MongoDB is a NoSQL database, where data is stored in JavaScript objects.

MongoDB clusters consist of sub-databases.

Sub-databases consist of collections.

Collections consist of documents.

## Mongoose starter code

``` js
// Dependencies
const express = require('express');
const mongoose = require('mongoose');
const app = express();
const PORT = 3000;

// Database Configuration
const DATABASE_URL =
	'mongodb+srv://sei:<password>@sei-w0kys.azure.mongodb.net/tweeter?retryWrites=true';
const db = mongoose.connection;

// Database Connection
mongoose.connect(DATABASE_URL, {
	useNewUrlParser: true,
	useUnifiedTopology: true,
	useFindAndModify: false,
	useCreateIndex: true,
});

// Database Connection Error/Success - optional but can be really helpful
db.on('error', (err) => console.log(err.message + ' is Mongod not running?'));
db.on('connected', () => console.log('mongo connected'));
db.on('disconnected', () => console.log('mongo disconnected'));

// App Listener
app.listen(PORT, () => console.log(`express is listening on port: ${PORT}`));
```