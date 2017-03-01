# Firebase-Udacity
Code repository for Udacity's [Firebase in a Weekend: Android](https://www.udacity.com/course/firebase-in-a-weekend-by-google-android--ud0352) course


### Set-Up
A new Firebase project is required. Go to [firebase.google.com](https://firebase.google.com/).

### Realtime Database
#### Data
```
{
    "messages" : {
        "-KdqgvFEYzj3zQEh2W4b" : {
            "name" : "user_1",
            "text" : "hello!"
        },
        "-KdqtFtHUFCnUIfjRK-c" : {
            "name" : "user_2",
            "text" : "hi!"
        }	
    }
}
```
#### Rules
```
{
    "rules": {
        "messages" : {
            // only authenticated users can read and write the messages node
            ".read": "auth != null",
            ".write": "auth != null",
                "$id": {
                    // the read and write rules cascade to the individual messages
                    // messages should have a 'name' and a 'text' key or a 'name' and 'photoUrl' key
                    ".validate": "newData.hasChildren(['name', 'text']) && !newData.hasChildren(['photoUrl']) || newData.hasChildren(['name', 'photoUrl']) && !newData.hasChildren(['text'])"
                } 
          }
    }
}
```
Check out [Firebase Realtime Database Security Documentation](https://firebase.google.com/docs/database/security/) for more information.

### Storage
#### Files
Create a folder called **chat_photos** in the `Storage` dashboard of [Firebase Cosole](https://console.firebase.google.com/).
#### Rules
```
service firebase.storage {
    match /b/friendlychat-c780d.appspot.com/o {
        match /{imageId=**} {
            allow read: if request.auth != null;
            allow write: if request.auth != null && request.resource.size < 3 * 1024 * 1024;
        }
    }
}

```
Check out [Firebase Storage Security Documentation](https://firebase.google.com/docs/storage/security/)
and [Firebase Storage Security Rules Reference](https://firebase.google.com/docs/reference/security/storage/) for more information.

### Authentication
- [Authentication in the Console](https://console.firebase.google.com/): Authenticate and manage users from a variety of providers
- [FirebaseUI-Android](https://github.com/firebase/FirebaseUI-Android) on Github

### Notifications
#### Steps
- Add the gradle dependency for messaging
- Go to the Notifications tab in the Firebase Console
- Create your own message to send as notification
- Send the notification __*__
- See the notification on your Android device

`* Make sure that the app is in the background before sending the notifiaction`


##### Notes on Security _(Realtime Database vs Storage)_
> ------------------------------------------------------------------------------------------------------------------
> Firebase Storage Security rule types: **_`read`, `write`_**
> Firebase Realtime Database rule types: **_`.read`, `.write`, `.validate`_**
> ------------------------------------------------------------------------------------------------------------------
> Firebase Storage Security rules **are not** cascading
> >_A value of true for a parent doesn't cause all children to be true._
>
> Firebase Realtime Database rules **are** cascading for `.read` and `.write`
> >_A value of true for a parent applies all children below the point where the node was declared true._
