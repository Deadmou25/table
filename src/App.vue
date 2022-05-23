<template>
  <div class="container">
    <div id="app">
      <div class="offset">
        <div class="search">
          <input type="search" @change="searchData" placeholder="Поиск" v-model="search">
          <button class="search__button"></button>
        </div>
        <table cellspacing="0">
          <thead class="tableHeader">
          <tr>
            <th>id
              &#709;
            </th>
            <th>Заголовок
              <button class="arrow">&#709;</button>
            </th>
            <th>Описание
              <button class="arrow">&#709;</button>
            </th>
          </tr>
          </thead>
          <tbody>
          <tr
              v-for="p in this.displayedPosts"
              :key="p.id"
          >
            <td class="id">{{ p.id }}</td>
            <td class="title">{{ p.title }}</td>
            <td class="body">{{ p.body }}</td>
          </tr>
          </tbody>
        </table>
        <div class="navigation">
          <div>
            <button type="button" @click="previousPage" :disabled="page===1" class="page-link">Назад</button>
          </div>
          <div class="page-number">
            <button type="button"
                    v-for="pageNumber in pages"
                    :key="pageNumber.id"
                    @click="page=pageNumber"
                    :class="{active:isPageActive(pageNumber)}"
            >
              {{ pageNumber }}
            </button>
          </div>
          <div>
            <button type="button" @click="nextPage" :disabled="page===pages.length" class="page-link"> Далее</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";


export default {
  components: {},

  data() {
    return {
      posts: [],
      page: 1,
      perPage: 0,
      pages: [],
      search: "",
      searchDelay: 500,
      searchTimer: 0,
      filterPosts: []
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

    searchData() {
      clearTimeout(this.searchTimer)
      this.searchTimer = setTimeout(() => {
        this.filterPosts = this.posts.filter(item => {
          return item.body.includes(this.search) || item.title.includes(this.search) || String(item.id).includes(this.search)
        })
      }, this.searchDelay)
      this.filterPosts.sort((a, b) => {
        if (a.id < b.id){
          a.slice()
          return 1
        }
        return -1
      })
    },

    setPages() {
      let numberOfPages = Math.ceil(this.posts.length / this.perPage);
      if (numberOfPages >= 10) {
        this.perPage += 1
      }
      for (let index = 1; index <= numberOfPages; index++) {
        this.pages.push(index);
      }
    },

    nextPage() {
      this.page++
    },

    previousPage() {
      this.page--
    },

    isPageActive(page) {
      return this.page === page;
    },
  },

  computed: {
    displayedPosts: function () {
      let page = this.page;
      let perPage = this.perPage;
      let from = (page * perPage) - perPage;
      let to = (page * perPage);
      if (this.search === "") {
        return this.posts.slice(from, to)
      }

      return this.filterPosts.slice(from, to)
    },
    // maxPage: function () {
    //   for (let i=0;i<this.filterPosts.length;i++){
    //     if(this.filterPosts[i]>10){
    //       return this.perPage +=1
    //     }
    //   }
    //   return this.filterPosts.length/this.perPage
    // }

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

.search {
  margin: 25px 0 15px 0;
  display: inline-flex;
  width: 100%;
}

.search__button {
  width: 21px;
  height: 21px;
  border: none;
  background-image: url("https://cdn.icon-icons.com/icons2/1769/PNG/128/4092559-magnifier-mobile-ui-search-ui-website-zoom_114034.png");
  background-repeat: no-repeat;
  background-size: 21px 21px;
  background-color: #5A5C66;
  margin: 8px 0px 8px 0;
  padding-left: 20px;
}


.search input {
  width: 631px;
  height: 52px;
  padding-left: 28px;
  background-color: #5A5C66;
  margin-right: -60px;
  margin-top: -5.6px;
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

td {
  padding: 0 !important;
}


.navigation {
  display: flex;
  justify-content: space-around;

}

.page-number {
  display: flex;
  align-items: center;
}

.page-number button {
  background: none;
  border: none;
  font-weight: 700;
  font-size: 16px;
  margin-right: 5px;


}

.page-link {
  color: black;
  background: none;
  font-size: 24px;
  border: none;
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

.active {
  color: green;
}
</style>
