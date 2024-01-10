
<template>

<div>
  <nav>
    <h1 class="header">Movies At your Fingertips!</h1>
    <input class="searchbar" type="text" placeholder="Search" v-model="text" @input="filteredList"/>
  </nav>
   
  <div class="content-box"> 
    <div class="allMovie">
      <h1 class="box-heading">All Movies</h1>
      
      <div class="movie-section">
        <div class="list" v-for="movie in this.movies" :key="movie.id">
          <div class="img">
          <img :src="movie.poster" alt="photo">
          </div>
          <div class="title">
          {{movie.title}}
          </div>
          <div class="des">
          {{movie.overview}}
          </div>
          <button class="btn" @click = "favorite(movie) ">
           <i  class="fa fa-star icon" aria-hidden="true"></i>
           </button>
       </div>

      </div>
    </div>

    <div class="fav-filter">

      <div class="filteredMovie">
       <h1 class="box-heading">Search Results</h1>
        <div class="movie-section-fil">

          <div class="list list-fil" v-for="movie in this.selectedMovies" :key="movie.id">
            <div class="img">
             <img :src="movie.poster" alt="photo">
            </div>
            <div class="title">
             {{movie.title}}
            </div>
            <div class="des">
              {{movie.overview}}
            </div>
            <button class="btn" @click = "favorite(movie)"><i class="fa fa-star icon" aria-hidden="true"></i></button>
          </div>
        </div>
      </div>

      <div class="favourite">
         <h1 class="box-heading">Favourite Movies</h1>
         <div class="movie-section-fil">
            <div class="list list-fil" v-for="movie in this.favouriteMovies" :key="movie.id">
              <div class="img">
              <img :src="movie.poster" alt="photo">
              </div>
              <div class="title">
              {{movie.title}}
              </div>
              <div class="des">
                {{movie.overview}}
              </div>
              <button class="btn" @click = "deletemovie(movie)"><i class="fa fa-star icon icon-fav " aria-hidden="true"></i></button>
            </div>
          </div>
      </div>
    </div>
  </div>
</div>

</template>

<script >

import axios from 'axios'
 

export default {
    name: 'home',
    mounted() {
        axios({
          method: "GET",
          "url": "assets/json/movies.json"
        }).then(response => {
          this.movies = JSON.parse(JSON.stringify(response.data));
        }, error => {
          // eslint-disable-next-line
          console.error(error);
        });
    },
    data() {
        return {

          movies:[],
          selectedMovies:[],
          favouriteMovies:[],
          text:""
        }
    },
    components: {},
    methods: {
      filteredList(event) {
        this.selectedMovies = this.movies.filter((movie) => {
          return movie.title.toLowerCase().includes(event.target.value.toLowerCase());
        });
      },

      favorite(event){
        if(!this.favouriteMovies.includes(event)){
            this.favouriteMovies.push(event);
          }
      },

      deletemovie(event){
        if(this.favouriteMovies.includes(event)){
          this.favouriteMovies.splice(this.favouriteMovies.indexOf(event), 1);
        }
      }
    }
}


</script>


<style scoped>

body{
  margin: 0;
  padding: 0;
}
::-webkit-scrollbar {
    display: none;
}

nav{
  display: flex;
  flex-direction: column;
  height: 150px;
  width: 100vw;
  background-color: rgb(0, 0, 0);
  margin: auto;
  padding: 1rem;
  align-items: center;
  justify-content: center;
}

.header{
  color: white;
}
.searchbar{
   height: 3rem;
   width: 30rem;
   border-radius: 8px;
   font-size: 1.2rem;
   padding-left: 15px;
   box-shadow: 6px 6px gray;
}

 .content-box{
       position: relative;
       margin: 1rem 2rem 1rem ;
       display: flex;
       flex-wrap: wrap;
       justify-content: center;
      background-color: rgb(237, 235, 235);
      height: 1000px;
      border-radius: 8px;

  }


  .allMovie{
    width: 47%;
    height: 1000px;
    margin:1rem;
  }

  .fav-filter{

    display: flex;
    flex-wrap:wrap;
    width: 47%;
    height: 1000px;
    margin:1rem;
  }
  .filteredMovie,.favourite{
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    height: 50%;
    /* margin:1rem; */
  }

  .list{
    position: relative;
    padding: 10px;
    height: 50%;
    width: 50%;
    background-color: white;
    border: 1px solid black;
    align-items: center;
    text-align: start;
    overflow-y: hidden;
    overflow-x: hidden;
  }
  .list:hover{
    background-color: rgb(220, 219, 221);
  }
  .list-fil{
      height: 100%;
      width: 50%;
  }


  .moviename{
     height:20%;
     width: 20%;
     text-decoration: none;
  }

  .icon:hover{
     color:goldenrod;
  }
  .box-heading{
    display: flex;
    align-items: center;
    width: 100%;
    height: 4rem;
    justify-content: center;
    align-items: center;
    color:rgb(0, 0, 0) ;
    border: 2px solid black;
    border-radius: 6px;
    box-shadow: 2px 2px gray;
    background-color: rgb(178, 178, 178);
  }
  .movie-section{
    display: flex;
    flex-wrap: wrap;
    overflow-y: scroll;
    padding: 0;
    width: 100%;
    height:90% ;
    border: 1px solid black;
    /* border-bottom: 2px solid black;
    border-top: 2px solid black; */
  }

  .movie-section-fil{
  
    display: flex;
    flex-wrap: wrap;
    overflow-y: scroll;
    margin-top:-1.7rem;
    width: 100%;
    height:79% ;
    border: 1px solid black;
    /* border-bottom: 2px solid black;
    border-top: 2px solid black; */
    /* overflow-y: scroll; */
  }
  .btn{
    position: absolute;
    right: 7%;
    bottom:33%;
    background-color:q;
    height: 25px;
    width: 10%;
    margin: 0;
    padding: 0;
    cursor: pointer;
  }

  .icon{
    height: 60%;
    width: 60%;
  }
  .icon-fav{
    color:gold
  }
  .img{
    margin: 0;
    padding: 0%;
    height: 70%;
    width: 100%; 
  }
  img{
    height: 100%;
    width: 100%;
  }

  .movie-section-fil .img{
    margin: 0;
    padding: 0%;
    height: 87%;
    width: 100%; 
  }
  img{
    height: 100%;
    width: 100%;
  }

  .title{
    height: 10%;
    /* text-decoration: underline; */
    font-weight: bold;
    overflow:auto;
    text-align: center;
    font-size: large;
    text-overflow: ellipsis;
    margin: 0.2rem;

  }
  .des{
    /* position: relative; */
    height: 14%;
    width: 100%;
    text-align: center;
    overflow:scroll;
    font-size:small;
    text-overflow: ellipsis;
    margin: 0.1rem;
    
  }

  .movie-section-fil .des{
    height: 0%;
    width: 0%; 
  }
  
  
</style>

