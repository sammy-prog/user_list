<template>
  <div class="home">
    <div class="home__container">
      <div class="home__container__sidebar">
        <router-link to="/" class="home__container__sidebar--link"><h4>Logopsium</h4></router-link>
        <hr>
        <h2>MENU ELEMENT</h2>
        <hr>
        <h2>MENU ELEMENT</h2>
        <hr>
        <h2>MENU ELEMENT</h2>
        <hr>
        <div style="margin-top: 25vh">
          <a style="cursor:pointer" @click.prevent="logout" class="home__container__sidebar--link">
            &lt;-] Admin
          </a>
        </div>
      </div>
      <div class="home__container__content">
        <h1 style="margin-left: 1vw;font-size: 40px">Users</h1>
        <div class="home__container__content__grid">
          <div @click="modal = true; currentUser = user" class="home__container__content__grid--image" v-for="user in users" :key="user.id">
            <img :src="user.image" alt="">
            <div class="home__container__content__grid--overlay">
              <div class="home__container__content__grid--overlay--text">{{user.name}}</div>
              <div style="margin-top:30px" class="home__container__content__grid--overlay--text">{{user.address.city}}</div>
            </div>
          </div>
        </div> 
         <div id="myModal" class="modal" v-if="modal">
              <div class="modal-content">
                <span @click.stop="modal = false; currentUser = {}" class="close">&times;</span>
                <img :src="currentUser.image" alt="" style="float:left; width:30%;margin-right:40px">
                <div class="modal__text" style="margin-top:30px;color:black">
                   <h3>{{currentUser.name}}</h3>
                   <a style="text-decoration: none !important; color: black !important" :href="getMailLink(currentUser)"><h3>{{currentUser.email}}</h3></a>
                   <h3>{{currentUser.phone}}</h3>
                   <h3>{{currentUser.address.city}}, {{currentUser.address.street}}</h3>
                   <h3>{{currentUser.website}}</h3>
                </div>
               
              </div>
            </div> 
      </div>
    </div>
  </div>
</template>

<script>

var json = require('../api/users.json'); 

export default {
  name: 'HomeView',
  data() {
    return {
      users: [],
      modal: false,
      currentUser: {}
    }
  },
  mounted() {
    fetch("/api/users")
      .then(this.users = json)
      .catch(this.users = json)
      
  },
  methods: {
    getMailLink(user) {
      let mailLnk = ''
      mailLnk = `mailto:${user.email}?subject=We%20are%20hiring!&body=Hello,%20${user.name}`
      return mailLnk
    },
    logout() {
      localStorage.setItem('isUserAuthenticated', false);
      this.$router.push('/login');
    }
  }
}
</script>

<style>
* {
  margin: 0;
  overflow-x: hidden;
}
.home__container {
  display: flex;
}
.home__container__sidebar {
  background-color: rgb(233, 233, 233);
  min-height: 100vh;
  padding: 20px;
  display: block;
}
.home__container__sidebar h2{
  margin-top: 40px;
  cursor: pointer;
}
.home__container__sidebar hr{
  margin-top: 30px;
}
.home__container__sidebar--link {
  text-decoration: none !important;
  color: black !important;
}
.home__container__content {
  width: 80%;
  margin: auto;
  margin-top: 10vh;
}
.home__container__content__grid {
  display: grid;
  grid-template-columns: auto auto auto auto;
  column-gap: 50px;
  row-gap: 50px;
  padding: 10px;
  margin-top: 30px;
}
.home__container__content__grid img{
  width: 15vw;
  height: 20vw;
  border-radius: 20px;
}
.home__container__content__grid--image{
  position: relative;
  width: 15vw;
  border-radius: 20px;
  height: 20vw;
  overflow: hidden;
}
.home__container__content__grid--overlay {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  width: 15vw;
  opacity: 0;
  transition: .5s ease;
  background-color: #000000;
  border-radius: 20px;
}

.home__container__content__grid--image:hover .home__container__content__grid--overlay {
  opacity: 0.75;
}

.home__container__content__grid--overlay--text {
  color: white;
  font-size: 20px;
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  text-align: center;
}


.modal {
  position: fixed; 
  z-index: 1;
  padding-top: 100px;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgb(0,0,0);
  background-color: rgba(0,0,0,0.7);
}

.modal-content {
  background-color: #fefefe;
  margin: auto;
  border: 1px solid #888;
  width: 50%;
}

.close {
  color: #363636;
  float: right;
  font-size: 38px;
  font-weight: bold;
  margin-top: 3px;
  margin-right: 10px;
}
.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
}
.modal__text h3{
  margin-top: 12px;
}
@media only screen and (max-width: 1000px) {
  .home__container__content__grid {
    display: grid;
    grid-template-columns: auto auto;
  }
  .home__container__content__grid img{
    width: 30vw;
    height: 30vw;
  }
  .home__container__content__grid--image{
    width: 30vw;
    height: 30vw;
  }
  .home__container__content__grid--overlay {
    width: 30vw;
  }
  .modal-content {
    width: 80%;
  }
}
@media only screen and (max-width: 700px) {
  .home__container__content__grid img{
    width: 70vw;
    height: 70vw;
  }
  .home__container__content__grid--image{
    width: 70vw;
    height: 70vw;
    margin-top: 30px;
  }
  .home__container__content__grid--overlay {
    width: 70vw;
  }
  .home__container__content__grid {
    display: block;
    margin-top: -25px;
  }
  .home__container__sidebar {
    display: none;
  }
  .home__container__content{
    margin-top: 2vh;
  }
  
}

</style>