<template>
    <div class="main__top top">
        <div class="container">
            <div class="top__top">
                <h2 class="top__top-title">
                    New Movie
                </h2>
                <a href="https://www.netflix.com/de-en/" class="top__top-btn">
                    <span>See more</span>
                    <svg width="20" height="21" viewBox="0 0 20 21" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M7.5 4.66668L13.3333 10.5L7.5 16.3333" stroke="#fff" stroke-width="2"
                            stroke-linecap="round" stroke-linejoin="round" />
                    </svg>
                </a>
            </div>
            <swiper class="top__swiper top-swiper" :loop="true" :modules="modules" :slides-per-view="2" :space-between="30" navigation
                @swiper="onSwiper" @slideChange="onSlideChange" :breakpoints="{ 301:{ slidesPerView: 1 }, 901:{ slidesPerView:2 } }">
                <swiper-slide class="top-swiper__slide top-slide">
                    <NewSlide @sendInfoToParent="sendInfoToParent" :moviesInfo="this.dataOfmovies.value.titles[2]" />
                </swiper-slide>
                <swiper-slide class="top-swiper__slide top-slide">
                    <NewSlide @sendInfoToParent="sendInfoToParent" :moviesInfo="this.dataOfmovies.value.titles[22]" />
                </swiper-slide>
                <swiper-slide class="top-swiper__slide top-slide">
                    <NewSlide @sendInfoToParent="sendInfoToParent" :moviesInfo="this.dataOfmovies.value.titles[30]" />
                </swiper-slide>
                <swiper-slide class="top-swiper__slide top-slide">
                    <NewSlide @sendInfoToParent="sendInfoToParent" :moviesInfo="this.dataOfmovies.value.titles[42]" />
                </swiper-slide>
            </swiper>
        </div>
</div>
</template>

<script>
import { Navigation } from 'swiper';
import { Swiper, SwiperSlide } from 'swiper/vue';

import 'swiper/css';
import 'swiper/css/navigation';

import BigPosterSlide from './Big-poster-slide.vue';
import NewSlide from './New-slide.vue';

export default {
    inject: ['dataOfmovies'],
    components: {
        Swiper,
        SwiperSlide,
        BigPosterSlide,
        NewSlide,
    },
    name: 'New',
    setup() {
        const onSwiper = (swiper) => {
        };
        const onSlideChange = () => {
        };
        return {
            onSwiper,
            onSlideChange,
            modules: [Navigation],
        };
    },
    methods: {
        sendInfoToParent(elem) {
            this.$emit('sendInfoToParent', elem)
        }
    },
};
</script>

<style lang="scss">
@import './assets/scss/vars';
.top {
    @include adaptiv-value("padding-top", 70, 25, 1);
    @include adaptiv-value("margin-bottom", 90, 50, 1);
    &__top {
        display: flex;
        justify-content: space-between;
        align-items: center;
        @include adaptiv-value("margin-bottom", 45, 25, 1);
    }

    &__top-title {
        font-weight: 700;
        @include adaptiv-value("font-size", 36, 20, 1);
        @include adaptiv-value("line-height", 47, 26, 1);
        color: #fff;
    }

    &__top-btn {
        font-weight: 400;
        @include adaptiv-value("font-size", 18, 12, 1);
        @include adaptiv-value("line-height", 24, 18, 1);
        color: #fff;
        background: #BE123C;
        border-radius: 6px;
        @include adaptiv-value("padding-top", 8, 6, 1);
        @include adaptiv-value("padding-bottom", 8, 6, 1);
        @include adaptiv-value("padding-right", 16, 10, 1);
        @include adaptiv-value("padding-left", 16, 10, 1);
        max-width: 170px;
        display: flex;
        align-items: center;
        justify-content: center;
        @include adaptiv-value("gap", 8, 4, 1);
        border: 1px solid transparent;
        transition: border 0.3s, background 0.3s;
        &:hover {
            background: transparent;
            border: 1px solid #BE123C;
        }   
        svg {
            @include adaptiv-value("width", 20, 15, 1);
            @include adaptiv-value("height", 20, 15, 1);
        }
    }
}

.top-swiper {
    position: relative;
    @include adaptiv-value("padding-bottom", 100, 55, 1);
    .swiper-button-prev:after, .swiper-rtl .swiper-button-next:after {
        content: unset !important   
    }
    .swiper-button-next:after, .swiper-rtl .swiper-button-prev:after {
        content: unset !important   
    }
    .swiper-button-prev {
        border-radius: 5px;
        transform: rotate(180deg) translateX(150%);
        top: unset;
        bottom: 0 !important;
        position: absolute;
        bottom: unset;
        @include adaptiv-value("width", 50, 30, 1);
        @include adaptiv-value("height", 50, 30, 1);
        left: 50%;
        padding: 10px;
        background: #BE123C;
        object-fit: contain;
        border: 1px solid transparent;
        transition: border 0.3s, background 0.3s, filter 0.3s;
        &::before {
            content: '';
            top: 50%;
            left: 50%;
            background-image: url(../src/img/swiper-arrow.svg);
            transform: translateX(-50%) translateY(-50%);
            background-size: contain;
            @include adaptiv-value("width", 50, 30, 1);
            @include adaptiv-value("height", 50, 30, 1);
            max-width: 40px;
            max-height: 40px;
            position: absolute !important;
        }
        &:hover {
            border: 1px solid #BE123C;
            background: transparent;
        }
      
    }
    .swiper-button-next {
        border-radius: 5px;
        transform: translateX(150%) !important;
        top: unset;
        bottom: 0 !important;
        position: absolute;
        bottom: unset;
          @include adaptiv-value("width", 50, 30, 1);
        @include adaptiv-value("height", 50, 30, 1);
        right: 50%;
        padding: 10px;
        background: #BE123C;
        border: 1px solid transparent;
        transition: border 0.3s, background 0.3s, filter 0.3s;
        &::before {
            content: '';
            top: 50%;
            left: 50%;
            transform: translateX(-50%) translateY(-50%);
            background-image: url(../src/img/swiper-arrow.svg);
            background-size: contain;
            @include adaptiv-value("width", 50, 30, 1);
            @include adaptiv-value("height", 50, 30, 1);
            max-width: 40px;
            max-height: 40px;
            position: absolute !important;
        }
        &:hover {
            border: 1px solid #BE123C;
            background: transparent;
            filter: none;
        }
    }
}

.top-slide {
    width: 100%;
}

@media (max-width: 550px) {
    .top-swiper {
        .swiper-button-prev {
            left: 52%;
        }
        .swiper-button-next {
            right: 52%;
        }
    }
}


</style>