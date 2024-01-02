<script>
import { ref, toRaw } from 'vue'
import '../styles/style.sass'

const getRandomInt = (max) => Math.floor(Math.random() * max)

import axios from 'axios'

export default {
  data() {
    return {
      thumbnail: '',
      clicked: false,
      textContent: "Узнать"
    }
  },
  methods: {
    async getBook() {
      const response = await axios.get(`https://www.googleapis.com/books/v1/volumes/?q=inauthor:"дарья+донцова"&maxResults=40&startIndex=${getRandomInt(100)}&langRestrict=ru`)
      const post = response.data.items.map((el) =>  { 
        return {
          thumbnail: el.volumeInfo.imageLinks.thumbnail,
          title: el.volumeInfo.title, 
          link: el.saleInfo.buyLink }
        })[getRandomInt(40)]
      
      this.thumbnail = `<a href="${post.link}"> <img src="${ post.thumbnail }"" alt="${ post.title }" /> </a>`
      this.clicked = true
      this.textContent = "Попробовать снова"
    }
  }
}


// export default {
//   name: 'App',
//   created() {
//     this.searchedLocation = this.getCurrentLocation();
//     axios.get(
//     `https://www.googleapis.com/books/v1/volumes/?q=inauthor:%22%D0%B4%D0%B0%D1%80%D1%8C%D1%8F+%D0%B4%D0%BE%D0%BD%D1%86%D0%BE%D0%B2%D0%B0%22&maxResults=40&startIndex=${this.startIndex}&langRestrict=ru`)
//     .then(a => this.weather = a.data)
//     .catch(err => console.error('Cannot load data', err))
//   },

// methods: {
//     actOnSubmit() {
//       axios.get(
//       `https://www.googleapis.com/books/v1/volumes/?q=inauthor:%22%D0%B4%D0%B0%D1%80%D1%8C%D1%8F+%D0%B4%D0%BE%D0%BD%D1%86%D0%BE%D0%B2%D0%B0%22&maxResults=40&startIndex=${this.startIndex}&langRestrict=ru`)
//       .then(a => this.weather = a.data)
//       .catch(err => console.error('Cannot load data', err))
//     },
//     getCurrentLocation() {
//         if(navigator.geolocation) {
//           return navigator.geolocation.getCurrentPosition(this.coordinatesSuccess)
//         } else {
//           return undefined
//         }
//       },
//   coordinatesSuccess(position) {
//     let coords = position.coords;
//     return coords.latitude + ',' + coords.longitude;
//   }
//   }
// }

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

  <div class="book-wrapper">
    <button type="button" @click="getBook" :class="{ clicked }">{{ textContent }}</button>
    <div v-if="{ clicked }"> 
     <div v-html="thumbnail">
      
     </div> 
    </div>
  </div>
</template>

<style scoped>
h1 {
  max-width: 22rem;
  text-align: left;
  font-weight: 400;
  padding: 5rem 3rem;
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

.book-wrapper {
  padding: 0 2rem;
  height: 100%;
  display: flex;
  align-items: center;
  color: #009985;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  font-size: 4rem;
  width: 21rem;

  box-sizing: border-box;

}

button {
  font-weight: 400;
  border: none;
  color: #c63e90;
  text-shadow: 0.05rem 0 #feed02;
  font-size: 3rem;
  padding: 2.5rem;
  background: #009985;
  font-family: 'Roboto Serif', serif;
  border: 1px solid transparent;
  transition: all 0.3s ease;
  cursor: pointer;
  margin-top: 9rem;
}

button:hover,
button.clicked {
  background: none;
  color: #009985;
  border: 1px solid #009985;
}

button.clicked {
  margin-top: 1rem;
  font-size: 1.5rem;
  padding: 0.5rem;
}

img {
  height: 20rem;
}

a {
  height: 100%;
  display: block;
}

@media (max-width: 768px) {
  .book-wrapper {
    width: 100%;
    height: 30rem;
    margin-top: 1rem;
  }


}</style>
