# Sveltefire + Firebase storage

## NOTICE
1. Use user.uid instead of user.email for folders (that's how it is in this repo but not how it was in the video)
2. I *think* this is how the rules should be    
`rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{folderName}/{allFiles=**} {
      allow read, write: if request.auth.uid == folderName;
    }
  }
}`