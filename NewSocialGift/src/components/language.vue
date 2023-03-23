<template>
  <section id="LanguageSection">
    <nav>
      <ol id="LanguageList">
        <li>
          <img id="switchImg" src="../components/icons/ds.png" />
        </li>
        <li id="switchLi">
          <label class="switch">
            <input type="checkbox" />
            <span class="slider"></span>
          </label>
        </li>
        <li>
          <select name="select" id="LanguageSelect">
            <option value="value1" selected>Spanish</option>
            <option value="value2">English</option>
          </select>
        </li>
      </ol>
    </nav>
  </section>
</template>

<style scoped>
@import '../assets/language.css';
</style>
