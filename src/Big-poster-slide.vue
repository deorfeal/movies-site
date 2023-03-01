<template>
    <div class="header-slide__wrapper">
        <div class="header-slide__show">
            <img class="header-slide__img" :src="this.moviesInfo.jawSummary.backgroundImage.url" alt="img">
        </div>
        <div class="header-slide__inner">
            <div class="header-slide__box header-slide-box">
                <h2 class="header-slide-box__title">
                    {{this.moviesInfo.jawSummary.title}}
                </h2>
                <div class="header-slide-box__row header-slide-box-row">
                    <p class="header-slide-box-row__text">
                        Tags:
                    </p>
                    <div class="header-slide-box-row__box">
                        <a v-for="item of this.moviesInfo.jawSummary.tags" :key="item.id" href="#" class="header-slide-box-row__box-tag">
                            {{ item.name }}
                        </a>
                    </div>
                </div>
                <p class="header-slide-box__text">
                   {{ this.moviesInfo.jawSummary.synopsis }}
                </p>
                <a @click="sendInfoToParent" data-fancybox href="#more-info" class="header-slide-box__trailer">
                    <!-- <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path fill-rule="evenodd" clip-rule="evenodd"
                            d="M10 18C14.4183 18 18 14.4183 18 10C18 5.58172 14.4183 2 10 2C5.58172 2 2 5.58172 2 10C2 14.4183 5.58172 18 10 18ZM9.5547 7.16795C9.24784 6.96338 8.8533 6.94431 8.52814 7.11833C8.20298 7.29235 8 7.63121 8 8V12C8 12.3688 8.20298 12.7077 8.52814 12.8817C8.8533 13.0557 9.24784 13.0366 9.5547 12.8321L12.5547 10.8321C12.8329 10.6466 13 10.3344 13 10C13 9.66565 12.8329 9.35342 12.5547 9.16795L9.5547 7.16795Z"
                            fill="white" />
                    </svg> -->
                    <p class="header-slide-box__trailer-text">
                        More info
                    </p>
                </a>
            </div>
        </div>
</div>
</template>
<script>

export default {
    name: 'Big-poster-slide',
    data() {
        return {

        }
    },
    props: ['moviesInfo'],
    mounted() {
    },
    methods: {
        sendInfoToParent() {
            this.$emit('sendInfoToParent', this.moviesInfo)
        }
    },
};
</script>

<style lang="scss">
@import './assets/scss/vars';
.header-slide {
    position: relative;

    &__show {
        &::before {
            content: '';
            width: 100%;
            height: 100%;
            background: rgba(#000000, 0.5);
            position: absolute;
            top: 0;
            bottom: 0;
            right: 0;
            left: 0;
        }
    }

    &__img {
        position: absolute;
        z-index: -1;
        width: 85%;
        height: 85%;
        top: 50%;
        bottom: 0;
        left: 50%;
        right: 0;
        object-fit: cover;
        transform: translateX(-50%) translateY(-50%);
        border-radius: 0 0 20px 20px;
    }

    &__inner {
        max-width: 1275px;
        margin-left: auto;
        margin-right: auto;
        padding-left: 15px;
        padding-right: 15px;
        z-index: 10;
        position: relative;
    }
}

.header-slide-box {
    display: flex;
    flex-direction: column;
    @include adaptiv-value("gap", 15, 10, 1);

    &__title {
        color: #FFFFFF;
        max-width: 400px;
        @include adaptiv-value("font-size", 48, 30, 1);
        @include adaptiv-value("line-height", 56, 38, 1);
    }

    &__text {
        max-width: 295px;
        font-weight: 500;
        color: #FFFFFF;
        @include adaptiv-value("font-size", 14, 12, 1);
        @include adaptiv-value("line-height", 18, 16, 1);
    }

    &__trailer {
        background: #BE123C;
        border-radius: 6px;
        @include adaptiv-value("padding-top", 8, 8, 1);
        @include adaptiv-value("padding-bottom", 8, 8, 1);
        @include adaptiv-value("padding-right", 16, 8, 1);
        @include adaptiv-value("padding-left", 16, 8, 1);
        @include adaptiv-value("max-width", 170, 120, 1);
        display: flex;
        align-items: center;
        gap: 8px;
        justify-content:center;
        border: 1px solid transparent;
        transition: border 0.3s, background 0.3s;
        &:hover {
            background: transparent;
            border: 1px solid #BE123C;
        }

    }

    &__trailer-text {
        @include adaptiv-value("font-size", 14, 12, 1);
        @include adaptiv-value("line-height", 24, 15, 1);
        text-transform: uppercase;
        color: #FFFFFF;
    }
}

.header-slide-box-row {
    display: flex;
    gap: 10px;
    display: flex;
    align-items: center;
    &__text {
        color: #fff;
        font-weight: 700;
        line-height: 23px;
        background: #000;

        @include adaptiv-value("font-size", 18, 16, 1);
        @include adaptiv-value("padding-top", 5, 3, 1);
        @include adaptiv-value("padding-bottom", 5, 3, 1);
        @include adaptiv-value("padding-right", 10, 8, 1);
        @include adaptiv-value("padding-left", 10, 8, 1);
    }

    &__box {
        display: flex;
        gap: 10px;
        align-items: center;
    }

    &__box-tag {
        font-weight: 400;
        @include adaptiv-value("font-size", 12, 11, 1);
        line-height: 14px;
        color: #9CA3AF;
    }

    &__rate {
        display: flex;
        gap: 10px;
        align-items: center;
    }

    &__rate-img {
        width: 35px;
        height: 17px;
    }

    &__rate-text {
        font-weight: 400;
        font-size: 12px;
        line-height: 12px;
        color: #FFFFFF;
    }

    &__procents {
        display: flex;
        align-items: center;
        gap: 10px;
    }

    &__procents-img {
        width: 16px;
        height: 16px;
    }

    &__procents-text {
        font-weight: 400;
        font-size: 12px;
        line-height: 12px;
        color: #FFFFFF;
    }
}
@media (max-width: 1550px) {
    .header-slide__img {
        width: 90%;
    }
    // .header-slide-box {
    //    max-width: 90%;
    //    width: 90%;
    //    margin-left: auto;
    //    margin-right: auto;
    // }
}

@media (max-width: 1450px) {
    .header-slide__img {
        width: 98%;
    }
}

@media (max-width: 1300px) {
    .header-slide__img {
        width: 100%;
        border-radius: 0;
        height: 90%;
    }
}

@media (max-width: 1300px) {
    // .header-slide-box {
    //    max-width: 80%;
    //    width: 80%;
    //    margin-left: auto;
    //    margin-right: auto;
    // }
}
</style>