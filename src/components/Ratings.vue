<template>
    <div class="d-flex flex-row align-items-center">
        <div class="mr-3 rating">{{ratingValue}}</div>
        <b-icon class="mr-2 rating-star" icon="star-fill"></b-icon>
        <b-icon class="mr-2 rating-star" icon="star-fill"></b-icon>
        <b-icon class="mr-2 rating-star" icon="star-fill"></b-icon>
        <b-icon class="mr-2 rating-star" icon="star-fill"></b-icon>
        <b-icon class="mr-2 rating-star" icon="star-half"></b-icon>
    </div>
</template>

<script>
export default {
    props: {
        ratingValue: {
            type: String,
            default:'0' 
        },
    },
}
</script>

<style scoped>
.rating{
    font-weight: 400;
    line-height: 2.02rem;
    font-size: 1.2rem;
    color: #FEFEFE;

}
.rating-star{
    height: 1.5rem;
    color: #FBC02D;
}
</style>