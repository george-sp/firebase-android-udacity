# Firebase-Udacity
Code repository for Udacity's [Firebase in a Weekend: Android](https://www.udacity.com/course/firebase-in-a-weekend-by-google-android--ud0352) course


### Set-Up
A new Firebase project is required. Go to [firebase.google.com](https://firebase.google.com/).

#### Rules
```
{
  "rules": {
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
```
