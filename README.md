
# Foodtacular

## Table of Contents
1. [Overview](#Overview)
1. [Product Spec](#Product-Spec)
1. [Wireframes](#Wireframes)
2. [Schema](#Schema)

## Overview
### Description
An app that allows users to plan and track their diet and health.

### App Evaluation
- **Category: Health**
- **Mobile: iOS**
- **Story: **
- **Market: Fitness Industry**
- **Habit: Make it easy for people to track calories**
- **Scope: Calorie Tracker**

## Product Spec

### 1. User Stories (Required and Optional)

**Required Must-have Stories**

* Login Page
* API Requests for Food
* Ingredients Aggregator (Summing up the calories)
* User can set goals

**Optional Nice-to-have Stories**

* Calendar view with data for each date.
* Graph view with progess indicator
* Settings page
* User Profile Page
* Friends Progress Page

### 2. Screen Archetypes

* Login 
   * Associated Accounts (google, apple, facebook)
* Register - User signs up or logs into their account
   * Upon Download/Reopening of the application, the user is prompted to log in to gain access to their profile information to be properly matched with another person. 
* Settings Screen
   * Lets people change language, and app notification settings.
* Profile Screen 
   * Allows user to upload a photo and edit their diet plans and goals.
* Diet Plan Screen.
   * Allows users to edit and choose prefrences in terms of diet goals.

### 3. Navigation

**Tab Navigation** (Tab to Screen)

* Day's Nutrition setter
* Feed View
* Settings

**Flow Navigation** (Screen to Screen)

* Log-in -> Account creation if no log in (apple, google, facebook)
* User enters Data on meals that they have eaten in the day -> Data is compiled and stored for the day specfied
* Screen showing data collected and user's progress.
* Feed View showcases data from other users. (Bonus Story)
* Settings page -> User can change goals.

## Wireframes
<img src="https://i.imgur.com/ummsM7x.jpg" width=600>

### [BONUS] Digital Wireframes & Mockups

### [BONUS] Interactive Prototype

## Schema 
### Models
#### Post

   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | objectId      | String   | unique id for the user post (default field) |
   | author        | Pointer to User| submission author |
   | image         | File     | image submitted by author |
   | description   | String   | description by author |
   | ingredients   | Hash     | ingredients for recipe |
   | favorites     | Number   | favorited items by the author |
   | likesCount    | Number   | number of likes for the post |
   | createdAt     | DateTime | date when post is created (default field) |
   | updatedAt     | DateTime | date when post is last updated (default field) |
### Networking
#### List of network requests by screen
   - Home Feed Screen
      - (Read/GET) Query all posts where user is author
         ```swift
         let query = PFQuery(className:"Post")
         query.whereKey("author", equalTo: currentUser)
         query.order(byDescending: "createdAt")
         query.findObjectsInBackground { (posts: [PFObject]?, error: Error?) in
            if let error = error { 
               print(error.localizedDescription)
            } else if let posts = posts {
               print("Successfully retrieved \(posts.count) posts.")
           // TODO: Do something with posts...
            }
         }
         
         let recipe = PFObject(className:"recipe")
         recipe["creator"] = Username
         recipe["image"] = true
         recipe["fav"] = fav
         recipe.saveInBackground { (succeeded, error)  in
             if (succeeded) {
                  // The object has been saved.
             } else {
                  // Error 
             }
         }
         ```
      - (Delete) Delete existing recipe
      - (Create) Create a new recipe
      - (Create/POST) Create a new like on a post
      - (Delete) Delete existing like
      - (Create/POST) Create a new comment on a post
      - (Delete) Delete existing comment
   - Create Post Screen
      - (Create/POST) Create a new post object
   - Profile Screen
      - (Read/GET) Query logged in user object
      - (Update/PUT) Update user profile image
#### [OPTIONAL:] Existing API Endpoints
##### An API Of Spoonacular
- Base URL - [https://api.spoonacular.com/](https://api.spoonacular.com/)

https://api.spoonacular.comapples,+flour,+sugar&number=2

   HTTP Verb | Endpoint | Description
   ----------|----------|------------
    `GET`    | /ingredients | get all ingredients
    `GET`    | /recipes/findByIngredients?ingredients= | return recipes
    `GET`    | /recipes/{id}/nutritionWidget.json   | gets nutrition for recipe
    `GET`    | /food/menuItems/search?query=burger&number=2 | return information from restaurants
    
    

What we have so far :
    
<img src="http://g.recordit.co/SNHFMgGeSd.gif" width=200>
    
    
