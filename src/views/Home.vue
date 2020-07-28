<template>
  <div class="cards-container">
    <div class="search-bar">
      <input type="text" placeholder="Search By Article Name">
    </div>
    <template v-for="article in articles">
      <div class="article" :key="article.publishedAt">
        <div class="pic">
          <img v-bind:src="article.urlToImage" alt="Article Picture">
        </div>
        <div class="data">
          <div class="article-title-desc">
            <h2><a v-bind:href="article.url" target="_blank">{{ article.title  }}</a></h2>
            <h4>{{ article.description }}</h4>
          </div>
          <div class="author">
            <h5>Author: {{ article.author }}</h5>
          </div>
          <div class="publish-date">
            <h5>Published On: {{ article.publishedAt }}</h5>
          </div>
          <div class="content">
            <p>{{ article.content }}</p>
          </div>
        </div>
      </div>
    </template>
  </div>
</template>


<script>

export default {
  name: "Home",
    data() {
      return {
        articles: [],
        search: ""
      }
    },
    methods: {
      getArticles() {
        return fetch("http://newsapi.org/v2/top-headlines?country=us&apiKey=cd9551e111db43b695d86bbc339c2e32")
          .then(response => response.json())
          .then(json => {
            this.articles = json.articles;
          })
      }
    },
    created() {
      this.getArticles();
    }
};
</script>

<style scoped>
  .cards-container {
    padding: 5px;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-column-gap: 10px;
    grid-row-gap: 10px;
  }
  .search-bar {
    grid-row: 1;
    grid-column: 1/4;
  }
  .data {
    padding: 25px;
  }
  input {
    width: 100%;
    max-width: 300px;
    padding: 8px 15px;
    background: rgba(50, 50, 50, 0.2);
    border: 0px solid #dbdbdb;
  }
  .article {
    width: 90%;
    margin: 15px auto;
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.3);
    transition: 0.3s;
    background-color: white;
    border-radius: 5px;
  }
  .article-title-desc {
    text-align: left;
    align-self: center;
  }
  .article-title-desc h4 {
    padding: 5px 20px;
    border: 1px solid lightgrey;
    border-radius: 5px;
    text-align: center;
    color: darkslategray;
  }
  .article-title-desc h2 {
    color: navy;
    padding-bottom: 10px;
  }
  a {
    text-decoration: none;
    color: inherit;
  }
  .author {
    text-align: left;
    padding: 10px 0 0 15px;
  }
  .publish-date {
    text-align: left;
    padding: 0 0 5px 15px;
  }
  .article:hover {
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.3);
  }
  .pic {
    align-self: center;
    text-align: center;
  }
  img {
    border: 1px solid gray;
    height: 230px;
    width: 100%;
  }
  .content {
    padding: 5px;
    text-indent: 15px;
  }
</style>