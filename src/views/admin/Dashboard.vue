<template>
  <div class="dashboard">
    <!--Top Navbar start-->
    <div class="dashboard-navbar">
      <nav class="navbar navbar-expand-lg navbar-light bg-light dashboard-bar">
        <div class="container-fluid">
          <div class="navbar-brand left-part">TIC ADMIN</div>
        </div>
      </nav>
    </div>
    <!--Top Navbar end-->
    <!--Dashboard sidebar start-->
    <div class="dashboard-sidebar">
      <aside class="sidebar">
        <div class="sidebar-div" style="position: relative; overflow: visible; width: auto; height: 100%;">
          <div class="sidebar-scrollbar" style="overflow: hidden; width: auto; height: 100%;">
            <div class="user-profile">
              <div class="profile-image">
                <img :src="profile.url" class="profile-img"/>
              </div>
              <p class="profile-text">{{profile.username}}</p>
            </div>
            <Sidebar/>
          </div>
        </div>
      </aside>
    </div>
    <!--Dashboard sidebar end-->
    <!--Dashboard container start-->
    <div class="page-wrapper" style="min-height: 363px;">
      <router-view/>
    </div>
  </div>
</template>

<script>
import Sidebar from '@/components/Sidebar'
import api from '@/utils/api'
export default {
  name: 'Dashboard',
  components: {Sidebar},
  data () {
    return {
      profile: {}
    }
  },
  mounted: async function () {
    this.profile = (await api.info()).data
    // eslint-disable-next-line no-undef
    this.profile.url = 'https://cdn.v2ex.com/gravatar/' + md5(this.profile.email) + '?s=128'
  }
}
</script>

<style scoped>
  .left-part:hover {
    color: white;

  }

  .dashboard-bar {
    background: linear-gradient(to right,#0078bc 1%,#00beda 100%);
  }

  .left-part {
    color: white;
  }

  .sidebar {
    z-index: 10;
    position: absolute;
    width: 265px;
    padding-top: 57px;
    height: 100%;
    top: 0;
    overflow-y: auto;
    background: #fff;
  }

  .profile-img {
    width: 7vw;
    height: 7vw;
    border-radius: 50%;
    border: solid 0.5px;
    border-color: #d6d3d3;
  }

  .profile-text {
    font-weight: bold;
    color: cornflowerblue;
    margin-top: 1vw;
  }

  .user-profile {
    margin: 1vw auto;
  }

  .page-wrapper {
    background: #f4f8f9;
    padding-bottom: 15px;
  }

  .navbar {
     z-index: 1000;
   }

  .page-top {
    padding-top: 1.5vw;
  }

  @media (min-width: 1024px){
    .page-wrapper {
      margin-left: 265px;
    }
  }
</style>
