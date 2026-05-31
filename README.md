# Mjavy
Event Management system 
// Register
function register() {
  const email = document.getElementById("email").value;
  const password = document.getElementById("password").value;

  firebase.auth().createUserWithEmailAndPassword(email, password)
    .then(() => alert("User Registered"))
    .catch(err => alert(err.message));
}

// Login
function login() {
  const email = document.getElementById("email").value;
  const password = document.getElementById("password").value;

  firebase.auth().signInWithEmailAndPassword(email, password)
    .then(() => window.location.href = "dashboard.html")
    .catch(err => alert(err.message));
}
function createEvent() {
  const title = document.getElementById("title").value;
  const date = document.getElementById("date").value;

  firebase.firestore().collection("events").add({
    title: title,
    date: date,
    createdBy: firebase.auth().currentUser.email
  }).then(() => alert("Event Created"));
}
firebase.firestore().collection("events")
  .onSnapshot(snapshot => {
    snapshot.forEach(doc => {
      console.log(doc.data());
      // show event on screen
    });
  });
