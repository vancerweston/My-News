<template>
  <div class="home">
    <div class="buttons">
      <button class="nav-button" v-on:click="reload()">All Articles</button>
      <button class="nav-button" v-on:click="business()">Busniness</button>
      <button class="nav-button" v-on:click="entertainment()">
        Entertainment
      </button>
      <button class="nav-button" v-on:click="health()">Health</button>
      <button class="nav-button" v-on:click="science()">Science</button>
      <button class="nav-button" v-on:click="sports()">Sports</button>
      <button class="nav-button" v-on:click="technology()">Technology</button>
    </div>
    <div class="cards-container">
      <div class="search-bar">
        <input
          type="text"
          placeholder="Search By Article Name"
          v-model="search"
        />
      </div>
      <template v-for="article in filteredArticles">
        <div class="article" :key="article.publishedAt">
          <div class="pic">
            <a v-bind:href="article.url" target="_blank">
              <img v-bind:src="article.urlToImage" alt="No Picture Avaliable" />
            </a>
          </div>
          <div class="data">
            <div class="article-title-desc">
              <h2>
                <a v-bind:href="article.url" target="_blank">{{
                  article.title
                }}</a>
              </h2>
              <h4>{{ article.description }}</h4>
            </div>
            <div class="author">
              <h5>Author: {{ article.author }}</h5>
            </div>
            <div class="publish-date">
              <h5>Published On: {{ article.publishedAt | dobFilter }}</h5>
            </div>
            <div class="content">
              <p>{{ article.content }}</p>
            </div>
          </div>
        </div>
      </template>
    </div>
    <footer>
      <h4>Vue News - Copyright Vance Weston 2020</h4>
      <div class="footer-nav">
        <p class="footer-button" v-on:click="reload()">All Articles</p>
        <p>|</p>
        <p class="footer-button" v-on:click="business()">Busniness</p>
        <p>|</p>
        <p class="footer-button" v-on:click="entertainment()">Entertainment</p>
        <p>|</p>
        <p class="footer-button" v-on:click="health()">Health</p>
        <p>|</p>
        <p class="footer-button" v-on:click="science()">Science</p>
        <p>|</p>
        <p class="footer-button" v-on:click="sports()">Sports</p>
        <p>|</p>
        <p class="footer-button" v-on:click="technology()">Technology</p>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      articles: [],
      search: ""
    };
  },
  methods: {
    business() {
      let b =
        "http://newsapi.org/v2/top-headlines?country=us&category=business&apiKey=cd9551e111db43b695d86bbc339c2e32";
      return fetch(b)
        .then(response => response.json())
        .then(json => {
          this.articles = json.articles;
        });
    },
    entertainment() {
      let e =
        "http://newsapi.org/v2/top-headlines?country=us&category=entertainment&apiKey=cd9551e111db43b695d86bbc339c2e32";
      return fetch(e)
        .then(response => response.json())
        .then(json => {
          this.articles = json.articles;
        });
    },
    health() {
      let h =
        "http://newsapi.org/v2/top-headlines?country=us&category=health&apiKey=cd9551e111db43b695d86bbc339c2e32";
      return fetch(h)
        .then(response => response.json())
        .then(json => {
          this.articles = json.articles;
        });
    },
    science() {
      let sc =
        "http://newsapi.org/v2/top-headlines?country=us&category=science&apiKey=cd9551e111db43b695d86bbc339c2e32";
      return fetch(sc)
        .then(response => response.json())
        .then(json => {
          this.articles = json.articles;
        });
    },
    sports() {
      let sp =
        "http://newsapi.org/v2/top-headlines?country=us&category=sports&apiKey=cd9551e111db43b695d86bbc339c2e32";
      return fetch(sp)
        .then(response => response.json())
        .then(json => {
          this.articles = json.articles;
        });
    },
    technology() {
      let t =
        "http://newsapi.org/v2/top-headlines?country=us&category=technology&apiKey=cd9551e111db43b695d86bbc339c2e32";
      return fetch(t)
        .then(response => response.json())
        .then(json => {
          this.articles = json.articles;
        });
    },
    reload() {
      location.reload();
    },
    getArticles() {
      let url =
        "http://newsapi.org/v2/top-headlines?country=us&apiKey=cd9551e111db43b695d86bbc339c2e32";
      return fetch(url)
        .then(response => response.json())
        .then(json => {
          this.articles = json.articles;
        });
    }
  },
  created() {
    this.getArticles();
  },
  filters: {
    dobFilter: function(value) {
      const options = {
        year: "numeric",
        month: "long",
        day: "numeric"
      };
      const date = new Date(value);
      return date.toLocaleDateString("en-US", options);
    }
  },
  computed: {
    filteredArticles() {
      return this.articles.filter(article => {
        const title = article.title;
        const s = this.search.toLowerCase();
        return title.toLowerCase().includes(s);
      });
    }
  }
};
</script>

<style scoped>
.cards-container {
  padding: 5px;
  display: grid;
  grid-template-columns: 33% 33% 33%;
  grid-column-gap: 10px;
  grid-row-gap: 10px;
}
.search-bar {
  grid-row: 1;
  grid-column: 1/4;
  margin: auto;
  width: 100%;
  max-width: 800px;
}
.data {
  padding: 25px;
}
.buttons {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-around;
  align-items: center;
  align-content: center;
}
.nav-button {
  background-color: lightgrey;
  padding: 5px;
  width: 100%;
  border-radius: 0 0 8px 8px;
  border: white 1px solid;
  cursor: pointer;
  margin-bottom: 20px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.3);
}
.nav-button:active {
  background-color: white;
}
input {
  width: 100%;
  max-width: 800px;
  padding: 8px 15px;
  background: white;
  border: 0px solid #dbdbdb;
}
.article {
  width: 90%;
  margin: 15px auto;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.3);
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
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.3);
}
.pic {
  align-self: center;
  text-align: center;
  height: 230px;
  width: 100%;
}
img {
  border: 1px solid gray;
  height: 230px;
  width: 100%;
  margin: auto;
}
.content {
  padding: 5px;
  text-indent: 15px;
}
footer {
  width: 100%;
  text-align: center;
  padding-top: 7px;
  height: 55px;
  background-color: white;
  vertical-align: middle;
}
.footer-nav {
  margin-top: 5px;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-around;
  align-items: center;
  align-content: center;
}
.footer-button {
  color: darkslategray;
  cursor: pointer;
}
@media only screen and (max-width: 1100px) {
  .cards-container {
    padding: 5px;
    display: grid;
    grid-template-columns: 50% 50%;
    grid-column-gap: 10px;
    grid-row-gap: 10px;
  }
  .search-bar {
    grid-row: 1;
    grid-column: 1/3;
    margin: auto;
    width: 100%;
  }
}
@media only screen and (max-width: 800px) {
  .cards-container {
    padding: 5px;
    display: grid;
    grid-template-columns: 100%;
    grid-column-gap: 10px;
    grid-row-gap: 10px;
  }
  .search-bar {
    grid-row: 1;
    grid-column: 1;
    margin: auto;
    width: 100%;
  }
  .data {
    padding: 25px;
  }
  .buttons {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: space-around;
    align-items: center;
    align-content: center;
  }
  .nav-button {
    background-color: lightgrey;
    padding: 5px;
    width: 100%;
    border-radius: 0 0 8px 8px;
    border: white 1px solid;
    cursor: pointer;
    margin-bottom: 20px;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.3);
  }
  .nav-button:active {
    background-color: white;
  }
  input {
    width: 100%;
    padding: 8px 15px;
    background: white;
    border: 0px solid #dbdbdb;
  }
  .article {
    width: 90%;
    margin: 15px auto;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.3);
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
    box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.3);
  }
  .pic {
    align-self: center;
    text-align: center;
    height: 230px;
    width: 100%;
  }
  img {
    border: 1px solid gray;
    height: 230px;
    width: 100%;
    margin: auto;
  }
  .content {
    padding: 5px;
    text-indent: 15px;
  }
  footer {
    width: 100%;
    text-align: center;
    padding-top: 7px;
    height: 80px;
    background-color: white;
    vertical-align: middle;
  }
  .footer-nav {
    margin-top: 5px;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: space-around;
    align-items: center;
    align-content: center;
  }
  .footer-button {
    color: darkslategray;
    cursor: pointer;
  }
}
@media only screen and (max-width: 570px) {
  .buttons {
    display: block;
  }
  .nav-button {
    background-color: lightgrey;
    padding: 5px;
    width: 100%;
    border-radius: 0 0 8px 8px;
    border: white 1px solid;
    cursor: pointer;
    margin-bottom: 5px;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.3);
  }
  footer {
    height: 40px;
  }
  footer h4 {
    margin-top: 5px;
  }
  .footer-nav {
    display: none;
  }
}
</style>
