# Sveltefire + Firebase storage

## NOTICE
I *believe* these rules should work.     
`rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{folderName} {
      allow read, write: if request.auth.email == folderName;
    }
  }
}`