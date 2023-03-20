<template>
    <body>
        
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
      

      <section id="GeneralSection">
        <div class="navigation">
        <ul>
            <li>
              <a href=""> <img src="../../img/logo.png" id="logoNavBar" alt=""></a>
            </li>
            <li>
            <a href=""><i class="fa-solid fa-house"></i> Home</a>
            </li>
            <li>
              <a href=""><i class="fa-solid fa-magnifying-glass"></i> Search</a>
            </li>
            <li>
              <a href=""><i class="fa-solid fa-envelope"></i> Messages</a>
            </li>
            <li>
              <a href=""><i class="fa-sharp fa-solid fa-bell"></i> Notifications</a>
            </li>
            <li>
              <a href=""><i class="fa-solid fa-pen-to-square"></i> Create</a>
            </li>
            <li id ="MoreLi">
              <a href="" onclick="openForm()"><i class="fa-solid fa-bars"></i> More</a>
            </li>
        </ul>
        </div>
        <div id="chat-profiles">
            <div>
                <img class="iconocrear" src="../../img/Crear.png">
            </div>
            <div id="list-profiles">
                <ul>
                    <li><a><img>NickName</a></li>
                    <li><a><img>NickName</a></li>
                    <li><a><img>NickName</a></li>
                    <li><a><img>NickName</a></li>
                </ul>
            </div>
            <div>

            </div>
        </div>
        <div class="chat-section">
            <div class="listheader">
                <img class="profileimglist" src="../../img/DefaultProfilePhoto.png">
                <h3>NickName</h3>
                <a href="#"><i id="moreimg" class="fa-solid fa-info" style="color: #000000;"></i></a>
            </div>
            <div id="chatdiv">
                
            </div>
        </div>
      </section>

    </body>
  </template>

<style scoped src="../assets/ChatStyle.css"></style>

  