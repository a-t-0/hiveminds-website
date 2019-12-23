This is an implementation of: https://medium.com/javascript-in-plain-english/full-stack-mongodb-react-node-js-express-js-in-one-simple-app-6cc8ed6de274

Forked from: https://github.com/manuquirozy/living-lab-app-repo

Combined with: https://medium.com/poka-techblog/simplify-your-javascript-use-map-reduce-and-filter-bd02c593cc2d

The changes are:

0. Removed the link to the original cloud account.

1. Wrote javascript method that takes the data (the entire table), and transforms the colum  `temperature` into an array and returns it.
That means you can show a specific entry of the datatable into the html/website.

What I have learned from this, is that, instead of making separate queries to get a specific region/entry of the data table in MongoDB, it appearently is conventional to copy the entire datatable into the application, every `x` (mili)seconds. And you can get whatever you want from this table by transforming its columns into arrays in the `app.js` which has the body/render of the html/website.

# How to use
To get an element from the mongoDB you must run the backend, and after that, in a separate cmd, run the front ent (client):
 If you get an error with npm start just type npm install <keyword> of error message, untill it doesn't give an error anymore. (repeat if the npm install gives an error as well).
0. look at https://github.com/a-t-0/living-lab-app-repo
open the project with netbeans
open cmd with administrative priviliges 
cd into subfolder /backend/`
npm install
npm start
Now the backend should be running. 
Then open a new cmd AS ADMIN
cd into the /client/ folder.
npm i ajv
npm install
npm install react-scripts
(Make sure you don't have any of the client files opened in notepad/netbeans when you do this)
then npm start then visit:http://localhost:3000/

# Understanding: client: 
0. The `AppV2.js` connects to the MongoDB database named `fullstack_app` as specified in line 13 of `/backend/server.js/` containing:
```
const dbRoute = 'mongodb://localhost:27017/fullstack_app';
```
Within the database `fullstack_app` it searches in the collection named:`datas` which I can't find anywhere.  
1. Then the first table displays the elements of all the documents in the collection `datas` that are listed in the columns.  (line 50 to 82).
2. If the document contains an element with element name that is not specified in the table columns, the table will just show an empty row.
3. The line:
```
dat.temperature={data.map((dat) => dat.temperature)}
```
displays the temperature. and the right part of the equal sign folds the dat.temperature value to contain all the values of element type temperatures into a single row.
To understand how the arrow (lambda function) works, look here: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions


4. To get a specific element of a datatype E.g. temperature you can create a function, and put that above the html:
getSingleEntry(data) {
        var officersIds = [];
        data.forEach(function (data) {officersIds.push(data.temperature);})   
        console.log(officersIds[2]);
        return officersIds[2];
    }
5. In the html in the `App.js` you can write comments with: `{/*This is a comment example*/}`
6. `AppV5` puts the dropdownbox in the front end that is connected to the database and functions that can display a single element. It also has the option to add/modify elements of the dropdownbox.
7. use <script> to hide the output of a computation. The result is stored beyond/after the scope of the script.
8. `AppV8` : Made anyonymous function which is only called upon button click, using: https://stackoverflow.com/questions/14425397/onclick-function-runs-automatically 
9. `AppV9` Made a function that is not executed on loading site, passes parameter and is called on click, using: https://upmostly.com/tutorials/pass-a-parameter-through-onclick-in-react
10. `AppV10` Fills a dropdownbox with the column `Temperature` of a collection named datas in db `fullstack_app`.
11. You can make a backup of your mongoDB collections after you have downloaded the tools from: https://www.mongodb.com/download-center/community?jmp=docs
To export db, see instructions at: https://docs.mongodb.com/manual/reference/program/mongoexport/ use: mongoexport --collection=<collection name>
11.a Connection string = mongodb://localhost:27017/?readPreference=primary&appname=MongoDB%20Compass%20Community&ssl=false
11.b To run the server, use first create `c:/data\db`, then add `C:\Program Files\MongoDB\Server\4.2\bin` to path in environment variables `path`.
11.c then run `mongod.exe` (note the d.)
11.d In the future add C:\Program Files\MongoDB\Server\4.2\bin/mongod.exe to startup on your server.
12. To implement (one)/many to many relations just enter the document id to each respective collection, as explained in: http://blog.markstarkman.com/blog/2011/09/15/mongodb-many-to-many-relationship-data-modeling/
12.a so at university, add all the id's of the faculty, then at faculty, add the university.
12.b then at faculty, add bachelor and master, then at bachelor add faculty.
12.c then at e.g. bachelor, add courses, at courses at bachelor (OR master).

13. You can automate starting up the mongdb server with: 

14.a YOu can select the database in file: 
14.b You can select the collection in file `/backend/data.js` in line: `module.exports = mongoose.model("universities", DataSchema);`
14.c TODO: Find out whether/how you can access multiple collections (from different databases, on 1 webpage).