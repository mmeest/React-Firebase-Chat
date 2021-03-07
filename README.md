# React-Firebase-Chat
Chat application written in Firebase and React

## About Firebase
Firebase is a platform developed by Google for creating mobile and web applications. It was originally an independent company founded in 2011. In 2014, Google acquired the platform and it is now their flagship offering for app development. 
* Started in 2011
* Created by Firebase Inc

## Create React application
1. On terminal write:
```
npx create-react-app superchat

cd superchat
npm start
```

2. Install 'firebase' and 'react-firebase-hooks'
```
npm install firebase react-firebase-hooks
```

superchat/src/App.js      - where all frontend code is stored

3. Create new project on Firebase console: https://console.firebase.google.com/

4. Go to \
  'Authentication > Sign-in method'\
And enable 'Google'

5. Go to \
  'Cloud Firestore'\
And enable database

6. Klick on the gear symbol and 'Project settings'

7. From embedded code '</>' selector copy api key values to your app initializer:
```
firebase.initializeApp({
  ...
})
```

8. Add section to your app if user is signed in
```
      <section>
        {user ? <ChatRoom /> : <SignIn />}
      </section>
```

9. Add sign in function
```
function SignIn() {
  const signInWithGoogle = () => {
    const provider = new firebase.auth.GoogleAuthProvider();
    auth.signInWithPopup(provider);         // popup window
  }

  return (
    <button onClick={signInWithGoogle}>Sign in with Google</button>
  )
}
```

10. Add sign out button
```
function SignOut() {
  return auht.currentUser && (
    <button onClick={() => auth.signOut()}>Sign Out</button>
  )
}
```

11. Create chatroom function
```
function ChatRoom() {
  const messagesRef = firestore.collection('messages');
  // query documents in a collection:
  const query = messagesRef.orderBy('creditedAt').limit(25);

  // listen to data with a hook
  const [messages] = useCollectionData(query, {idField: 'id'});
}
```

