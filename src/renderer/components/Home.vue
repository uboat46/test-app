<template>
  <div id="home">
    <!-- Navbar (sit on top) -->
    <div class="w3-top">
      <div class="w3-bar" id="myNavbar">
        <a 
        class="w3-bar-item w3-button w3-hover-black w3-hide-medium w3-hide-large w3-right"  
        @click.prevent="toggleFunction" 
        title="Toggle Navigation Menu">
            <i class="fa fa-bars"></i>
        </a>
        <a class="w3-bar-item w3-button">HOME</a>
        <a class="w3-bar-item w3-button w3-hide-small"><i class="fa fa-user"></i> ABOUT</a>
        <a class="w3-bar-item w3-button w3-hide-small"><i class="fa fa-th"></i> PORTFOLIO</a>
        <a class="w3-bar-item w3-button w3-hide-small"><i class="fa fa-envelope"></i> CONTACT</a>
      </div>

        <!-- Navbar on small screens -->
      <div id="navDemo" class="w3-bar-block w3-white w3-hide w3-hide-large w3-hide-medium">
        <a class="w3-bar-item w3-button" @click.prevent="toggleFunction">ABOUT</a>
        <a class="w3-bar-item w3-button" @click.prevent="toggleFunction">PORTFOLIO</a>
        <a class="w3-bar-item w3-button" @click.prevent="toggleFunction">CONTACT</a>
      </div>
    </div>

    <!-- First Parallax Image with Logo Text -->
    <div class="bgimg-1 w3-display-container w3-opacity-min" id="home">
      <div class="w3-display-middle" style="white-space:nowrap;">
        <span class="w3-center w3-padding-large w3-black w3-xlarge w3-wide w3-animate-opacity">MY <span class="w3-hide-small">DESKTOP</span> APP</span>
      </div>
    </div>

    <!-- First Parallax Image with Logo Text -->
    <div class="w3-row">
      <div class="w3-col w3-center l4 m6 s12" v-for="item in items" :key="item.nombre" :style="{'background-color': item.color}">
          <h1 class="w3-text-black">{{item.nombre}}</h1>
      </div>
    </div>

  </div>
</template>

<script>
  const {shell} = require('electron')

  export default {
    name: 'home',
    data () {
        return {
            items:[{nombre: "lol",color:'red'},{nombre:"lal",color:'blue'},{nombre:"lal",color:'red'},{nombre:"lal",color:'blue'}]
        }
    },
    methods: {
        handleScroll (event) {
            var navbar = document.getElementById("myNavbar");
            if (document.body.scrollTop > 100 || document.documentElement.scrollTop > 100) {
                navbar.className = "w3-bar" + " w3-card-2" + " w3-animate-top" + " w3-white";
            } else {
                navbar.className = navbar.className.replace(" w3-card-2 w3-animate-top w3-white", "");
            }
        },
        toggleFunction () {
            shell.beep();
            var x = document.getElementById("navDemo");
            if (x.className.indexOf("w3-show") == -1) {
                x.className += " w3-show";
            } else {
                x.className = x.className.replace(" w3-show", "");
            }
        }
    },
    created () {
        window.addEventListener('scroll', this.handleScroll);
    },
    destroyed () {
        window.removeEventListener('scroll', this.handleScroll);
    }
  }
</script>

<style>
body,h1,h2,h3,h4,h5,h6 {font-family: "Lato", sans-serif;}
body, html {
    height: 100%;
    color: #fff;
    line-height: 1.8;
}

/* Create a Parallax Effect */
.bgimg-1, .bgimg-2, .bgimg-3 {
    background-attachment: fixed;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
}

/* First image (Logo. Full height) */
.bgimg-1 {
    background-image: url('~@/assets/image.jpg');
    min-height: 500px;
}

/* Second image (Portfolio) */
.bgimg-2 {
    background-image: url("/w3images/parallax2.jpg");
    min-height: 400px;
}

/* Third image (Contact) */
.bgimg-3 {
    background-image: url("/w3images/parallax3.jpg");
    min-height: 400px;
}

.w3-wide {letter-spacing: 10px;}
.w3-hover-opacity {cursor: pointer;}

/* Turn off parallax scrolling for tablets and phones */
@media only screen and (max-device-width: 1024px) {
    .bgimg-1, .bgimg-2, .bgimg-3 {
        background-attachment: scroll;
    }
}
</style>
