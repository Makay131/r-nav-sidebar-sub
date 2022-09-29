<template>
  <div class="open-btn" @click="handleClickForOpen" v-show="!isActive">
    <box-icon color="white" name='menu-alt-left'></box-icon>
  </div>
  <div :class="{sidebar: true, active: isActive}">
    <div class="close-btn" @click="handleClickForClose">
      <box-icon color="white" name='x' animation="flashing-hover"></box-icon>
    </div>
    <div class="menu">
      <div class="item"><a href="#"><box-icon color="white" name='home'></box-icon> Home</a></div>
      <div class="item" id="messages" @click="handleClickForSubMenu">
        <a href="#" class="sub-btn"><box-icon color="white" name='message-dots'></box-icon> Messages <box-icon v-if="!isArrowOne" color="white" name='chevron-right' id="dropdown-arrow"></box-icon><box-icon v-if="isArrowOne" color="white" name='chevron-down' id="dropdown-arrow"></box-icon></a>
        <div class="sub-menu">
          <a href="#" class="sub-item">Private</a>
          <a href="#" class="sub-item">Friends</a>
          <a href="#" class="sub-item">Channel-1</a>
        </div>
      </div>
      <div class="item"><a href="#"><box-icon color="white" name='user-pin'></box-icon> Profile</a></div>
      <div class="item"><a href="#"><box-icon type="solid" color="white" name='dashboard'></box-icon> Dashboard</a></div>
      <div class="item" id="settings" @click="handleClickForSubMenu">
        <a href="#" class="sub-btn"><box-icon color="white" name='cog'></box-icon> Settings <box-icon v-if="!isArrowTwo" color="white" name='chevron-right' id="dropdown-arrow"></box-icon><box-icon v-if="isArrowTwo" color="white" name='chevron-down' id="dropdown-arrow"></box-icon></a>
        <div class="sub-menu">
          <a href="#" class="sub-item">Accessibility</a>
          <a href="#" class="sub-item">General</a>
        </div>
      </div>
      <div class="item"><a href="#"><box-icon color="white" name='log-out'></box-icon> Logout</a></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Navbar',
  data() {
    return {
      isActive: false,
      isArrowOne: false,
      isArrowTwo: false,
    }
  },
  created() {
    document.body.classList.add('body')
  },
  methods: {
    handleClickForSubMenu(e) {
      e.path.forEach(el => {
        if(el.id?.includes('messages')) {
          el.classList.toggle('active');
          this.isArrowOne = !this.isArrowOne;
        }
        if(el.id?.includes('settings'))
        el.classList.toggle('active');
          this.isArrowTwo = !this.isArrowTwo;
      });
    },
    handleClickForClose() {
      this.isActive = false;
    },
    handleClickForOpen() {
      this.isActive = true;
    },
  }
}
</script>


<style>
  .body {
  background: url(../assets/bg.jpg) no-repeat;
  background-size: cover;
  background-position: center;
  min-height: 100vh;
  min-width: 100vw;
  }

  .sidebar {
    position: fixed;
    top: 0;
    left: 0;
    height: 100vh;
    width: 0px;
    overflow-y: auto;
    overflow-x: hidden;
    position: relative;

    background: rgba(255,255,255, .1);
    backdrop-filter: blur(8px);
    transition: width .4s ease;
  }

  .sidebar.active {
    width: 250px;
  }

  .sidebar .menu {
    width: 100%;
    margin-top: 60px;
    white-space: nowrap;
  }

  .sidebar .menu .item {
    width: 100%;
    cursor: pointer;
    list-style: none;
  }
  .sidebar .menu .item a {
    font-size: 1.2rem;
    color: #fff;
    text-decoration: none;
    padding: 5px 30px;
    line-height: 60px;
    display: block;
    border-top-left-radius: 5px;
    border-bottom-left-radius: 5px;
  }
  .sidebar .menu .item a:hover {
    background: #087f5b;
    transition: .4s ease;
  }

  .sidebar .menu .item a box-icon:nth-child(1) {
    margin-right: 10px;
    line-height: 70px;
    transform: translateY(5px);
  }

  .sub-item {
    display: block;
  }

  .sidebar .menu .item a #dropdown-arrow {
    position: absolute;
    right: 0;
    transform: translate(-10px, 10px);
  }
  .sidebar .menu .item .sub-menu {
    max-height: 0;
    visibility: hidden;
    opacity: 0;
    transition: all .5s cubic-bezier(.05,.56,.76,.92);
  }

  .sidebar .menu .item .sub-menu a {
    background: rgba(255,255,255, .1);
    padding-left: 40px;
    font-size: 1rem;
  }
  .sidebar .menu .item .sub-menu a:hover {
    background: rgba(8, 127, 91, 0.643);
  }

  .sidebar .menu .item.active .sub-menu {
    max-height: 400px;
    visibility: visible;
    opacity: 1;
  }

  .close-btn {
    position: absolute;
    top: 10px;
    right: 10px;
    border: 1px solid transparent;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;

    transition: all .4s ease;
  }
  .close-btn:hover {
    border: 1px solid rgba(8, 127, 91, 0.281);
  }

  .open-btn {
    font-size: 1.8rem;
    position: absolute;
    top: 10px;
    left: 20px;
    padding: 10px;
    cursor: pointer;
  }
</style>
