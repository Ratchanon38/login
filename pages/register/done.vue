<template>
  <div>
    <v-app-bar
      color="primary"
      dense
      flat
      dark
    >
      <v-toolbar-title>Register</v-toolbar-title>
    </v-app-bar>
    <v-container class="pt-0 pb-0">
      <v-row>
        <v-col cols="12">
          <div class="set-padding">
            <div class="text-center mt-10">
              <img src="~/assets/welcome.jpg" alt="" width="236px">
              <h1 class="text-title">Welcome {{ StudentID }}</h1>
              <p class="mt-7">
                Welcome to the Computer Science,<br/>ยินดีต้อนรับสู่ สาขา วิทยาการคอมพิวเตอร์.<br/> We hope you have a good time here.
              </p>
            </div>
            <v-btn rounded color="primary" dark class="w-100 mt-10 my-btn" @click="Edit">Edit</v-btn>
            <div class="w-100 text-center my-btn outlined text-primary mt-5" @click="close">Close</div>                    
          </div>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
window.onload = function (e) {
      liff.init(function (data) { initializeApp(data); });
    }
    function initializeApp(data) {
      jQuery("#post").click(function () {
        jQuery.post(
          `https://nuxt-login1.firebaseio.com/members/${this.$store.getters.getLine.userId}/profile.json`,
          
          function (responseText) { liff.closeWindow();},
          "html"
        );
      });
    }
export default {  
  data(){
    return {
      StudentID: this.$store.getters.getRegister.StudentID
    }
  },
  methods: {
    Edit() {      
      this.$router.push('/Edit')
    },
      register() {
      if(this.validate()){
        this.$store.dispatch('setregister', this.form)
        this.$axios.patch(`https://nuxt-login1.firebaseio.com/members/${this.$store.getters.getLine.userId}/profile.json`, this.$store.getters.getRegister).then((res) => {
        }).catch(e => console.log(e))         
      }      
    },
    close(){
      liff.closeWindow();
    }
  }
}
</script>
