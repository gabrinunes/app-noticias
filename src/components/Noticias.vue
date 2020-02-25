<template>
  <div>
      <div>
          <b-input v-model="search"></b-input>
          <b-button @click="Buscar" >Search</b-button>
      </div>
     <b-alert v-if="alert" show variant="danger">Não achamos nenhum resultado para sua pesquisa:(</b-alert>
     <div v-else>
       <div class="articlerow" v-for="news in news" :key="news.index">
       <div class="article">
        <h2 class="title"></h2>
        <h3>{{news.title}}</h3>
        <p>{{news.content}}</p>
         <a :href="news.url" target="_blank" class="readmore">Read More</a>' +
       </div>
       <div class="share">
         <img class="storyimage" :src="news.urlToImage" />
       </div>
      </div>
  </div>
     </div>
</template>

<script>
export default {
     data(){
         return {
             news:[],
             search:'',
             API_KEY:'dc98e06600f84cebb1fdb9130a200e9d',
             alert: false
         }
     },
     created(){
       window.addEventListener('keyup',evt => {
           if(evt.keyCode==13){
             this.Buscar()
           }
       })
     },
     methods:{
         Buscar(){
             this.$http('everything?q='+this.search+'&sortBy=publishedAt&apiKey='+this.API_KEY).then(res=>{
               this.news = res.data.articles
               if(this.news ==''){
                   this.alert = true
               }
             },err =>{
                 console.log(err)
             })
         },
         Home(){
             this.$http('top-headlines?country=br&category=business&apiKey='+this.API_KEY).then(res =>{
                 this. news = res.data.articles
                 },err =>{
                 console.log(err)
             })
         }
     },
     mounted(){
         this.Home()
     }

}
</script>
 
<style>
  .articlerow {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

  .storyimage {
    width: 100%;
    height: auto;
  }
</style>