<template>
    <b-container>
        <b-row>
            <div class="slider__wrap" v-if="items.length > 0"> <!-- Если не будет проверки, то когда придут данные слайдер крашнется -->
                <VueSlickCarousel :arrows="true" :dots="true" :slidesToShow="3" :responsive="responsive">
                    <b-col v-for="(item, i) in items" :key="i">
                        <b-card
                            :title="item.title"
                            :img-src="item.src"
                            :img-alt="item.title"
                            img-top
                            tag="article"
                            style="max-width: 20rem;"
                            class="mb-2"
                        >
                            <b-card-text>{{item.descr}}</b-card-text>
                            <b-button href="#" variant="primary">Go somewhere</b-button>
                        </b-card>
                    </b-col>
                </VueSlickCarousel>
            </div>
        </b-row>
    </b-container>
</template>

<script>
import Vue from 'vue'
import VueSlickCarousel from 'vue-slick-carousel'
import 'vue-slick-carousel/dist/vue-slick-carousel.css'
// optional style for arrows & dots
import 'vue-slick-carousel/dist/vue-slick-carousel-theme.css'


  import 'bootstrap/dist/css/bootstrap.css'
  import 'bootstrap-vue/dist/bootstrap-vue.css'

import { BootstrapVue, IconsPlugin, BRow, BCol, BContainer } from 'bootstrap-vue'
Vue.use(BootstrapVue)
Vue.use(IconsPlugin)


export default {
    name: 'custom-slider',
    components: { VueSlickCarousel, BContainer, BRow, BCol },
    data() {
        return {
            items: [],
            responsive: [
                {
                    breakpoint: 1024,
                    settings: {
                        slidesToShow: 2,
                        arrows: true
                    }
                },
                {
                    breakpoint: 577,
                    settings: {
                        slidesToShow: 1,
                        arrows: true
                    }
                }
            ]
        }
    },
    methods: {
        async getItemsFromServer() {
            console.log('Request...');
            await setTimeout(() => {
                let dataFromApi = [  //C Сервера придут 5 объектов
                    {
                        title: 'Первый слайд',
                        src: 'https://picsum.photos/600/300/?image=25',
                        descr: 'Some quick example text to build on the card title and make up the bulk of the card'
                    },
                    {
                        title: 'Второй слайд',
                        src: 'https://wallpaperscave.ru/images/original/18/08-30/earth-seasons-fall-80316.jpg',
                        descr: 'Some quick example text to build on the card title and make up the bulk'
                    },
                    {
                        title: 'Третий слайд',
                        src: 'https://www.nastol.com.ua/download.php?img=201707/2560x1600/nastol.com.ua-238215.jpg',
                        descr: 'Some quick example text to build on the card title'
                    },
                    {
                        title: 'Четвёртый слайд',
                        src: 'https://avatars.mds.yandex.net/get-pdb/2863112/cd771fc7-648e-4fd5-bf85-6bf1b40fa1d8/s1200?webp=false',
                        descr: 'Some quick example title and make up the bulk of the card on the card '
                    },
                    {
                        title: 'Пятый слайд',
                        src: 'https://www.otdih.pro/images/mixx/2014-04/04a9939d76a98b48.jpg',
                        descr: 'Some quick example text to build on the card title and make up the bulk of the card quick example text to build on the card title and make up the bulk of the card'
                    },
                ]; 
                this.items = dataFromApi;
                console.log(this.items);
                console.log('Success...');
            }, 2000);
        }
    },
    created() {
        this.getItemsFromServer();
    }
}
</script>

<style scoped>
.slider__wrap {
    width: 100%;
    margin: 0px auto;
}

.card {
    width: 100% !important;
    color: #000;
    min-height: 450px;
}
.card img {
    height: 200px;
    object-fit: cover;
}
</style>