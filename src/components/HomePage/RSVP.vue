<template>
  <form id="rsvp-form" ref="rsvpForm" @submit.prevent="saveEmail">
    <input type="text" class="squad" v-model="fakeEmail">
    <label for="email">Enter Your Email to RSVP</label>
    <input required type="email" autocomplete="off" v-model="trueEmail" id="email">
    <app-round-btn @click="saveEmail" class="submit" :link="false">
      <span class="material-icons">send</span>
    </app-round-btn>
  </form>

  <AppAlert @click="dismiss" v-if="showAlert">{{message}}</AppAlert>

</template>

<script>
import RoundButton from "@/components/utils/RoundButton";
// import db from "@/firebaseInit";
import Alert from "@/components/utils/Alert";

export default {
name: "RSVP",
  components:{
    AppRoundBtn: RoundButton,
    AppAlert:Alert,
  },
  emits:{
    rsvp:false
  },
  data(){
    return{
      fakeEmail:'',
      trueEmail:'',
      showAlert:false,
      message:''
    }
  },
  methods:{
    dismiss(){
      this.showAlert = false
      this.message = ''
    },
    saveEmail(){
      // console.log('akskk')
      // if(this.fakeEmail === "" && this.validEmail(this.trueEmail)){
      //   db.collection("emails_collections").add({
      //     email:this.trueEmail,
      //     mail_sent:false
      //   }).then(()=>{
      //     // console.log(res.id)
      //     this.$refs.rsvpForm.reset()
      //     localStorage.setItem('RSVP',true.toString())
      //     this.$emit('rsvp',true)
      //   })
      // } else {
      //   this.message = "Oops!! Error"
      //   this.showAlert = true
      // }
      if (this.fakeEmail === '' && this.validEmail(this.trueEmail)){
        this.$router.push({name:'Register', query:{email:this.trueEmail}})
      } else {
        this.showAlert = true
        this.message = 'Email Error!!'
      }

    },
    validEmail: function (email) {
      let re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
    }
  }
}
</script>

<style scoped>

.squad{
  display: none;
}

form{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
}
  label{
    margin: 25px auto;
    color: var(--color-frontEnd);
    font-size: 25px;
  }

  input{
    width: min(600px, 70%);
    padding: 15px 25px;
    color: var(--color-frontEnd);
    font-size: 20px;
    height: 60px;
    border-radius: 50px;
    outline: none;
    background: var(--bg-frontEnd);
    border: none;
    box-shadow: 7px 7px 15px rgb(17, 122, 9), -7px -7px 15px rgba(223, 223, 223, .15);
  }

  input:focus{
    transition: none;
    box-shadow: none;
    border:2px solid #aaa;
  }

  .submit{
    margin: 25px;
  }

  .material-icons {
    font-size: 20px;
  }

@media screen and (max-width: 1400px){
  input{
    padding: 10px;
    height: 50px;
    font-size: 17px;
  }
}

  @media only screen and (max-width: 700px) {
    .material-icons {
      font-size: 16px;
    }

    label{
      margin: 20px 25px;
      font-size: 18px;
    }

    input{
      height: 45px;
      font-size: 15px;
    }
  }

</style>

























