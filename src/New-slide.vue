<template>
    <div class="top-slide__box top-slide-box">
        <a @click="sendInfoToParent" data-fancybox href="#more-info" class="top-slide-box__top top-slide-box-top">
            <div class="top-slide-box-top__row">
                <p class="top-slide-box-top__row-tet">
                    {{ this.moviesInfo.summary.type }}
                </p>
                <button class="top-slide-box-top__row-favorite">
                    <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path fill-rule="evenodd" clip-rule="evenodd"
                            d="M3.17157 5.48284C4.73367 3.96185 7.26633 3.96185 8.82842 5.48284L9.99999 6.62359L11.1716 5.48284C12.7337 3.96185 15.2663 3.96185 16.8284 5.48284C18.3905 7.00383 18.3905 9.46984 16.8284 10.9908L9.99999 17.6396L3.17157 10.9908C1.60948 9.46984 1.60948 7.00383 3.17157 5.48284Z"
                            fill="#D1D5DB" />
                    </svg>
                </button>
            </div>
            <img class="top-slide-box-top__img" :src="this.moviesInfo.jawSummary.backgroundImage.url" alt="img">
            <a @click="sendInfoToParent" data-fancybox href="#more-info" class="top-slide-box-top__more">
                MORE INFO
            </a>
        </a>
        <div class="top-slide-box__info">
            <span class="top-slide-box__info-date">
                {{ this.moviesInfo.availability.availabilityDate }}
            </span>
        </div>
        <a href="https://www.netflix.com/gb/" class="top-slide-box__info-name">
            {{ this.moviesInfo.jawSummary.title }}
        </a>
        <div class="top-slide-box__row top-slide-box-row">
            <div class="top-slide-box-row__box">
                <p class="top-slide-box-row__box-text">
                        Tags:
                </p>
                <a v-for="item of this.moviesInfo.jawSummary.tags" :key="item.id" href="https://www.netflix.com/gb/" class="top-slide-box-row__box-tag">
                    {{ item.name }}
                </a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'New-slide',
    props: ['moviesInfo'],
    methods: {
        sendInfoToParent() {
            this.$emit('sendInfoToParent', this.moviesInfo)
        }
    },
};
</script>


<style lang="scss">
@import './assets/scss/vars';
.top-slide {}

.top-slide-box {
    display: flex;
    flex-direction: column;
    gap: 7px;

    &__info {
        font-weight: 700;
        color: #9CA3AF;

        @include adaptiv-value("font-size", 12, 11, 1);
        @include adaptiv-value("line-height", 16, 14, 1);
    }

    &__info-date {}

    &__info-year {}

    &__info-name {
        font-weight: 700;
        color: #fff;
        align-self: flex-start;
        background: transparent;
        border-radius: 5px;
        padding: 5px 0;
        transition: background 0.3s, padding 0.3s;
        @include adaptiv-value("font-size", 18, 16, 1);
        @include adaptiv-value("line-height", 23, 20, 1);
        &:hover {
            padding: 5px 10px;
            background: #BE123C;
        }
    }
    &__row {}
}

.top-slide-box-top {
    width: 100%;
    @include adaptiv-value("height", 370, 180, 1);
    position: relative;
    @include adaptiv-value("margin-bottom", 12, 8, 1);
    &::before {
        content: '';
        background: rgba( #9CA3AF, 0.0);
        z-index: 10;
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        width: 100%;
        height: 100%;
        border-radius: 20px 20px 0 0;
        transition: background 0.3s;
    }
    &__more {
        @include adaptiv-value("font-size", 14, 12, 1);
        @include adaptiv-value("line-height", 24, 20, 1);
        text-transform: uppercase;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translateX(-50%) translateY(-50%);
        color: #FFFFFF;
        background: #BE123C;
        border-radius: 6px;
        @include adaptiv-value("padding-top", 8, 8, 1);
        @include adaptiv-value("padding-bottom", 8, 8, 1);
        @include adaptiv-value("padding-right", 40, 20, 1);
        @include adaptiv-value("padding-left", 40, 20, 1);
        max-width: 170px;
        display: flex;
        align-items: center;
        gap: 8px;
        justify-content: center;
        border: 1px solid transparent;
        transition: border 0.3s, background 0.3s;
        z-index: 50;
        opacity: 0;
        transition: opacity 0.3s, border 0.3s, background 0.3s;
        &:hover {
            border: 1px solid #BE123C;
            background: transparent;
        }
    }
    &:hover {
        &::before {
            content: '';
            background: rgba( #9CA3AF, 0.2);
        }
        .top-slide-box-top__more {
            opacity: 1;
        }
    }

    &__row {
        position: absolute;
        top: 0;
        right: 0;
        width: 100%;
        height: 100%;
        z-index: 15;
    }

    &__row-tet {
        position: absolute;
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
        z-index: 10;
        color: #000;
        background: rgba(243, 244, 246, 0.5);

        @include adaptiv-value("font-size", 14, 12, 1);
        @include adaptiv-value("right", 15, 10, 1);
        @include adaptiv-value("bottom", 15, 10, 1);
        @include adaptiv-value("padding-top", 10, 5, 1);
        @include adaptiv-value("padding-bottom", 10, 5, 1);
        @include adaptiv-value("padding-right", 15, 10, 1);
        @include adaptiv-value("padding-left", 15, 10, 1);
    }

    &__row-favorite {
        z-index: 15;
        position: absolute;
        @include adaptiv-value("width", 30, 25, 1);
        @include adaptiv-value("height", 30, 25, 1);
        background: rgba(243, 244, 246, 0.5);
        backdrop-filter: blur(1px);
        @include adaptiv-value("top", 15, 10, 1);
        @include adaptiv-value("right", 15, 10, 1);
        z-index: 1;
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 100%;
        z-index: 10;
        transition: background 0.3s;
        svg {
            @include adaptiv-value("width", 20, 15, 1);
            @include adaptiv-value("height", 20, 15, 1);
        }
        svg path {
            fill: #000;
            transition: fill 0.3s;
        }
        &:hover {
            background: #000;
            svg path {
                fill: #BE123C;
            }
        }
    }

    &__img {
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
        @include adaptiv-value("border-top-left-radius", 20, 10, 1);
        @include adaptiv-value("border-top-right-radius", 20, 10, 1);
        right: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
    }
}

.top-slide-box-row {
    display: flex;
    align-items: center;
    &__box {
        display: flex;
        @include adaptiv-value("gap", 10, 6, 1);
        align-items: center;
    }
    &__box-text {
        color: #fff;
        font-weight: 700;
        background: #000;
        padding: 5px 10px;

        @include adaptiv-value("font-size", 18, 16, 1);
        @include adaptiv-value("line-height", 23, 20, 1);
    }
    &__box-tag {
        font-weight: 400;
        @include adaptiv-value("font-size", 12, 11, 1);
        @include adaptiv-value("line-height", 16, 14, 1);
        color: #9CA3AF;
        transition: color 0.3s;
        &:hover {
            color: #fff;
        }
    }
    &__imdb {
        display: flex;
        align-items: center;
        gap: 10px;
    }

    &__imdb-img {
        width: 35px;
        height: 17px;
    }

    &__imdb-rait {
        font-weight: 400;
        font-size: 12px;
        line-height: 12px;
        color: #9CA3AF;

    }

    &__tomatoes {
        gap: 10px;
        display: flex;
        align-items: center;
    }

    &__tomatoes-img {
        width: 16px;
        height: 16px;
    }

    &__tomatoes-rait {
        font-weight: 400;
        font-size: 12px;
        line-height: 12px;
        color: #9CA3AF;

    }
}
</style>