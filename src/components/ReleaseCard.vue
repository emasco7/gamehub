<template>
  <div class="mt-5 d-flex flex-column release-bg">
        <img class="release-img" :src="require(`@/assets/img/${releaseImage}`)" :alt="releaseImage">
        <p class="m-0 mt-2 release-title ml-2">{{releaseTitle}}</p>
        <p class="m-0  mt-2 release-category  ml-2">{{releaseCategory}}</p>
        <Ratings v-if="hasRatings" class="ml-2  mt-2 release-rating" :ratingValue="releaseRating"/>
        <p class="m-0  mt-2 release-studio  ml-2">{{releaseStudio}}</p>
    </div>
</template>

<script>
import Ratings from './Ratings.vue';
export default {
    components: {
        Ratings,
    },
    props: {
        releaseImage: {
            type: String,
            default:'black_panther.svg' 
        },
        releaseTitle: {
            type: String,
            default:'Black Panther' 
        },
        releaseCategory: {
            type: String,
            default:'Action'
        },
        releaseRating: {
            type: String,
            default:'0'
        }, 
        releaseStudio: {
            type: String,
            default:'JINDU'
        },
        hasRatings: {
            type: Boolean,
            default:true
        },
        
    },
}
</script>

<style scoped>
.release-img{
    height: 16.8rem;
    /* width: 20.25rem; */
    border-top-left-radius: 0.375rem;
    border-top-right-radius: 0.375rem;
    object-fit: cover;
}
.release-title{
    font-weight: 500;
    line-height: 2rem;
    font-size: 1.2rem;
    color: #FBC02D;
}
.release-category{
    font-weight: 400;
    line-height: 2rem;
    font-size: 1.2rem;
    color: #FEFEFE;
}
.release-studio{
    font-weight: 400;
    font-size: 1.25rem;
    line-height: 1.65rem;
    color: rgba(254, 254, 254, 0.7);
}
.release-bg{
    background: #212122;
    box-shadow: 0px 4px 4px rgba(18, 18, 18, 0.16);
    border-radius: 6px;
     height: 28rem;
    /*width: 20.25rem; */
}
</style>