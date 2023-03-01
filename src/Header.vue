<template>
    <div class="header">
        <div class="header__top header-top">
            <div class="container">
                <div class="header-top__inner">
                    <a class="header-top__logo logo" href="#">
                        <img class="logo__img" src="./img/logo.png" alt="img">
                    </a>
                    <Search @sendInfoToParent="sendInfoToParent" />
                    <a href="https://www.netflix.com/gb/" class="header-top__singin header-top-singin" type="button">
                        <p class="header-top-singin__text">
                            Sign in
                        </p>
                    </a>
                </div>
            </div>
        </div>
        <div class="container-big">
            <BigPoster @sendInfoToParent="sendInfoToParent" />
        </div> 
    </div>
</template>

<script>

import BigPoster from './Big-poster.vue'
import Search from './Search.vue'

export default {
    name: 'Header',
    components: {
        BigPoster,
        Search
    },
    data() {
        return {
            inputValue: '',
        }
    },
    methods: {
        sendInfoToParent(elem) {
            this.$emit('sendInfoToParent', elem)
        },
    },
    inject: ['dataOfmovies'],
}

</script>

<style lang="scss">
@import './assets/scss/vars';

.header {
    width: 100%;
    position: relative;

}

.header-top {
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
    background: rgba(#000000, 0.7);
    @include adaptiv-value("height", 80, 68, 1);
    width: 100%;
    z-index: 100;
    left: 0;
    right: 0;
    position: fixed;

    &__singin {}
}

.header-top__inner {
    max-width: 1275px;
    margin: 0 auto;
    padding-left: 15px;
    padding-right: 15px;
    padding-top: 15px;
    padding-bottom: 15px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: absolute;
    left: 0;
    right: 0;
    width: 100%;
    z-index: 10;
    gap: 30px;
}

.logo {
    @include adaptiv-value("width", 185, 140, 1);
    &__img {
        @include adaptiv-value("width", 185, 140, 1);
    }
}

.header-top-singin {
    gap: 25px;
    display: flex;
    align-items: center;

    &__text {
        font-weight: 700;
        @include adaptiv-value("font-size", 16, 12, 1);
        @include adaptiv-value("line-height", 24, 14, 1);
        color: #FFFFFF;
        background: #BE123C;
        padding: 5px 10px;
        border-radius: 5px;
        border: 1px solid transparent;
        transition: background 0.3s, border 0.3s;
        &:hover {
            border: 1px solid #BE123C;
            background: transparent;
        }
    }

}
@media ( max-width: 900px ) {
    .header-top__inner {
        gap: 10px;
    }
    .header-top-form {
        display: flex;
        justify-content: center;
        align-items: center;
        @include adaptiv-value("width", 35, 25, 1);
        @include adaptiv-value("height", 36, 26, 1);
        background: #BE123C;
        margin-left: auto;
        border: 1px solid transparent;
        svg path {
            stroke: #fff;
        }
        transition: border 0.3s, background 0.3s;
        &:hover {
            background: transparent;
            border: 1px solid #BE123C;
        }
        .header-top-form__btn {
            width: 60%;
            height: 60%;
            left: 50%;
            right: unset;
            transform: translateX(-50%) translateY(-50%);
            svg {
                width: 100%;
                height: 100%;
            }
        }
    }
    .header-top-form__input {
        display: none;
    }
}
</style>