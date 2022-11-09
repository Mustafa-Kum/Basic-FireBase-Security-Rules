## FireBase Rules

rules_version = '2';

service cloud.firestore {
  
  match /database/{database}/documents {
  
    match /{document=**} {
      
      allow read;
      
      allow write: if isSignedIn();
      
      allow update: if isSignedIn() && isOwner(<parametreID>);
      
      allow delete: if isSignedIn();
    
    }
    
    function isSignedIn(){
      
      return request.auth !=null
    
    }
    
    function isOwner(<paramatre>){
      
      return request.auth.uid == <parametre>
    
    }
  
  }

}
