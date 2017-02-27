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
Check out [Database Security Rules documentation](https://firebase.google.com/docs/database/security/) for more information.

### Storage
#### Files
Create a folder called **chat_photos** in the `Storage` dashboard of [Firebase Cosole](https://console.firebase.google.com/).

### Authentication
- [Authentication in the Console](https://console.firebase.google.com/): Authenticate and manage users from a variety of providers
- [FirebaseUI-Android](https://github.com/firebase/FirebaseUI-Android) on Github