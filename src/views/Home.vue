<template>
  <div class="body-inner-content travel-page">
    <div class="travel-overview">
			<div class="container">
				<div class="row"> 
					<div class="col-xs-12">
							<div v-for="article in item.articles" class="article">
								<a v-bind:href="article.url"> <h3>{{ article.title }} </h3></a>
								<h5>{{ article.author }}, {{ article.publishedAt }}</h5>
                <p>{{article.description}}</p>
								<img v-bind:src="article.urlToImage" v-bind:alt="article.urlToImage">
							</div>
					</div>
				</div>
			</div>
		</div>
  </div>
</template>
<script>

  export default {
    data() {
      return {
    		item: []
      }
    },
    created() {
      this.$http.get("https://newsapi.org/v2/everything?q=bitcoin&from=2019-03-25&sortBy=publishedAt&apiKey=02f507e0937249598fd3f45428547706")
        .then(response => response.json(), error => console.log(error))
        .then(json => this.item = json, error => console.log(error));
    },
  }
</script>

<style>
.container {
  width: 940px;
  margin: 0 auto;
}
.article a, .article h3, .article h5, .article p{
  padding-left: 20px;
  margin: 0;
  text-decoration: none;
}
.article h3 {
  color: #333;
}
.article p {
  padding-bottom: 20px;
}
.article {
  text-align: left;
  margin-bottom: 25px;
  border-radius: 5px;
  box-shadow: 0px 0px 5px #ccc;
  padding: 10px 0 0 0;
  background: rgba(204, 204, 204, 0.1);
}
img {
  width: 100%;
}
</style>