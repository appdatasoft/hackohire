<template>
  <b-navbar toggleable="md" type="dark">
    <b-navbar-toggle target="nav_collapse"/>
    <b-navbar-brand to="/"><img src="" srcset="../assets/hohlogo.png 1x, ../assets/hohlogo.png 2x" width= "20%" alt="hackohire for happy teams"></b-navbar-brand>
    <b-navbar-nav>
    <div v-if="!signedIn">
      <b-nav-item to="/signIn">Login</b-nav-item>
      </div>
      <div v-if="signedIn">
      <amplify-sign-out></amplify-sign-out> 
      </div>
      <!-- <b-nav-item to="/pricing">Jobs</b-nav-item>-->
      <!--<b-nav-item to="/pricing">Interviews</b-nav-item>-->
      <!--<b-nav-item to="/pricing">Events</b-nav-item>-->
      <!--<b-nav-item to="/pricing">Podcast</b-nav-item>-->
    </b-navbar-nav> 
  </b-navbar>    
</template>

<script>
import { AmplifyEventBus } from 'aws-amplify-vue'
import { Auth, API, graphqlOperation } from 'aws-amplify'
import 'vue-awesome/icons/user-circle'
import 'vue-awesome/icons/sign-out'
import 'vue-awesome/icons/github'
import 'vue-awesome/icons/twitter'

export default {
    name: 'Navbar',
    async beforeCreate() {
    try {
      const user = await Auth.currentAuthenticatedUser()
      this.signedIn = true
    } catch (err) {
      this.signedIn = false
    }
    AmplifyEventBus.$on('authState', info => {
      if (info === 'signedIn') {
        this.signedIn = true
      } else {
        this.signedIn = false
      }
    });
  },
  data () {
    return {
      signedIn: false
    }
  },
    methods: {
        signIn() {
            this.$store.dispatch('signIn')
        }
    }
}
</script>
<link src='../vendor/bootstrap/css/bootstrap.min.css'/>
<link src='../vendor/simple-line-icons/css/simple-line-icons.css'/>
<link src='../vendor/bootstrap/css/bootstrap.min.css'/>
<link src='../device-mockups/device-mockups.min.css'/>
<link src='../css/lato.css'/>
<link src='../css/multi.css'/>
<link src='../css/cataraman.css'/>
<link src='../css/new-age.min.css'/>
<style scoped>
@import '~bootstrap/dist/css/bootstrap.css';
@import '~bootstrap-vue/dist/bootstrap-vue.css';
body {
  margin: 0
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.container {
  padding: 40px;
}
.signout {
  background-color: #ededed;
  margin: 0;
  padding: 11px 0px 1px;
}
.main{
  margin: 0;
  padding: 0;
}

.fa-icon {
    top: .125em;
    position: relative;
}

.b-main-content {
  padding-top: 1.5rem;
  padding-bottom: 1.5rem;
  margin-right: 0;
  margin-left: 0;
}

.b-form-1 {
  padding-top: 1.5rem;
  padding-bottom: 1.5rem;
  margin-right: 0;
  margin-left: 0;
  border-width: .2rem;
}

.navbar {
    background-color: #563d7c;
}
.navbar-nav .nav-link {
    color: #cbbde2;
}
.nav-username {
  color: white;
  padding-left: .5em;
  padding-right: .5em;
}
</style>
