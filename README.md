CENG 495 Cloud Computing Assignment 2

EXPLANATIONS:

I used JavaScript for communicating MongoDB, dynamically adding values to HTML, button click actions and page redirections.
And for the views, HTML and CSS is used.

##App Files:

index.html: To start the application, index file should be run on browser. This file connects to Stitch app which is linked to a MongoDB Atlas Cluster.
Add user, delete user and login options are implemented in this page. Username values are ensured to be unique (controlled by js before adding). You should first add a username to be able to login. Index page redirects to user page after login.

user.html: This page displays username and user rating (the average rating of all products of the user). Users with no product have 0 rating. Also, if a product is not rated yet, its rating is 0 too.
User page has a form to Exhibit a new invention. Fields other than "optional field 1" and "optional field 2" should be non empty. Also, before adding a product, its product name is checked if it's present in the db or not. Because product names should be unique since they are used as key for rating dropping etc. 
The invention gallery shows all inventions from all users. By clicking the invention name below the picture, you can redirect to the invention page.

invention.html: Other informations about the product (product owner, photo, name, cost, material, rating and optional elements) can be seen on this page. 
To drop the product, the username should match the product owner name. In the database, I used a field called "isVisible" for each product, which toggles to false when a product is dropped.
If a user is rating for the first time, a rating record is created in db. Else, the value of the record is updated.
Also, overall rating of the product is calculated when the page is uploading, so after submitting a new rating you should refresh the page to see the updated result. 

styles/style.css: Contains stying for html files.

##Database Design Choices:

I created a collection called 'users' under the database 'ceng495_hw2_db'.
Objects have the following fields:

_id: default id
user_name: unique name of the user
inventions: An array that contains invention objects
    [
        productName: name of the invention
        productPhoto: url of the invention picture
        productCost: cost of the invention
        productMaterial: material(s) of the invention
        ratings: an array that contains (username, rating value) pairs
            [
                rating_user: name of the user who submitted the rating
                rating_value: an int value between 1 and 5
            ]
        totalRating: average of ratings for the invention
        isVisible: the boolean value for displaying the invention on the user page
        optionalElement1: any optional info about the invention
        optionalElement1: any optional info about the invention
    ]