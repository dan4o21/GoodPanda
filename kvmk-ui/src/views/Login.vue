<template>
  <div class="container">
    <div class="row">
      <div class="col-lg-3 col-md-2"></div>
      <div class="col-lg-6 col-md-8 login-box">
        <div class="col-lg-12 login-key">
          <i class="fa fa-key" aria-hidden="true"></i>
        </div>
        <div class="col-lg-12 login-title">

        </div>

        <div class="col-lg-12 login-form">
          <div class="col-lg-12 login-form">
            <form>
              <div class="form-group">
                <label class="form-control-label">
                  USERNAME
                </label>
                <input type="text" v-model="email" class="form-control">
              </div>
              <div class="form-group">
                <label class="form-control-label">PASSWORD</label>
                <input type="password" v-model="password" class="form-control">
              </div>

              <div class="col-lg-12 loginbttm">
                <div class="col-lg-6 login-btm login-text">
                  <!-- Error Message -->
                </div>
                <div class="col-lg-6 login-btm login-button">
                  <button type="submit" v-on:click="login" class="btn btn-outline-primary">LOGIN</button>
                </div>
              </div>
            </form>
          </div>
        </div>
        <div class="col-lg-3 col-md-2"></div>
      </div>
    </div>
    </div>
 </template>

<script>

/*
import UsersService from "@/services/users-service";*/
import RecipeService from '../services/recipe-service'
import isLogged from "@/utils/Auth";
export default {
  name: 'Login',
  data() {
    return {
      email: "",
      password: "",

   }
  },
  methods: {
    login(e)
    {
      console.log("loginclicked");
      e.preventDefault() //prevent refreshing the page



      const  form = {
        email: this.email,
        password: this.password,
      }
      RecipeService.login(form).then(
          response =>
          {
            if(response === "login_success")
            {
              this.$cookies.set("isLogged","true");
              console.log(response);
              this.$router.push({
                name: "Home"

              })
            }
             else {
               console.log("unsuccessful login")
            }
          }

      )

    },
    mounted: function() {
      document.cookie = "username=John Doe";
    },


    register(e) {

      e.preventDefault()
      const form = {
        name: this.name,
        email: this.email,
        password: this.password,

      }
      RecipeService.register(form).then(
          response => {
            this.name = "";
            this.email = "";
            this.password = "";
          },
      )
    }
  }
}
</script>

