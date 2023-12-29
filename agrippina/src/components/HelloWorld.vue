<script>
import { ref } from 'vue'
import '../styles/style.sass'

const count = ref(0)

import axios from 'axios'

export default {
  data() {
    return {
      posts: []
    }
  },
  mounted() {
    axios
      .get('https://www.googleapis.com/books/v1/volumes?q=%D0%B4%D0%BE%D0%BD%D1%86%D0%BE%D0%B2%D0%B0')
      .then((response) => {
        this.posts = response.data
      })
  }
}

</script>

<template>
  <h1>
    <span class="first">
      Какая ты
    </span>
    <span class="second">
      сегодня
    </span>
    <span class="third">
      книга Дарьи
    </span>
    <span class="fourth">
      Донцовой?
    </span>
  </h1>

  <div class="button-wrapper">
    <button type="button" @click="count++">Узнать</button>
  </div>
  {{ posts }}
</template>

<style scoped>
h1 {
  max-width: 22rem;
  text-align: left;
  font-weight: 400;
  padding: 5rem 3rem;
  border-left: 1px solid;
}


.first {
  display: inline-block;
  color: #feed02;
  font-weight: 100;
  text-shadow: 0.1rem 0.1rem #c63e90;
  font-size: 3.9rem;
}


.second {
  font-weight: 700;
  font-size: 4rem;
  text-align: center;
}

.fourth {
  color: #feed02;
  font-weight: 700;
  letter-spacing: -1.5px;
  text-shadow: 0 0.15rem #009985;
}

.third {
  color: #009985;
  font-style: oblique;
  font-weight: 100;
  letter-spacing: -1.5px;
}

.button-wrapper {
  padding: 2em;
  height: 100%;
  background: #c63e90;
  display: flex;
  align-items: center;
}

button {
  border-radius: 3rem;
  font-weight: 900;
  border: none;
  color: #c63e90;
  text-shadow: 0.05rem 0 #feed02;
  font-size: 3rem;
  padding: 2.5rem;
  background: #009985;
  font-family: 'Roboto Serif', serif;
  font-style: italic;
  border: 1px solid transparent;
  transition: all 0.3s ease;
  cursor: pointer;
}

button:hover {
  background: none;
  color: #009985;
  border: 1px solid #009985;
}
</style>
