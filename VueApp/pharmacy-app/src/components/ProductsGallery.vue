<template>
    <carousel-3d ref="newProductsExplorer" 
        :animationSpeed="1500"
        :autoplay="true"
        :autoplay-timeout="5000"
        :autoplayHoverPause="true"
        :border="0"
        :controls-visible="true"
        :controls-prev-html="'&#10092;'"
        :controls-next-html="'&#10093;'"
        :count="products.length"
        :display="3"
        :inverse-scaling="300"
        :perspective="0"
        :space="500"
        :height="340"
        :width="360"
        class="mt-4">
        <slide v-for="(product, i) in products" :index ="i" :key="i">
            <figure>
                <router-link :to="'/store/product/' + product.id">
                    <img :src="product.image" width="360" height="280" />
                    <figcaption>
                        <span class="title">{{product.name}}</span><br>
                        <span class="subtitle">{{getCost(product.cost)}} {{priceLabel}}</span>
                    </figcaption>
                </router-link>
            </figure>
        </slide>
    </carousel-3d>
</template>

<script>
import { Carousel3d, Slide } from 'vue-carousel-3d';

export default {
    name: 'ProductsGallery',
    components: {
        Carousel3d,
        Slide
    },
    props: {
        products: Array,
        priceLabel: String
    },
    updated() {
        this.$refs.newProductsExplorer.goSlide(this.$refs.newProductsExplorer.currentIndex);
    }
}
</script>

<style scoped>

.carousel-3d-container figure {
    margin:0;
}

.carousel-3d-slide {
    background-color: rgba(255,255,255,0);
}

.carousel-3d-container figcaption {
    position: absolute;
    background-color: rgba(255,255,255,0);
    color: #000;
    bottom: 0;
    min-width: 100%;
    text-align: center;
}

.title {
    font-size: 1.75rem;
}

.subtitle {
    font-size: 15px;
}
</style>