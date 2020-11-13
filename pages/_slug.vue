<template>
  <div class="container">
    <!-- start-------------------- -->
    <div class="data">
      <!-- image -->
      <div class="data-img">
        <img :src="anime_data['image_url']" alt="" />
      </div>

      <div class="data-info">
        <!-- data info -->
        <NuxtLink to="/">Tap To Go back 👈</NuxtLink>
        <p><span>title: </span> <br> {{ anime_data["title"] }}</p>
        <p>
          <span>alternative title: </span><br>{{ anime_data["alternative_title"] }}
        </p>
        <p><span>summary: </span><br>{{ anime_data["summary"] }}</p>
        <p><span>aired from: </span><br>{{ anime_data["aired_from"] }}</p>
        <p>
          <span>broadcasting date: </span><br>{{ anime_data["broadcasting_date"] }}
        </p>
        <p><span>status: </span><br>{{ anime_data["status"] }}</p>
        <p><span>rating: </span><br>{{ anime_data["rating"] }}</p>
        <p><span>producer(s): </span><br>{{ anime_data["producers"] }}</p>
        <p><span>genre: </span><br>{{ anime_data["genre"] }}</p>
        <p>
          <span>number of episodes: </span
          ><br>{{ anime_data["number_of_episodes"] }}
        </p>
        <p>
          <span>number of episodes released: </span
          ><br>{{ anime_data["number_of_episodes_released"] }}
        </p>
      </div>

      <div
        class="data-list"
        v-for="(data, propertyName) in anime_data['episodes'][0]"
        :key="data.id"
      >
        <input
          type="checkbox"
          :id="
            'chbox-' +
            anime_data['title'].slice(0, 5) +
            propertyName.replace(/\s/g, '')
          "
        />
        <label for="chbox">
          <a :href="data[0]" id="links"> {{ propertyName }} </a>
        </label>
      </div>
      <div class="button">
        <input type="button" value="save" @click="save()" />

      </div>
    </div>
    <!-- end-------------------- -->
    <!-- <pre>{{ anime_data }}</pre> -->
  </div>
</template>

<script>
export default {
  async asyncData({ params, $axios }) {
    const api = `https://norapi.herokuapp.com/${params.slug}`;
    const anime_data = await $axios.$get(api);
    // const get_index = Object.keys(anime_data["episodes"][0]);
    const x = params;
    return { anime_data, x };
  },
  data() {
    return {};
  },
  mounted() {
    try {
      this.load();
    } catch (err) {
      return err
    }
  },
  methods: {
    save: function () {
      const inputs = document.querySelectorAll('input[type="checkbox"]');
      let arrData = [];
      inputs.forEach(function (input) {
        arrData.push({ id: input.id, checked: input.checked });
      });
      localStorage.setItem(this.anime_data.id, JSON.stringify(arrData));
    },

    load: function () {
      let inputs = JSON.parse(localStorage.getItem(this.anime_data.id)) ;
      inputs.forEach(function (input) {
        document.getElementById(input.id).checked = input.checked;
      });
    },
  },
};
</script>


<style scoped>
@import url("https://fonts.googleapis.com/css?family=Eater");
@import url("https://fonts.googleapis.com/css?family=Cutive");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

*:before,
*:after {
  box-sizing: border-box;
}

.container {
  display: flex;
  justify-content: center;
}

.data {
  flex-basis: 60%;
  height: 70%;
  border: 5px solid grey;
  padding: 20px;
}

.data-img {
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 50px;
  width: 320px;
  height: 450px;
  box-shadow: 20px 20px 20px rgba(0, 0, 0, 0.5),
    -20px -5px 20px rgba(0, 0, 0, 0.5);
}


img {
  width: 90%;
  height: 90%;
}

.data-info {
  margin: 0 auto;
  margin-top: 10px;
  text-align: center;
}

span {
  font-weight: bold;
  letter-spacing: 2px;
  color: green;
  font-family: "Eater";
}

p {
  font-family: "Cutive";
  font-size: 15px;
}

.data-list {
  display: flex;
  justify-content: center;
  position: relative;
  border: 1px solid crimson;
  margin-top: 5px;
}

a {
  text-decoration: none;
  color: grey;
  font-weight: bold;
}

input[type="checkbox"] {
  position: absolute;
  right: 20px;
  top: 3px;
}

input[type="checkbox"]:checked + label {
  background: green;
  border: 2px solid yellow;
  padding: 3px;
}

input[type="checkbox"]:checked + label > a {
  color: white;
}

/* save button */

div.button {
  margin-top: 10px;
  display: flex;
  justify-content: center;
}

input[type="button"] {
  width: 50px;
  height: 30px;
  cursor: pointer;
}

@media only screen and (max-width: 490px) {
  input[type="checkbox"] {
    position: absolute;
    right: 10px;
    top: 3px;
  }
}

@media only screen and (min-width: 1500px) {
  input[type="checkbox"] {
    position: absolute;
    right: 200px;
    top: 3px;
  }
}

@media only screen and (max-width: 500px) {
 .data {
   overflow-x: hidden;
   word-wrap: break-word;
   flex-basis: 500px;
 }
}
</style>
