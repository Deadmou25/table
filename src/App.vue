<template>
  <div class="container">
    <div id="app">
      <div class="offset">
        <table cellspacing="0">
          <thead class="tableHeader">
          <tr>
            <th>id
              <button class="arrow">&#709;</button>
            </th>
            <th>Заголовок
              <button class="arrow" @click="sortedArray">&#709;</button>
            </th>
            <th>Описание
              <button class="arrow" >&#709;</button>
            </th>
          </tr>
          </thead>
          <tbody>
          <tr
              v-for="p in displayedPosts"
              :key="p.id"
          >
            <td class="id">{{ p.id }}</td>
            <td class="title">{{ p.title }}</td>
            <td class="body">{{ p.body }}</td>
          </tr>
          </tbody>
        </table>
        <nav aria-label="Page navigation example">
          <ul class="pagination">
            <div>
              <li class="page-item">
                <button type="button" class="page-link" @click="previousPage" :disabled="this.back">Назад</button>
              </li>
            </div>
            <div>
              <li class="page-item">
                <button type="button" class="page-number"
                        v-for="pageNumber in pages"
                        :key="pageNumber.id"
                >
                  {{ pageNumber }}
                </button>
              </li>
            </div>
            <div>
              <li class="page-item">
                <button type="button" @click="nextPage" class="page-link"> Далее</button>
              </li>
            </div>
          </ul>
        </nav>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";


export default {
  data() {
    return {
      posts: [],
      page: 1,
      perPage: 10,
      pages: [],
      back: true
    }
  },

  methods: {
    getPosts() {
      axios.get('https://jsonplaceholder.typicode.com/posts')
          .then(response => {
            this.posts = response.data;
            this.setPages()
          })
          .catch(e => {
            console.log(e);
          })

    },

    sortedArray() {

      let sortedPosts = this.posts;

      sortedPosts.sort((a,b) => {
        let fa = a.title.toLowerCase(), fb = b.title.toLowerCase();
        if (fa < fb) {
          return -1
        }
        if (fa > fb) {
          return 1
        }
        return 0
      })
    },

    setPages() {
      let numberOfPages = Math.ceil(this.posts.length / this.perPage);
      for (let index = 1; index <= numberOfPages; index++) {
        this.pages.push(index);
      }
    },

    sortById() {

    },

    nextPage() {
      this.page++
    },

    previousPage() {
      this.page--
      if(this.page!==1){
        this.back=true
      }else{
        this.back=false
      }
    }
  },

  computed: {
    displayedPosts() {
      let page = this.page;
      let perPage = this.perPage;
      let from = (page * perPage) - perPage;
      let to = (page * perPage);
      return this.posts.slice(from, to);
    },
  },

  created() {
    this.getPosts();
  },
}
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  height: 100%;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-family: Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  max-height: 100%;
  line-height: 22px;
  font-size: 14px;
  width: 100%;
}

* {
  margin: 0;
  padding: 0;
}

.tableHeader {
  background-color: #474955;
  height: 54px;
  text-align: center;
  align-items: center;
  color: white;
}

.tableHeader tr {
  border: none;
}

li {
  list-style: none;
}

li button:hover {
  color: #7EBC3C;
}

nav {
  display: flex;
  width: 100%;
  justify-content: center;
}

nav ul li {
  display: flex;
  justify-content: space-between;
}

.tableHeader {
  width: 100%;
}

.tableHeader tr td {
  height: 57px;
  text-align: left;
  padding: 0;
}

.pagination {
  display: flex;
  justify-content: space-between;
}

td {
  padding: 0 !important;
}

.page-number {
  color: black;
  background: white;
  border: none;
}

.page-link {
  color: black;
}

li .page-number:hover {
  color: green;
}

.container {
  max-width: 1079px;
  margin: 0 auto;
}

.id {
  width: 114px;
  height: 87px;
  margin-right: 50px;
}

.arrow {
  border: none;
  color: white;
  background: inherit;
}
</style>
