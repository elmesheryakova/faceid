<template>
  <div class="Authentication">
    <h1>Face recognition with FaceIO</h1>
    <div class='container'>
    <div @click='login' class='btn' v-if="user === ''">Sign in</div>
    <div class='btn' @click='register' v-if="user === ''">Register</div>
    <div class='btn' @click='logout'  v-if="user != ''">Log out</div>
    </div>
  </div>
</template>
<script>
export default {
  data(){
   return {
    user:''
   }
  },
  methods: {
    register(){
      window.faceio.enroll({
        "locale": "auto", 
        "payload": {
          "whoami": 123456,
          "email": "john.doe@example.com"
        }
      }).then(userInfo => {
          // User Successfully Enrolled! 
          alert(
              `User Successfully Enrolled! Details:
            Unique Facial ID: ${userInfo.facialId}
            Enrollment Date: ${userInfo.timestamp}
            Gender: ${userInfo.details.gender}
            Age Approximation: ${userInfo.details.age}`
          );
        console.log(userInfo);
        // handle success, save the facial ID (userInfo.facialId), redirect to the dashboard...
      }).catch(errCode => {
        // Something went wrong during enrollment, log the failure
        console.log(errCode);
      })
    },
    logout(){
      this.user=''
    },
    login(){
      window.faceio.authenticate({
          "locale": "auto" // Default user locale
      }).then(userData => {
          console.log("Success, user identified")
          console.log("Linked facial Id: " + userData.facialId)
          console.log("Payload: " + JSON.stringify(userData.payload)) // {"whoami": 123456, "email": "john.doe@example.com"} from the enroll() example above
          this.user=userData.payload.whoami
      }).catch(errCode => {
          console.log(errCode)
      })
    }
  }
}
</script>
<style scoped>
.container{
  width:90%;
  margin:20px auto;
  display:flex;
  justify-content:space-around;
  align-items:center;
  padding:1em;
}
.btn{
  border:1px solid black;
  border-radius:5px;
  padding:1em 2em;
}
.btn:hover{
  background:#000;
  color:#fff
}
</style>


