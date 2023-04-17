<template>
  <section id="LanguageSection">
    <nav><!-- BORRAR -->
      <ol id="LanguageList">
        <li>
          <img id="switchImg" src="src/components/icons/CurrentWhite.png" />
        </li>
        <li id="switchLi">
          <label class="switch">
            <input type="checkbox" id="toggleSwitch" @click="toggleImage()"/>
            <span class="slider"></span>
          </label>
        </li>
        <li>
          <select name="select" id="LanguageSelect">
            <option value="value1" selected>Spanish</option>
            <option value="value2">English</option>
          </select>
        </li>
        <li id="hamburguerMenu" v-if="showHamburguerMenu"><a href="#" ><i class="fa-solid fa-bars"></i></a></li>
      </ol>
    </nav>
  </section>
</template>

<!-- CHAT GPT-->
<script>
export default {
  name: 'Language',
  props: {
    showHamburguerMenu: {
      type: Boolean,
      default: true
    }
  },
  methods: {
    toggleImage() {
      var img = document.getElementById("switchImg");
      if (img.src.match("CurrentWhite.png")) {
        img.src = "src/components/icons/CurrentDark.png";
        document.body.style.backgroundColor = "Black";
      } else {
        img.src = "src/components/icons/CurrentWhite.png";
        document.body.style.backgroundColor = "White";
      }
    }
  }
}
</script>

<style scoped>
@import '../assets/language.css';
</style>

<style>

  @media screen and (max-width: 600px) {
    #hamburguerMenu a{
      text-decoration: none;
      color: black;
    }

    #hamburguerMenu i{
      display: block !important;
      font-size: 40px!important;
  }

    .NavBar {
    display: none !important;
  }

  .NavBar--show {
    display: block !important;
  }
    
  }

</style>
