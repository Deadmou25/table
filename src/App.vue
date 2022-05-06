<template>

<div class="container-lg">
  <div id="app" class="col-sm-12">
    <div class="offset">
      <b-table
          :items="displayedPosts"
          :fields="fields"

      >

      </b-table>
      <nav aria-label="Page navigation example">
        <ul class="pagination">
          <li class="page-item">
            <button type="button" class="page-link"  @click="page--" disabled> Назад</button>
          </li>
          <li class="page-item">
            <button type="button" class="page-number"
                    v-for="pageNumber in pages.slice(0, 10)"
                    :key="pageNumber.id"
                    @click="page = pageNumber"> {{ pageNumber }}
            </button>
          </li>
          <li class="page-item">
            <button type="button" @click="page++"  class="page-link"> Далее</button>
          </li>
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
      posts: [''],
      page: 1,
      perPage: 10,
      pages: [],
      fields: [
        {
          key: 'id',
          sortable: true
        },
        {
          key: 'title',
          sortable: false
        },
        {
          key: 'body',
          label: 'Person age',
          sortable: true,
          // Variant applies to the whole column, including the header and footer

        }
      ],
    }
  },
  methods: {
    getPosts() {
      axios.get('https://jsonplaceholder.typicode.com/posts')
          .then(response=>{

              this.posts = response.data;

          })
    },
    setPages() {
      let numberOfPages = Math.ceil(this.posts.length / this.perPage);
      for (let index = 1; index <= numberOfPages; index++) {
        this.pages.push(index);
      }
    },
    paginate(posts) {
      let page = this.page;
      let perPage = this.perPage;
      let from = (page * perPage) - perPage;
      let to = (page * perPage);
      return posts.slice(from, to);
    }
  },
  computed: {
    displayedPosts() {
      return this.paginate(this.posts);
    }
  },
  watch: {
    posts() {
      this.setPages();
    }
  },
  created() {
    this.getPosts();
  },
  filters: {
    trimWords(value) {
      return value.split(" ").splice(0, 20).join(" ") + '...';
    }
  }
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

h6, h5, h4, h3, h2, h1 {
  margin: 0;
  padding: 0;
}
thead{
  background-color: #474955;
  height: 54px;
  text-align: center;
  align-items: center;
}
thead tr th{
  align-items: center;
  text-align: center;
}
li {
  list-style: none;
}

li button {

}

li button:hover {
  color: #7EBC3C;
}

p {
  padding: 0;
  margin: 0;
}

nav{
  display: flex;
  width: 100%;
  justify-content: center;
}
ul{
  display: flex;
}
nav ul li{
  display: flex;
  justify-content: space-between;
}


table {
  width: 100%;
}
table tr td{
  height: 57px;
  text-align: center;
  align-items: center;
  padding: 0px;

}
.pagination{
  display: flex;
  justify-content: space-between;
}
td{
  padding: 0 !important;
}
.page-number{
  color: black;
  background: white;
  border: none;
}
.page-link{
  color:black;

}
li .page-number:hover{
  color:green;

}

</style>
