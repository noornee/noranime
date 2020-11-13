<template>
  <div class="container">
        <header id="header-container">
            <h2>Welcome to noranime</h2>
        </header>    
    <section class="grid">
      <div class="grid__container">
        <div
          class="grid__item"
          v-for="data in anime_data['anime_list']"
          :key="data.id"
        >
          <NuxtLink :to="data['slug']">
            <div class="grid__img">
              <span class="text-content"> {{ data["title"] }} </span>
              <img
                :src="data['image_url']"
                :alt="data['title']"
                :title="data['title']"
              />
            </div>
          </NuxtLink>
        </div>
      </div>
    </section>
    <div class="btns">
  <button @click="about_us()">About us</button>
  <button @click="disclaimer()">Disclaimer</button>
    </div>

    <footer>
<div id="about-us">
  <h3>About us: </h3>
  <p>
    this site is more like my personal anime website. it basically contains some of the anime on my watchlist.
    yeah i know, its probably useless to some people but its quite useful to me cos i dont have to go to a site that keeps redirecting me anytime i wanna download an anime 😅...

  </p>
</div>

<div id="disclaimer">
  <h3>Disclaimer :</h3>
  <p>
    <b>This site does not host any of these files on its server. All files or contents are hosted on these third party websites</b> [<a href="https://animelist.pw">animelist.pw</a> and <a href="http://takanimelist.live/">takanimelist.live</a>]. i'm merely providing the index
  </p>
</div>
    </footer>

  </div>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    const api = "https://norapi.herokuapp.com/";
    const anime_data = await $axios.$get(api);
    return { anime_data };
  },
  data() {},
  methods: {
    about_us: function(){
     let x = document.getElementById('about-us');
     if (x.style.display === 'none'){
       x.style.display = 'block'
     }else {
       x.style.display = 'none'
     }
    },
    disclaimer: function(){
     let x = document.getElementById('disclaimer');
     if (x.style.display === 'none'){
       x.style.display = 'block'
     }else {
       x.style.display = 'none'
     }
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
@import url("https://fonts.googleapis.com/css?family=Cutive");
@import url("https://fontlibrary.org/face/waltograph");




* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

*:before,
*:after {
  box-sizing: border-box;
}

#header-container {
    width: 90vw;
    height: 10vh;
    margin: 20px auto;
    background: crimson;
    display: flex;
    justify-content: center;
    align-items: center;

}

#header-container h2 {
    color: greenyellow;
    font-variant: small-caps;
    font-family: 'Press Start 2P', cursive;
}

img {
  max-width: 100%;
  display: block;
}

.grid {
  margin: 2rem auto;
}

.grid__container {
  display: grid;
  background-color: #000;
  border: 1px solid #000;
  grid-gap: 1px;
  justify-self: center;
  max-width: 400px;
  height: auto;
  margin: 0 auto;
}

.grid__item {
  position: relative;
}



.grid__img {
  position: relative;
  /* pointer-events: none; */
  border: 10px solid black;
  overflow: hidden;
}

.grid__item img {
  object-fit: cover;
  transition: all 1s;
}

.grid__item:hover img {
  transform: scale(2) rotate(10deg);
  filter: blur(2px);
}

span.text-content {
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(0, 0, 0, 0.5);
  color: white;
  height: 100%;
  width: 100%;
  text-align: center;
  opacity: 0;
  position: absolute;

}

.grid__item:hover span.text-content {
  opacity: 1;
  z-index: 100;
  text-transform: capitalize;
  font-weight: bold;
  font-size: 1.2em;
  color: white;
  letter-spacing: 1px;
  font-family: 'Cutive';

}
 /* footer */
div.btns {
  display: flex;
  justify-content: center;
}

button {
  padding: 5px;
  margin-right: 5px;
  text-align: center;
  font-size: 25px;
  font-family: 'waltograph';
  cursor: pointer;
}

button:hover {
  background: green;
  color: white;
  border: none;
}

div#disclaimer {
border: 2px solid greenyellow;
display: none;
width: 50%;
}

div#about-us {
border: 2px solid crimson;
display: none;
width: 50%;
}

footer{
  width: 90vw;
  margin: 0 auto;
  display: flex;
  text-align: center;
  flex-wrap: wrap;
  font-variant:small-caps;
  letter-spacing: 2px;
  font-family: 'Cutive', cursive;
  font-weight: bold;

}

div#disclaimer a {
  color: white;
  background: green;
}

div#disclaimer a:hover {
  background: red;
}



@media only screen and (min-width: 768px) {
  .grid__container {
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: repeat(4, 1fr);
    max-width: 583px;
  }
}

@media only screen and (min-width: 1024px) {
  .grid__container {
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(2, 1fr);
    max-width: 1165px;
  }
}

@media only screen and (max-width: 400px) {
#header-container h2 {
    font-size: 20px;

}
}
</style>
