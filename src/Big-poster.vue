<template>
    <div class="header__bottom header-bottom">
       
        <swiper class="header-bottom__swiper header-bottom-swiper" :modules="modules" :slides-per-view="1"
            :space-between="0"  :autoplay="{ delay: 3000 }" :pagination="{ clickable: true, }"  :loop="true"  @swiper="onSwiper" @slideChange="onSlideChange">
            <swiper-slide class="header-bottom-swiper__slide header-slide">
                <BigPosterSlide  @sendInfoToParent="sendInfoToParent" :moviesInfo="this.dataOfmovies.value.titles[44]" />
            </swiper-slide>
            <swiper-slide class="header-bottom-swiper__slide header-slide">
                <BigPosterSlide  @sendInfoToParent="sendInfoToParent" :moviesInfo="this.dataOfmovies.value.titles[33]" />
            </swiper-slide>
            <swiper-slide class="header-bottom-swiper__slide header-slide">
                <BigPosterSlide  @sendInfoToParent="sendInfoToParent" :moviesInfo="this.dataOfmovies.value.titles[34]" />
            </swiper-slide>
        </swiper>
    </div>
</template>

<script>

import { Pagination, Autoplay } from 'swiper';
import { Swiper, SwiperSlide } from 'swiper/vue';

import 'swiper/css';
import 'swiper/css/pagination';

import BigPosterSlide from './Big-poster-slide.vue';

export default {
    components: {
        Swiper,
        SwiperSlide,
        BigPosterSlide,
    },
    name: 'Big-poster',
    data() {
        return {
            lastIdOfSlide: 0,
        }
    },
    setup() {
        const onSwiper = (swiper) => {
        };
        const onSlideChange = () => {
        };
        return {
            onSwiper,
            onSlideChange,
            modules: [Pagination, Autoplay],
        };
    },
    inject: ['dataOfmovies'],
    mounted() {
    },
    methods: {
        sendInfoToParent(elem) {
            this.$emit('sendInfoToParent', elem)
        }
    }
};
</script>

<style lang="scss">
@import './assets/scss/vars';
.header-bottom {
    position: relative;
    @include adaptiv-value("padding-top", 80, 65, 1);
}

.header-slide {
    display: flex;
    flex-direction: column;
    justify-content: center;
    @include adaptiv-value("min-height", 720, 500, 1);
}

.header-bottom-swiper {
    background: rgba(0, 0, 0, 0.4);
    border-radius: 0 0 20px 20px;

    .swiper-wrapper {}

    .swiper-pagination {
        gap: 10px;
        display: flex;
        flex-direction: column;
        height: 100%;
        right: 25px;
        left: unset;
        width: 8px;
        justify-content: center;
        align-items: flex-end;
    }

    .swiper-pagination-bullet {
        height: 30px;
        background: #BE123C !important;
        border-radius: 5px;
    }
}
@media(max-width: 1650px) {
    .header-bottom-swiper {
        border-radius: 0;
    }
}

@media (max-width: 550px) {
    .header-bottom-swiper .swiper-pagination {
        width: 100%;
        height: 8px;
        bottom: 50px;
        left: 50%;
        top: unset;
        right: unset;
        position: absolute;
        flex-direction: row;
        transform: translateX(-50%);
    }
    .header-bottom-swiper .swiper-pagination-bullet {
        width: 30px;
        height: 8px;
    }
}
</style>