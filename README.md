# School Emergency App

## Table of Contents
1. [Overview](#Overview)
1. [Product Spec](#Product-Spec)
1. [Wireframes](#Wireframes)
2. [Schema](#Schema)
3. [Gifs](#Gifs)


## Overview
### Description
An app to alert and communicate with other teachers/administrators when there is an emergency instead of using the intercom for increased security and communication in school emergency situations.

### App Evaluation
- **Category:** Communication/safety
- **Mobile:** This app is being created for mobile use but would be useful as a website as well for access from any device for universal access to the alert system by teachers and administrators.
- **Story:** The stripped down version of this app may not be particularly interesting to peers or classmates, but they are not the intended audience. The value should be evident in the design and implementation of the app.
- **Market:** The market for this app is limited to school teachers and administrators to be used in the spirit of safety. Valuable to all grade schools, and potentially colleges and businesses if developed further.
- **Habit:** This app is not habit forming and the current stripped down version would only necessarily be used when there is an emergency that requires immediate campus-wide communication.
- **Scope:** This app is for teachers and administrators in emergency situations, but it has potential to be developed into a general communcation app for professional messaging and extend to all educational institutions and businesses.

## Product Spec

### 1. User Stories (Required and Optional)

**Required Must-have Stories**


- [x]  Network is set up. 
- [X]  Network captures registered user.
- [x]  Each button leads to the correct screen. 
- [x]  App functions as intended. 


**Optional Nice-to-have Stories**

- [ ] Messaging Screen: chart for users to communicate
- [ ] Ability to track attendance of students

### 2. Screen Archetypes

* Login
   * User logs into their account
* Register 
   * User creates an account using name, school email, and password
   
* Home Screen 
   * User browses alerts in the home page
* Alert Screen
   * User chooses specific type of alert to post
* Confirm Screen 
   * User confirms or exits the alerts chosen before

### 3. Navigation

**Tab Navigation** (Tab to Screen)

* Alert selection
* Confirm alert

**Flow Navigation** (Screen to Screen)

* Forced Log-in -> Account creation if no log in is available
* Alert selection -> Jumps to alert post page 
* Confirm Alert -> Confirm or exit the alert chosen before 

## Wireframes
[Add picture of your hand sketched wireframes in this section]

<img src="https://i.imgur.com/UBfLSFn.jpg" width=600>


### [BONUS] Digital Wireframes & Mockups
<img src="https://i.imgur.com/xDECcc5.png"
 width=600>

### [BONUS] Interactive Prototype
<img src="https://i.imgur.com/TQk7hcn.gif" title='Video Walkthrough' width='' alt='Video Walkthrough' />


## Schema 
[This section will be completed in Unit 9]
### Models
| Property | Type | Description|
| -------- | -------- | -------- |
|createdAt   |DateTime  | Date when post is created (default field)    |
updatedAt | DateTime | Date when post was last updated (default field)
| objectId    | String    | Unique id for the user   |
| post  | String   | Post by author    |
| author | Pointer to User | Image author |
| alert (image)   | file   | Image that user activates   |



### Networking
- Home Feed Screen
  - (Read/GET) Query all posts where user is author

    ```
    // (Read/GET) Query all posts where user is author
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
    ```
    
  - (Create/POST) Create a new alert on a post
  
     ```  
     // (Create/POST) Create a new alert on a post
    let myAlert = PFObject(className:"Alert")
    myAlert["content"] = "This is an alert."

    // Add a relation between the Post and Comment
    myAlert["post"] = myPost

    // This will save both myPost and myAlert
    myAlert.saveInBackground()
    
     ```
     
  - (Delete) Delete existing alert

    ```
    // (Delete) Delete existing alert
    PFObject.deleteAll(inBackground: objectArray) { (succeeded, error) in
        if (succeeded) {
            // The array of objects was successfully deleted.
        } else {
            // There was an error. Check the errors localizedDescription.
        }
    }
    ```
    
  - (Create/POST) Create a new comment on a post
     
     ```
     // Create the comment on a post
    let myComment = PFObject(className:"Comment")
    myComment["content"] = "This is a comment."

    // Add a relation between the Post and Comment
    myComment["post"] = myPost

    // This will save both myPost and myComment
    myComment.saveInBackground()
     ```
     
  - (Delete) Delete existing comment
     
     ```
     // (Delete) Delete existing comment
     PFObject.deleteAll(inBackground: objectArray) { (succeeded, error) in
        if (succeeded) {
            // The array of objects was successfully deleted.
        } else {
            // There was an error. Check the errors localizedDescription.
        }
    }
     ```
- Create Post Screen
  - (Create/POST) Create a new post object
 
     ```
     // (Create/POST) Create a new post object
     
    var user = PFUser.currentUser()

    // Make a new post
    var post = PFObject(className:"Post")
    post["title"] = "My New Post"
    post["body"] = "This is some great content."
    post["user"] = user
    post.save()
     
     ```
- Profile Screen
  - (Read/GET) Query logged in user object
  
    ```
    // (Read/GET) Query logged in user object
    PFUser.logInWithUsername(inBackground:"myname", password:"mypass") {
      (user: PFUser?, error: Error?) -> Void in
      if user != nil {
        // Do stuff after successful login.
      } else {
        // The login failed. Check error to see why.
      }
    }
    ```
    
  - (Update/PUT) Update user profile image
  
     ```
     // (Update/PUT) Update user profile image
     
     let query = PFQuery(className:"Image") query.getObjectInBackground(withId: "xWMyZEGZ") { (Image: PFObject?, error: Error?) in
        if let error = error {
            print(error.localizedDescription)
        } else if let Image = Image {
            Image.saveInBackground()
        }
    }
     ```
## Gif Showing Progress of Unit 14 (final gif)
<iframe src="https://giphy.com/embed/ILDJ17JzhFAvIAfeIN" width="222" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/ILDJ17JzhFAvIAfeIN">via GIPHY</a></p>    
         
## Gif Showing Progress of Unit 13
<iframe src="https://giphy.com/embed/Jc8ZWQhD2We36vbkr7" width="480" height="392" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/Jc8ZWQhD2We36vbkr7">via GIPHY</a></p>
     
## Gif Showing Progress of Unit 12     
<iframe src="https://giphy.com/embed/sYKuGrcVeGIKiKp81U" width="215" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/sYKuGrcVeGIKiKp81U">via GIPHY</a></p>


## Gif Showing Progress of Unit 11     
<iframe src="https://giphy.com/embed/pV0CT2wAn5jqj3Cnq6" width="215" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/pV0CT2wAn5jqj3Cnq6">via GIPHY</a></p>     
     

## Gif Showing Progress of Unit 10


<iframe src="https://giphy.com/embed/45atXdX31VIMTeRCQ0" width="232" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/45atXdX31VIMTeRCQ0">via GIPHY</a></p>

