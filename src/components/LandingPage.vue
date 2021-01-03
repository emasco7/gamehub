<template>
  <b-container  fluid class="container-bg overflow-hidden">
    <b-navbar class="nav-bg animate__animated animate__fadeInDown" toggleable="lg" type="dark" fixed="top">
        <b-navbar-brand href="#">GAMEHUB</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
            <b-navbar-nav>
                <b-nav-item class="ml-5"  href="#">Home</b-nav-item>
                <b-nav-item-dropdown class="ml-5 p-0 nav-link" text="Category" right >
                    <b-dropdown-item href="#">Arcade</b-dropdown-item>
                    <b-dropdown-item href="#">Adventure</b-dropdown-item>
                    <b-dropdown-item href="#">PG 13</b-dropdown-item>
                    <b-dropdown-item href="#">Sports</b-dropdown-item>
                </b-nav-item-dropdown>
                <b-nav-item-dropdown class="ml-5 p-0 nav-link" text="Platform" right >
                    <b-dropdown-item href="#">PlayStation 3</b-dropdown-item>
                    <b-dropdown-item href="#">PlayStation 4</b-dropdown-item>
                    <b-dropdown-item href="#">PlayStation 5</b-dropdown-item>
                    <b-dropdown-item href="#">Xbox</b-dropdown-item>
                </b-nav-item-dropdown>
                <b-nav-item class="ml-5" href="#">Shop</b-nav-item>
                <input class="ml-5 search-input text-center" type="search" placeholder="🔍Search">
            </b-navbar-nav>

            <!-- Right aligned nav items -->
            <b-navbar-nav class="ml-auto">
                <b-button size="sm" class="my-2 my-sm-0 login-btn" type="submit">Login</b-button>
                <b-button size="sm" class="my-2 my-sm-0 login-btn" type="submit"><b-icon icon="cart2"></b-icon></b-button>
                

            </b-navbar-nav>
        </b-collapse>
    </b-navbar>
    <b-row align-v="center" class="home-bg">
        <img class="home-img" :src="require('../assets/img/'+currentSlideShow.img)"  :alt="currentSlideShow.img"/>
        <b-container fluid class="mt-4">
            <b-row>
                <div class="col-md-6">
                    <p class="category animate__animated animate__fadeInLeft">{{currentSlideShow.category}}</p>
                    <p class="title animate__animated animate__fadeInLeft">{{currentSlideShow.title}}</p>
                    <p class="subtitle animate__animated animate__fadeInLeft">{{currentSlideShow.subtitle}}</p>
                    <Ratings :ratingValue="currentSlideShow.ratings"/>
                    <div class="d-flex flex-row align-items-center mt-3">
                        <div class="mr-3 available">Available on :</div>
                        <img class="mr-4" src="~@/assets/img/xbox.svg" alt="xbox">
                        <img class="mr-4" src="~@/assets/img/ps4.svg" alt="ps4">
                        <img class="mr-4" src="~@/assets/img/PC.svg" alt="pc">
                    </div>
                    <b-button class="view-in-shop" variant="primary">VIEW IN SHOP</b-button>

                </div>
        
                <b-col md="6" align-self="end" class="animate__animated animate__fadeInRight">
                    <div class="d-flex flex-row align-items-center">
                        <div class="current-slide">{{currentSlide.toString().length>1?currentSlide:'0'+currentSlide}}</div>
                        <div class="text-white current-slide">/</div>
                        <div class="mr-3 total-slide">{{caurousel.length.toString().length>1?caurousel.length:'0'+caurousel.length}}</div>
                        <div class="ml-auto d-flex flex-row">
                            <div>
                                <b-icon class="previous-slide" icon="chevron-left" @click="currentSlide>1?currentSlide--:currentSlide"></b-icon>
                            </div>
                            <div class="ml-4">
                                <b-icon class="next-slide" icon="chevron-right" @click="currentSlide<caurousel.length?currentSlide++:currentSlide"></b-icon>
                            </div>
                        </div>
                    </div>
                    <b-progress class="mt-3 slide-progress" :value="(currentSlide/caurousel.length)*100" variant="warning"></b-progress>
                </b-col>
            </b-row>
        </b-container>
    </b-row>
    <b-row>
        <b-col lg="12">
         <h1 class="mt-5 text-white hero-title">NEW RELEASES</h1>
        </b-col>
        <b-col md="3" v-for="release in newRealeases" :key="release.id">
           <ReleaseCard :releaseImage="release.img" 
                        :releaseTitle="release.title" 
                        :releaseCategory="release.category"
                        :releaseRating="release.ratings"
                        :releaseStudio="release.studio"/>
        </b-col>
        <b-col md="12">
            <div class="mt-5 d-flex flex-row">
               <div class="d-flex flex-row ml-auto align-items-center">
                    <p class="m-0 view-shop">View in Shop</p>
                    <b-icon class="text-white ml-2 view-shop" icon="chevron-right"></b-icon>
               </div>
               
            </div>
        </b-col>
    </b-row>
    <b-row>
        <b-col lg="12">
            <h1 class="mt-5 text-white hero-title">COMING SOON</h1>
        </b-col>
    </b-row>
    <b-row class="coming-soon-bg mt-5">
        <b-col md="4">
            
        </b-col>
        <b-col md="4" align-self="end" class="mb-5">
            <b-progress class="mt-3 slide-progress" :value="10" variant="warning"></b-progress>
        </b-col>
        <b-col md="4" align-self="center" class="d-flex flex-column">
            <div class="ml-auto mr-4 d-flex flex-column">
                <p class="text-right coming-soon-title">SPIDER MAN</p>
                <p class="text-right coming-soon-subtitle">MILES MORALES</p>
                <p class="text-right coming-soon-date">Out on: <span>21/01/2021</span></p>
                <b-button class="view-in-shop ml-auto" variant="primary">PRE-ORDER NOW</b-button>
            </div>
        </b-col>
    </b-row>
    <b-row>
        <b-col lg="12">
            <h1 class="mt-5 text-white hero-title">PRE-ORDERS</h1>
        </b-col>
        <b-col md="3" v-for="preOrder in preOrders" :key="preOrder.id">
           <ReleaseCard :releaseImage="preOrder.img" 
                        :releaseTitle="preOrder.title" 
                        :releaseCategory="preOrder.category"
                        :releaseRating="preOrder.ratings"
                        :releaseStudio="preOrder.studio"
                        :hasRatings="false"/>
        </b-col>
        <b-col md="12">
            <div class="mt-5 d-flex flex-row">
               <div class="d-flex flex-row ml-auto align-items-center">
                    <p class="m-0 view-shop">View in Shop</p>
                    <b-icon class="text-white ml-2 view-shop" icon="chevron-right"></b-icon>
               </div>
               
            </div>
        </b-col>
    </b-row>

     <b-row>
        <b-col lg="12">
            <h1 class="mt-5 text-white hero-title">FEATURED</h1>
        </b-col>
        <b-col md="8" class="featured-bg d-flex">
            <div class="ml-auto d-flex ">
                 <div class="ml-auto mr-4 d-flex flex-column justify-content-center">
                    <p class="text-right coming-soon-title">CYBERPUNK</p>
                    <Ratings class="ml-auto coming-soon-subtitle" :ratingValue="4.7"/>
                    <b-button class="view-in-shop ml-auto" variant="primary">BUY NOW</b-button>
                </div>
            </div>
        </b-col>
        <b-col md="4" class="d-flex flex-column">
            <div class="mb-2 first-video d-flex justify-content-center align-items-center">
              <button class="play-btn">
                <b-icon class="text-white  play-icon" icon="play-fill"></b-icon>
              </button>
            </div>
            <div class="mt-2 second-video d-flex justify-content-center align-items-center">
                <button class="play-btn">
                    <b-icon class="text-white  play-icon" icon="play-fill"></b-icon>
                 </button>
            </div>
        </b-col>
     </b-row>
     <b-row class="win-big-bg my-5 mx-3">
         <b-col lg="12">
            <h1 class="mt-5 text-center win-big-title">WIN BIG ON GAMEHUB</h1>
        </b-col>
        <b-col md="6">
            <p class="promo ml-5">Stand a chance to win a brand new Playstation 5
                when you purchase games worth <span>N150,000</span></p>
            <p class="coming-soon-date mt-2 ml-5">Offer valid: <span>2nd January - 11th January 2021</span></p>
        </b-col>
        <b-col md="6" class="d-flex">
            <img class="ml-auto console" src="~@/assets/img/Playstation-5-games-console.png" alt="console">
        </b-col>
     </b-row>
     <footer>
         <b-row class="footer-bg">
             <b-col md="3 d-flex flex-column">
                 <p class="footer-brand">GAMEHUB</p>
                 <div class="d-flex flex-row mt-auto handles-bg">
                    <b-icon class="text-white " icon="facebook"></b-icon>
                    <b-icon class="text-white ml-4 " icon="twitter"></b-icon>
                    <b-icon class="text-white ml-4 " icon="instagram"></b-icon>
                    <b-icon class="text-white ml-4 " icon="linkedin"></b-icon>
                 </div>
             </b-col> 
            <b-col md="2" >
                <p class="footer-title">Category</p>
                 <ul class="footer-ul p-0 m-0">
                    <li v-for="category in categories" :key="category.id" >
                        <a class="footer-link" >{{category}}</a>
                    </li>
                </ul>
             </b-col>
            <b-col md="3">
                <p class="footer-title">Platform</p>
                 <ul class="footer-ul p-0 m-0">
                    <li v-for="platform in platforms" :key="platform.id">
                     <a class="footer-link" href="#">{{platform}}</a>
                    </li>
                </ul>
             </b-col>
            <b-col md="4">
                <p class="footer-title">Newsletter</p>
                <p class="text-white">Subscribe to our newsletter to stay
                    updated on the latest games,slash sales
                    and much more.</p>

                <b-input-group class="mt-3">
                    <b-form-input placeholder="Your email"></b-form-input>
                    <b-input-group-append>
                        <b-button class="subscribe-btn">Subscribe</b-button>
                    </b-input-group-append>
                </b-input-group>

             </b-col>
         </b-row>
         <b-row>
             <b-col md="12">
                 <p class="text-white text-center m-4">Gamehub © 2020 | All rights reserved</p>
             </b-col>
         </b-row>
     </footer>
  </b-container>
</template>

<script>

import Ratings from './Ratings.vue';
import ReleaseCard from "./ReleaseCard.vue";
export default {
    components: {
        Ratings,
        ReleaseCard
    },
data() {
    return {
        caurousel:[
           {img:'black_panther.svg',title:'BLACK PANTHER',category:'Action',ratings:'4.5',subtitle:"BLACK PANTHER is a superhero game based on Marvel Comics character of the same name. T’Challa is crowned king of Wakanda following his father’s death, but he is challenged by killmonger who plans to abandon the country’s isolationist policies."},
           {img:'vtm_bloodlines.svg',title:'BLOODLINES',category:'Adventure',ratings:'4.7',subtitle:"BLOODLINES depicts the fledgling’s journey through the early 21st-century Los Angeles to uncover the truth behind a recently discovered relic that heralds the end of all vampires. BLOODLINES is presented from first and third person perspective"},
           {img:'call_of_duty_modern_warfare.svg',title:'CALL OF DUTY',category:'Action',ratings:'4.5',subtitle:"CALL OF DUTY designed for all gaming platforms.Play iconic multiplayer maps and mode anytime, anywhere.100 player Battle Royale battleground | Fast 5v5 team deathmatch | Sniper vs sniper battle | Activision’s free-to-play."},
           {img:'cool_spiderman.svg',title:'SPIDERMAN',category:'Action',ratings:'4.6',subtitle:"SPIDERMAN is an action-adventure game developed by Insomniac Games and published by Sony Interactive Entertainment. Based on the Marvel Comics superhero SPIDERMAN, it is inspired by long-running comic book mythology."},
        ],
        currentSlide:1,
       newRealeases:[
           {img:'desperados.svg',title:'Red Dead Redemption 2',category:'Action',ratings:'4.5',studio:"Rockstar Games"},
           {img:'operator_nokk.svg',title:'Rainbow Seige Six',category:'Action',ratings:'4.3',studio:"Kalaiselvam G"},
           {img:'hitman.svg',title:'Hitman III',category:'Action',ratings:'4.7',studio:"Square Enix Ltd."},
           {img:'takkar_far_cry.svg',title:'Far Cry Primal',category:'Action',ratings:'4.5',studio:"Ubisoft"},
           {img:'sea_of_solitude.svg',title:'Sea of Solitude',category:'Action',ratings:'4.5',studio:"Rockstar Games"},
           {img:'girl_crimson.svg',title:'Crimson Desert',category:'Action',ratings:'4.8',studio:"Tencent"},
           {img:'destiny_2.svg',title:'Destiny 2',category:'Action',ratings:'4.4',studio:"Square Enix Ltd."},
           {img:'samurai_ghost_of_tsushima.svg',title:'Samurai Ghost',category:'Action',ratings:'4.6',studio:"EMASCO STUDIOS"}],
        preOrders:[
           {img:'kratos_in_god_of_war.svg',title:'God of War',category:'Action',ratings:'4.5',studio:"Rockstar Games"},
           {img:'black_adam_rock.svg',title:'Black Adam',category:'Action',ratings:'4.3',studio:"Kalaiselvam G"},
           {img:'dishonored_video_game.svg',title:'Dishonored',category:'Action',ratings:'4.7',studio:"Square Enix Ltd."},
           {img:'tom_clancys.svg',title:'Ghost Recon Wildland',category:'Action',ratings:'4.5',studio:"Ubisoft"}],
        categories:['Arcade','Adventure','PG 13','Sports'],
        platforms:['Playstation 3','Playstation 4','Playstation 5','Xbox'],
    }
},
computed: {
    currentSlideShow() {
        return this.caurousel[this.currentSlide-1]; 
    }
},
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap');
.container-bg{
   background: #121212;
}
.nav-bg{
    background: rgba(0, 0, 0, 0.685);
}
.navbar-dark .navbar-nav .nav-link {
  position: relative;
}
.navbar-dark .navbar-nav .nav-link::after{
    color: rgb(255, 255, 255);
    border-bottom: 3px solid #FBC02D;
    content:'';
    position: absolute;
    left: 0;
    width: 0;
    z-index: -1;
    bottom: -3px;
    transition: all 0.5s;
}
.navbar-dark .navbar-nav .nav-link:hover:after, .navbar-dark .navbar-nav .nav-link:focus:after {
    color: rgb(255, 255, 255);
    border-bottom: 3px solid #FBC02D;
    width: 100%;
}
.search-input{
    width:23rem;
    color: white;
    background: none;
    border: none;
    border-bottom: 3px solid white;
    transition: all 0.5s;
    
    

}
.search-input:focus,.search-input:hover{
    outline: none;
    border-bottom: 3px solid #FBC02D;
    transition: all 0.5s;

}

.home-bg{
    height: 100vh;
    /* background: url('~@/assets/img/black_panther.svg'); */
    background-size: cover;
    background-repeat: none;
}
.home-img{
    height: 100%;
    width: 100%;
    object-fit: cover;
    position: absolute;
    
}
.category{
    font-size: 1.5rem;
    line-height: 2.02rem;
    font-weight: 400;
    color: rgba(254, 254, 254, 0.75);
    --animate-duration:1s;
}
.title{
    font-family: 'Bebas Neue', Helvetica;
    color: #FBC02D;
    font-weight: 700;
    line-height: 4.75rem;
    font-size:4.75rem;
    --animate-duration:0.5s;

    
}
.subtitle{
    font-weight: 400;
    color: #FEFEFE;
    line-height: 2.02rem;
    font-size: 1.2rem;
    --animate-duration:0.8s;

}

.available{
    color: #FEFEFE;
}
.view-in-shop{
    margin-top: 3.125rem;
    width: 18.75rem;
    height: 4.375rem;
}
.current-slide,.total-slide{
    font-family: 'Bebas Neue', Helvetica;
    color: #FEFEFE;
    font-weight: 400;
    font-size:1.85rem;
    line-height: 2.25rem;
   
}

.previous-slide, .next-slide{
  font-size: 1.5rem;
    color:white;
    cursor: pointer;
}
.previous-slide:hover, .next-slide:hover{
  
    color:#FBC02D;
    cursor: pointer;
}
.slide-progress{
    height:0.375rem ;
}
.view-shop{
    font-weight: 500;
    color: #FEFEFE;
    line-height: 2.02rem;
    font-size: 1.5rem;
}
.hero-title{
    font-family: 'Bebas Neue', Helvetica;
    font-weight: 700;
    font-size: 4.75rem;
    line-height: 4.75rem;
}
.coming-soon-bg{
    background:url('~@/assets/img/spider_man_miles_morales.svg') ;
    background-size: cover;
    height: 100vh;
}
.coming-soon-title{
    font-weight: 700;
    font-size: 3.5rem;
    line-height: 3.5rem;
    color: #FBC02D;
}
.coming-soon-subtitle{
    font-weight: 700;
    font-size: 2.2rem;
    line-height: 2.2rem;
    color: #FBC02D;
}
.coming-soon-date{
    font-weight: 400;
    font-size: 1.5rem;
    line-height: 1.5rem;
    color: white;
}
.coming-soon-date span{
    font-weight: 500;
    font-size: 1.8rem;
    line-height: 1.8rem;
    color: white;
}
.featured-bg{
    background-image:url('~@/assets/img/cyberpunk.svg');
    background-repeat:none;
    background-size: cover;
    border-radius: 6px;

    height: 80vh;
}
.first-video,.second-video{
    height: 50%;
    width: 100%;
    background-repeat:none;
    background-size: cover;
    border-radius: 6px;
}
.first-video{
     background-image:url('~@/assets/img/a_man_is.svg');
    
}
.second-video{
     background-image:url('~@/assets/img/cyberpunk_2077.svg');
}
.play-btn{
    border-color: rgba(254, 254, 254, 0.8); 
    border-style:solid ;
    border-width:6px;
    border-radius: 50%;
    background: #303F9F;
    height: 3.125rem;
    width: 3.125rem;
    cursor: pointer;
}
.win-big-title{
    font-weight: 700;
    font-size: 3.2rem;
    line-height: 4rem;
    color: #FBC02D;
}
.win-big-bg{
    background: url('~@/assets/img/win_bg.svg');
    background-size: cover;
    background-repeat: no-repeat;
    border-radius: 6px;
}
.promo{
     font-weight: 400;
    font-size: 1.8rem;
    line-height: 2.56rem;
    color: white;
    margin-top: 3.25rem;
}
.promo span{
     font-weight: 800;
    font-size: 1.8rem;
    line-height: 2.56rem;
    color: #FBC02D;
}
.console{
    height: 13rem;
    margin-right: 3rem;
}
.footer-link{
    text-decoration: none;
    color: white;
    display: block;
    padding-top: 0.5rem;
    padding-bottom: 0.5rem;
   
    padding-right: 1rem;
}
.footer-ul{
    list-style-type: none;
}

.footer-title{
     font-weight: 800;
    font-size: 1.2rem;
    line-height: 2rem;
    color: white;
    margin-bottom:2.3rem;
}
.footer-brand{
    font-family: 'Bebas Neue', Helvetica;
    font-weight: 400;
    font-size: 3.75rem;
    line-height: 4.5rem;
    color: white;
}
.handles-bg{
    margin-bottom: 0.5rem;
}
.subscribe-btn{
    background: #303F9F;
    border-radius: 0px 6px 6px 0px;
    border: #303F9F;
}
.footer-bg{
    border-top-color:  #FBC02D;
    border-top-style: solid;
    border-top-width: 0.1875rem;
padding-top:40px ;
padding-bottom:48px ;
    border-bottom-color:  solid rgba(254, 254, 254, 0.5);;
    border-bottom-style: solid;
    border-bottom-width: 0.03125rem;
   
}
.login-btn{
    background: none;
    border: none;
}
.login-btn:hover{
    background: none;
    border: none;
}
</style>