#java

>[! ] Код на языке `Java`

```java
public class UsersViewModel extends ViewModel {  
    private FirebaseAuth auth;  
    private MutableLiveData<FirebaseUser> user = new MutableLiveData<>();  
    private MutableLiveData<List<User>> users = new MutableLiveData<>();  
    private FirebaseDatabase database;  
    private DatabaseReference usersReference;  
  
    public UsersViewModel() {  
        auth = FirebaseAuth.getInstance();  
        auth.addAuthStateListener(new FirebaseAuth.AuthStateListener() {  
            @Override  
            public void onAuthStateChanged(@NonNull FirebaseAuth firebaseAuth) {  
                user.setValue(firebaseAuth.getCurrentUser());  
            }  
        });  
        database = FirebaseDatabase.getInstance();  
        usersReference = database.getReference("Users");  
  
        usersReference.addValueEventListener(new ValueEventListener() {  
            @Override  
            public void onDataChange(@NonNull DataSnapshot snapshot) {  
                FirebaseUser currentUser = auth.getCurrentUser();  
                if (currentUser == null) {  
                    return;  
                }  
                List<User> usersFromDb = new ArrayList<>();  
                for (DataSnapshot childSnapshot : snapshot.getChildren()) {  
                    User user = childSnapshot.getValue(User.class);  
                    if (user == null) {  
                        return;  
                    }  
                    if (!user.getId().equals(currentUser.getUid())) {  
                        usersFromDb.add(user);  
                    }  
                }  
                users.setValue(usersFromDb);  
            }  
  
            @Override  
            public void onCancelled(@NonNull DatabaseError error) {  
  
            }  
        });  
    }  
  
    public LiveData<FirebaseUser> getUser() {  
        return user;  
    }  
  
    public LiveData<List<User>> getUsers() {  
        return users;  
    }  
  
    public void logout() {  
        auth.signOut();  
    }  
}
```