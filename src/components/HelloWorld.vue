<template>
  <div>
    <h1> Hello HTTP Request</h1>

    <label for="Name">Full Name</label><br>
    <input type="text" placeholder="enter your full name" v-model="user.fullname">
     <br>
     <br>
    <label for="email">Email Address</label><br>
    <input type="text" placeholder="enter your email address" v-model="user.email">
    <br>
     <br>
    <button @click="sendData()">Submit</button>
    <br>
     <br>
     <button @click="getUserData()">Get user data</button>
     <div>
      <ul>
        <li v-for="(u, index) in userData" :key="index"> {{ u.fullname }} | {{ u.email }} </li>
      </ul>
     </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      user : {
        fullname: '',
        email: ''
      },
      userData: []
    }
  },
  methods: {
    sendData() {
      this.$http.post("https://http-request-2addb-default-rtdb.europe-west1.firebasedatabase.app/data.json", this.user)
           .then(response => {
            console.log(response);
           })
           .catch(e => {
            console.log(e)
           })
    },
    getUserData() {
      console.log("called")
      this.$http.get("https://http-request-2addb-default-rtdb.europe-west1.firebasedatabase.app/data.json")
      .then((data) =>{
        let newArray = [];
        for(let key in data.body){
          newArray.push(data.body[key])
        }

        this.userData = newArray;
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
