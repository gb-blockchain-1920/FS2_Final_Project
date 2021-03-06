# Fullstack II Final Project
Deployed Website: https://gb-fullstackii-project.web.app/  
Github Repo: https://github.com/aalu1418/FS2_Final_Project

### Developer Information
- Deepanshu Gupta - 101253525
- Aaron Lu - 101278524
---

### Project Description & Specifications
A simple chat application that incorporates the Firebase Realtime Database for messaging & user conversations, Metamask for sending ether in the chat, and Express + Firebase Functions for the routing. Additionally, the application uses Firebase storage, authentication, and hosting for purposes from user management to profile image storage.

Must contain the following Client-side functionality:
- Entry page with intuitive navigation
  - Entry page is the login page with options for forgotten passwords and registering a new user
  - Simple chat navigation screen similar to common chat platforms
- Authentication - can be Firebase, basic, simulated, external, etc.
  - Use of firebase to manage the user registration and authentication process
  - Forgotten passwords & password reset are handled via an email from Firebase.
- User profile page
  - User profile page is accessed by click on the users name or picture.
  - Allows access to reset password, upload a profile picture, and attach a public key using Metamask
- Main App page with access that is different for authenticated users from nonauthenticated users
  - Authenticated users will see all available chats and messages in chat.html, and are automatically redireceted to chat.html from the login or registration page.
  - Nonauthenticated users will be automatically redirected to login.html. The framework of chat.html is visible for a moment but they have no access to the database.

About page with:
- Team info including mini-bio with pic for each team member
  - Short bios and links to github pages, etc are included
- Contact info placeholder
  - Email links are included in an icon using ```mailto:<example>@gmail.com```

Must contain the following Server-side functionality:
- Serving of content based on user requests
  - User request include the different chats, viewing their own profiles, receiving messages
  - Controlled via read permissions for the Firebase database & storage
  - URL requests are handled via Firebase functions & Express
- Handling of user submitted data
  - User submitted data includes sending messages, and uploading profile pictures
  - Controlled via write permissions for the database & storage
- Error handling
  - Various forms of error handling are included for the various listeners, function calls, etc

Interesting things:
  - Connecting Firebase Functions & Firebase Hosting
    - Firebase functions & Firebase hosting are two separate services that do not communicate when deployed ([link](https://stackoverflow.com/questions/56127080/how-can-i-serve-static-web-site-from-firebase-hosting-through-node-expressjs))
    - Solution is to place the hosting folder inside the functions folder and then the functions have access to the webpages
    - Additional solution, change the firebase.json rules to have hosting in the ```/functions/public/``` folder to speed up the loading and prevent file load errors.
  - Error handling for authentication listener ```check_user()```
    - Uses two functions in a race (timeout function vs get_user function)
    - When user is not authenticated get_user hangs - therefore timeout completes first and moves to the next step
---

### Testing Information
- Basic Instructions:
  1. Visit the deployed [website](https://gb-fullstackii-project.web.app/) and either login or register.
  2. Once logged in, the user can send messages to other registered users or send ether (if Metamask is present) using the two buttons in the bottom right corner.
  3. Click on the arrow next to the user's name to bring up the user profile. Here you can upload a profile image and connect your profile with Metamask. (A user must have their profile connected to Metamask to receive ether)
  4. There is an About and Logout button in the bottom right.
- Sending Message:
  1. Message is typed in the appropriate box and either the \<enter\> key or send button press will send it
  2. Realtime display of message will appear without refresh
  3. The sidebar with conversations automatically updates as well
  4. Conversations with the latest messages will move to the top of the list.
- Sending Ether:
  1. Select the button with a money icon in correct conversation
  2. Enter the amount and press send.
  3. Metamask will automatically start and guide a user through the process.
  4. The recipient must have their public key stored in the application by either registering (via profile page) or previously sending ether.
- Authenticated vs. Nonauthenticated
  - Authenticated:
    1. After authentication on the login or register page, user is automatically redirected to the chat page.
    2. If the user goes back to the login or register page, an automatic redirect will occur.
  - Nonauthenticated:
    1. If user visits chat page, an automatic redirect to the login page will occur.
- Password Reset & Forgot Password:
  1. Can be accessed from the login page or from the user profile
  2. Email is used to send a reset email via firebase
---

### Tools List
- [Bootstrap](https://getbootstrap.com/) for HTML/CSS/JS framework
- [Firebase](https://firebase.google.com/) for database & webhosting & functions
- [JQuery](https://jquery.com/) for DOM content (not really used yet)
- [Express](https://expressjs.com/) for routing URLs
---

### Ideas List: Ether transfer via chat app
- [x] Realtime database for storing messages & transactions
- [x] Authentication via Firebase using custom UI
- [x] HTML Layout
  - [x] Chat page (includes list of all chats, all possible conversations, conversation profile)
  - [x] Personal profile page
  - [x] About page
- [x] Chat Functionality - multiple chats, realtime messages
- [x] Ether transfer inside chat using metamask integration
- [x] ExpressJS for webpage routing & integration with Firebase Functions
---

### Task List
#### Aaron
- [x] experiment with Firebase
  - [x] write to database
  - [x] read from database
  - [x] store image in bucket
  - [x] get image in bucket - can access URL & display, not sure if need to download from storage
  - [x] setup authentication
    - [x] create login system to generate user
    - [x] access user data from a different page
    - [x] logout functionality
  - [x] secure database & retain functionality
    - [x] all authenticated users can pull everything from database
    - [x] all authenticated users can view everything from storage
    - [x] authenticated user can see info about everyone, but only specific data
    - [x] authenticated user can only see specific objects in storage
- [x] determine data (storage & database) storage structure
  - store in "sessions" (identified by users)
  - [x] create permissions in database for structure
- [x] integrate with existing framework
  - [x] login functionality
  - [x] new user functionality
  - [x] function for sending messages
    - [x] unique chat identifier
  - [x] function for getting messages
  - [x] get user list (people who you can send messages to, and get images)
  - [x] set user profile picture & profile page
- [x] chat functionality
  - [x] on left panel, open chat for particular user on clicking particular user's conversation box
  - [x] function for getting chat users for current logged in user
- [x] metamask integration
  - [x] get and save users public key
- [x] fix redirecting
  - [x] login page as default
  - [x] password reset
  - [x] 404 page handling
  - [x] auto-redirect depending on auth status
  - [x] ico image
- [x] connected Firebase Functions w/ ExpressJS for router
  - [x] deploy

#### Deepanshu
- [x] experiment with Bootstrap
  - [x] login page
  - [x] Register page
  - [x] Chat page layout
  - [x] css styling files and images for all pages
  - [x] profile picture and icons
  - [x] Message send bar and button with an icon
  - [x] Styling for Chatbox content
- [x] Register page
    [x] password and confirm password check
    [x] already a user link and render to login page
- [x] Login page
  - [x] provided the link if user is new
  - [x] forgot password option
- [x] Get the message and create message object for corresponding user (Chat page)
  - [x] Message to be entered as comma separated format (2 parameters: ethersToSent and receiver'saddress)
  - [x] Validations if anyone of the parameter is not null
  - [x] create msg objects
  - [x] get username/userid
  - [x] create msg objects array
  - [x] link username/userid with an array of msg objects
  - [x] Validation for if no/wrong msg is entered
  - [x] Display users on left sidepanel after getting the users list from db
- [x] metamask integration
  - [x] get and save users public key
  - [x] use metamask to send ether to a public address

---

### Notes Section
- [Aaron] make sure to add error handling for .then functions - complete
- [Aaron] 404 handling - complete
- [Deepanshu] Make sure to arrange the chat page layout acc to browser screen.
- [Deepanshu] Make sure to remove the uncommented which is kept, as of now, for reference. - complete
- [Aaron] need Deepanshu's email & gb id - complete
- [Aaron] final step is to add error handling & catching - complete
- [Aaron] setup validation in database - more advanced, future addition?
- [Aaron] future note - transfer more functions from front end (Firebase Hosting) to back end (Firebase Functions)
