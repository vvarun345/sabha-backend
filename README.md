# sabha-backend
Backend routes and database for KM Portal sabha

To install flask and mongoengine : pip install flask-mongoengine

To run the server : python3 app.py

The server by default runs on localhost:5000

# The following APIs have been added : 
# Add User : 
route : localhost:5000/api/user/add  |  method : PUT

request body : {"username":"username for user","password":"password for the account","full_name":"users full name","email":"users email-id","dob":"date of birth","phone":"phone number"}
(username,password,full_name required, remaining optional)

response : 200 = success, 400 = failure

# Retrieve list of all users, full-name, email, phone and role
route : localhost:5000/api/user/list | method : GET

request body : not required

response : 200 = success

# Update role of a user
route : localhost:5000/api/user/role_update | method = POST

request body : {"username":"username of user whose role is to be updated","role":"new role"}

response : 200 = success 400 = failure
# Add Post :
route : localhost:5000/api/posts/add | method = POST

request body : {"author":"username of post writer","title":"title of post","description":"post details"}

response : 200 = success body = {'id': post_id}  | 400 =failure

post_id must be stored in the frontend, and sent in body when comment/upvote/downvote on post is done

# Add Comment to a post :
route : localhost:5000/api/posts/comment/add | method = POST

request body : {"post_id":"id of post to which comment is added", "author":"username of comment writer", "description":"comment beng added"}

response : 200 = success | 400 = failure

# Upvote a post :
route : localhost:5000/api/posts/upvote | method = POST

request body: {"post_id":postid,"user": username of user who is upvoting}

response : 200 = success | 201 = already voted | 400 failure

# Downvote a post :
route : localhost:5000/api/posts/downvote | method = POST

request body: {"post_id":postid,"user": username of user who is downvoting}

response : 200 = success | 201 = already voted | 400 failure

# Retrieve a Post :
route : localhost:5000/api/posts/id | GET
  
request body : not required
  
response : { "_id": { "$oid": "5e8ad25d9e6029fcf8a2594f"},
             "author": "username of author",
             "comments": [list of comments],
             "description": "Post content",
             "downvotes": [list of users who have downvoted],
             "timestamp": { "$date": 1586175925169 },
             "title": "Post Title",
             "upvotes": [list of users who commented],
             "votes": 0 (integer : upvotes-downvotes) }
200 - success 400 - failure

# Retrieve all Posts :
route : localhost:5000/api/posts  | GET

request body : not required

response : a list of posts(post list may be empty if no post added). 200 - success

# Retrieve all Posts by a user :
route : localhost:5000/api/posts/user/user_name | GET

request body : not required

response : 200 - success | 400 - failure

# Retrieve all Posts by a keyword :
route : localhost:5000/api/posts/keyword/key_word | GET

request body : not required

response : 200 - success | 400 - failure
