<template>
  <div class="dark-mode-widget">
    <input type="checkbox" id="theme-toggle" @click="toggleDarkTheme">
    <label for="theme-toggle"><span></span></label>
  </div>
</template>
<script>
  export default {
    mounted() {
      this.checkUserPreference();
    },
    methods: {
      toggleDarkTheme() {
        const body = document.body;
        body.classList.toggle("dark-mode");
            //If dark mode is selected
            if (body.classList.contains("dark-mode")) {
                //Save user preference in storage
                localStorage.setItem("dark-theme", "true");
                //If light mode is selected
              } else {
                body.classList.remove("dark-mode");
                setTimeout(function() {
                  localStorage.removeItem("dark-theme");
                }, 100);
              }
            },
            checkUserPreference() {
            //Check Storage on Page load. Keep user preference through sessions
            if (localStorage.getItem("dark-theme")) {
              document.body.classList.add("dark-mode");
              document.getElementById('theme-toggle').checked = true;
            }
          }
        }
      };
    </script>
    <style>
      .dark-mode-widget {
        /*display: table;*/
        display:  flex;
        flex-direction: row-reverse;
        margin: .6em auto;
      }

      body.dark-mode {
        background: #22272d;
        color: #adbac7;
      }

      body.dark-mode h1,
      body.dark-mode h2,
      body.dark-mode h3,
      body.dark-mode p,
      body.dark-mode a {
        color: #adbac7;
      }

      #theme-toggle {
        display: none;
      }

      #theme-toggle+label {
        font-size: .6rem;
        display: flex;
        width: 4em;
        border-radius: 2em;
        background-position: bottom;
        background-color: #242625;
        /*background-size: auto 8em;*/
        /*background-image: linear-gradient(180deg, #021037 0%, #20206A 19%, #4184B1 66%, #62E7F7 100%);*/
        transition: .2s;
        border: 0.125em solid #242625;
        overflow: hidden;
      }

      #theme-toggle+label span {
        background: #fffad8;
        border-radius: 50%;
        height: 2em;
        width: 2em;
        transform: translateX(-.125em) scale(.65);
        transition: .2s;
        cursor: pointer;
      }

      #theme-toggle:checked {
        font-size: 10rem;
      }

      #theme-toggle:checked+label {
        background-position: top;
        border-color: #adbac7;
      }

      #theme-toggle:checked+label span {
        background: transparent;
        transform: translateX(calc(100%)) scale(.65);
        box-shadow: inset -.1875em -.1875em 0 0 #fbe7ef, inset -.5625em -.5625em 0 0 #fffff7;
      }
    </style>
