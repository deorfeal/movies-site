<template>
    <div class="big-wrapper" v-if="dataIsDone">
        <Header @sendInfoToParent="getInfoFromChildrens" @sendInfoToParentNewPageInfo="getInfoFromChildrensPage" />
        <div class="wrapper">
            <div class="main">
                <Top @sendInfoToParent="getInfoFromChildrens" />
                <Quality /> 
                <New @sendInfoToParent="getInfoFromChildrens" />
                <Popular /> 
            </div>
            <Footer />
        </div>
        <Teleport to="#biggest-wrapper">
            <div class="main__more-info more-info" id="more-info" v-if="this.filmInfo.value != ''">
                <div class="more-info__inner">
                    <h2 class="more-info__title">
                        {{ this.filmInfo.value.jawSummary.title }}
                    </h2>
                    <p class="more-info__date">
                        {{ this.filmInfo.value.availability.availabilityDate }}
                    </p>
                    <p class="more-info__text">
                        {{ this.filmInfo.value.jawSummary.currentContextualSynopsis.text }}
                    </p>
                    <div class="more-info__row">
                        <p class="more-info__row-text">
                            Cast:
                        </p>
                        <a v-for="item of this.filmInfo.value.jawSummary.cast" :key="item.id" class="more-info__row-cast"
                            href="https://www.netflix.com/gb/">
                            {{ item.name }}
                        </a>
                    </div>
                    <div class="more-info__tags">
                        <p class="more-info__tags-text">
                            Tags:
                        </p>
                        <a v-for="item of this.filmInfo.value.jawSummary.tags" :key="item.id" class="more-info__tag"
                            href="https://www.netflix.com/gb/">
                            {{ item.name }}
                        </a>
                    </div>
                    <div class="more-info__creators">
                        <p class="more-info__creators-text">
                            Creators:
                        </p>
                        <template v-for="item of this.filmInfo.value.jawSummary.creators">
                            <a :key="item.id" v-if="item != undefined" class="more-info__creators-creator" href="https://www.netflix.com/gb/">
                                {{ item.name }}
                            </a>
                        </template>
                    </div>
                    <div class="more-info__directors">
                        <p class="more-info__directors-text">
                            Directors:
                        </p>
                        <a v-for="item of this.filmInfo.value.jawSummary.directors" :key="item.id"
                            class="more-info__directors-director" href="https://www.netflix.com/gb/">
                            {{ item.name }}
                        </a>
                    </div>
                    <div class="more-info__genres">
                        <p class="more-info__genres-text">
                            Genres:
                        </p>
                        <a v-for="item of this.filmInfo.value.jawSummary.genres" :key="item.id"
                            class="more-info__genres-genre" href="https://www.netflix.com/gb/">
                            {{ item.name }}
                        </a>
                    </div>
                    <div class="more-info__quality">
                        <p class="more-info__quality-text">
                            Quality:
                        </p>
                        <p class="more-info__quality-current">
                            {{ this.filmInfo.value.jawSummary.delivery.quality }}
                        </p>
                    </div>
                    <div class="more-info__episodes">
                        <p class="more-info__episodes-text">
                            Episodes:
                        </p>
                        <p class="more-info__episodes-count">
                            {{ this.filmInfo.value.jawSummary.episodeCount }}
                        </p>
                    </div>
                    <div class="more-info__seasons">
                        <p class="more-info__seasons-text">
                            Seasons:
                        </p>
                        <p class="more-info__seasons-count">
                            {{ this.filmInfo.value.jawSummary.seasonCount }}
                        </p>
                    </div>
                    <div class="more-info__type">
                        <p class="more-info__type-text">
                            {{ this.filmInfo.value.jawSummary.type }}
                        </p>
                    </div>
                    <a class="more-info__link" href="https://www.netflix.com/gb/">
                        Watch
                    </a>
                    <a class="more-info__subsribe" href="https://www.netflix.com/gb/">
                        Subsribe
                    </a>
                </div>
                <img class="more-info__img" :src="this.filmInfo.value.jawSummary.backgroundImage.url" alt="bg">
            </div>
        </Teleport>  
    </div>
</template>

<script>

import Header from './Header.vue'
import Top from './Top.vue';
import New from './New.vue';
import Popular from './Popular.vue';
import Footer from './Footer.vue';
import Quality from './Quality.vue';

export default {
    name: 'Main',
    components: {
        Header,
        New,
        Top,
        Footer,
        Popular,
        Quality,
    },
    data() {
        return {
            dataOfmovies: { value: '' },
            dataIsDone: false,
            filmInfo: { value: '' },
        }
    },
    async mounted() {
        const options = {
            method: 'GET',
            headers: {
                'X-RapidAPI-Key': '9f5262ae0dmsh99f7de1c78c571fp1d16dejsn25a697130124',
                'X-RapidAPI-Host': 'netflix54.p.rapidapi.com'
            }
        };

        fetch('https://netflix54.p.rapidapi.com/search/?query=stranger&offset=0&limit_titles=50&limit_suggestions=20&lang=en', options)
            .then(response => response.json())
            .then(response => this.dataOfmovies.value = response)
            .catch(err => console.error(err));
    },
    watch: {
        dataOfmovies: {
            handler() {
                this.dataIsDone = true
            },
            deep: true,
        },
    },
    provide() {
        return {
            dataOfmovies: this.dataOfmovies,
        }
    },
    methods: {
        getInfoFromChildrens(elem) {
            this.filmInfo.value = elem
        },
    }
}

</script>


<style lang="scss">
@import './assets/scss/vars';
.big-wrapper {
    // max-width: 1440px;
    // margin-left: auto;
    // margin-right: auto;
}

// // 

.fancybox-content {
    background: unset;
}

.more-info {
    background: #000;
    color: #fff;
    display: none;
    // max-width: 1700px;
    // min-width: 1700px;
    max-height: 90%;
    min-width: 90%;
    max-width: 90%;
    z-index: 100;
    @include adaptiv-value("border-radius", 20, 5, 1);
    @include adaptiv-value("padding-top", 50, 40, 1);
    @include adaptiv-value("padding-bottom", 50, 40, 1);
    @include adaptiv-value("padding-right", 50, 20, 1);
    @include adaptiv-value("padding-left", 50, 20, 1);
    display: flex;
    justify-content: space-between;
    align-items: center;

    &__link {
        background: #000;
        @include adaptiv-value("padding-top", 15, 10, 1);
        @include adaptiv-value("padding-bottom", 15, 10, 1);
        @include adaptiv-value("padding-right", 10, 10, 1);
        @include adaptiv-value("padding-left", 10, 10, 1);
        color: #fff;
        @include adaptiv-value("font-size", 18, 12, 1);
        @include adaptiv-value("line-height", 21, 14, 1);
        border: 1px solid #BE123C;
        transition: background 0.3s;
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        background: #BE123C;

        &:hover {
            background: transparent;
        }
    }

    &__subsribe {
        background: #000;
        @include adaptiv-value("padding-top", 15, 10, 1);
        @include adaptiv-value("padding-bottom", 15, 10, 1);
        @include adaptiv-value("padding-right", 10, 10, 1);
        @include adaptiv-value("padding-left", 10, 10, 1);
        color: #fff;
        @include adaptiv-value("font-size", 18, 12, 1);
        @include adaptiv-value("line-height", 21, 14, 1);
        border: 1px solid #BE123C;

        transition: background 0.3s;
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;

        &:hover {
            background: #BE123C;
        }
    }

    &__inner {
        display: flex;
        flex-direction: column;
        @include adaptiv-value("gap", 25, 15, 1);
        max-width: 46%;
        align-items: flex-start;
    }

    &__img {
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        width: 50%;
        height: 100%;
        object-fit: cover;
        z-index: -1;
    }

    &::before {
        content: '';
        position: absolute;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        width: 100%;
        height: 100%;
        border-radius: 20px;
        background: rgba(0, 0, 0, 1);
        z-index: -1;
    }

    &__title {
        @include adaptiv-value("font-size", 48, 18, 1);
        @include adaptiv-value("line-height", 56, 22, 1);
        color: #FFFFFF;
        max-width: 400px;
        text-align: left;
        margin-right: auto;
    }

    &__date {
        font-weight: 500;
        @include adaptiv-value("font-size", 17, 13, 1);
        @include adaptiv-value("line-height", 18, 16, 1);
        color: #FFFFFF;
    }

    &__text {
        font-weight: 500;
        @include adaptiv-value("font-size", 14, 12, 1);
        @include adaptiv-value("line-height", 18, 16, 1);
        color: #FFFFFF;
        max-width: 400px;
        text-align: left;
    }

    &__row {
        display: flex;
        gap: 10px;
        flex-wrap: wrap;
        align-items: center;
    }

    &__row-text {
        font-weight: 500;
        @include adaptiv-value("font-size", 20, 13, 1);
        @include adaptiv-value("line-height", 24, 16, 1);
        color: #FFFFFF;
        max-width: 400px;
        text-align: left;
    }

    &__row-cast {
        background: #000;
        padding: 5px 10px;
        color: #fff;
        @include adaptiv-value("font-size", 18, 12, 1);
        @include adaptiv-value("line-height", 21, 14, 1);
        border: 1px solid #BE123C;
        transition: background 0.3s;

        &:hover {
            background: #BE123C;
        }
    }

    &__tags {
        display: flex;
        gap: 10px;
        flex-wrap: wrap;
        align-items: center;
    }

    &__tags-text {
        font-weight: 500;
        @include adaptiv-value("font-size", 20, 13, 1);
        @include adaptiv-value("line-height", 24, 16, 1);
        color: #FFFFFF;
        max-width: 400px;
        text-align: left;
    }

    &__tag {
        background: #000;
        padding: 5px 10px;
        color: #fff;
        @include adaptiv-value("font-size", 18, 12, 1);
        @include adaptiv-value("line-height", 21, 14, 1);
        border: 1px solid #BE123C;
        transition: background 0.3s;

        &:hover {
            background: #BE123C;
        }
    }

    &__creators {
        display: flex;
        gap: 10px;
        flex-wrap: wrap;
        align-items: center;
    }

    &__creators-text {
        font-weight: 500;
        @include adaptiv-value("font-size", 20, 13, 1);
        @include adaptiv-value("line-height", 24, 16, 1);
        color: #FFFFFF;
        max-width: 400px;
        text-align: left;
    }

    &__creators-creator {
        background: #000;
        padding: 5px 10px;
        color: #fff;
        @include adaptiv-value("font-size", 18, 12, 1);
        @include adaptiv-value("line-height", 21, 14, 1);
        border: 1px solid #BE123C;
        transition: background 0.3s;

        &:hover {
            background: #BE123C;
        }
    }

    &__directors {
        display: flex;
        gap: 10px;
        flex-wrap: wrap;
        align-items: center;
    }

    &__directors-text {
        font-weight: 500;
        @include adaptiv-value("font-size", 20, 13, 1);
        @include adaptiv-value("line-height", 24, 16, 1);
        color: #FFFFFF;
        max-width: 400px;
        text-align: left;
    }

    &__directors-director {
        background: #000;
        padding: 5px 10px;
        color: #fff;
        @include adaptiv-value("font-size", 18, 12, 1);
        @include adaptiv-value("line-height", 21, 14, 1);
        border: 1px solid #BE123C;
        transition: background 0.3s;

        &:hover {
            background: #BE123C;
        }
    }

    &__genres {
        display: flex;
        gap: 10px;
        flex-wrap: wrap;
        align-items: center;
    }

    &__genres-text {
        font-weight: 500;
        @include adaptiv-value("font-size", 20, 13, 1);
        @include adaptiv-value("line-height", 24, 16, 1);
        color: #FFFFFF;
        max-width: 400px;
        text-align: left;
    }

    &__genres-genre {
        background: #000;
        padding: 5px 10px;
        color: #fff;
        @include adaptiv-value("font-size", 18, 12, 1);
        @include adaptiv-value("line-height", 21, 14, 1);
        border: 1px solid #BE123C;
        transition: background 0.3s;

        &:hover {
            background: #BE123C;
        }
    }

    &__quality {
        display: flex;
        gap: 10px;
        flex-wrap: wrap;
        align-items: center;
    }

    &__quality-text {
        font-weight: 500;
        @include adaptiv-value("font-size", 20, 13, 1);
        @include adaptiv-value("line-height", 24, 16, 1);
        color: #FFFFFF;
        max-width: 400px;
        text-align: left;

    }

    &__quality-current {
        font-weight: 500;
        @include adaptiv-value("font-size", 14, 12, 1);
        @include adaptiv-value("line-height", 18, 16, 1);
        color: #FFFFFF;
        max-width: 400px;
        text-align: left;
        background: #BE123C;
        padding: 5px 10px;
    }

    &__episodes {
        display: flex;
        gap: 10px;
        flex-wrap: wrap;
        align-items: center;
    }

    &__episodes-text {
        font-weight: 500;
        @include adaptiv-value("font-size", 20, 13, 1);
        @include adaptiv-value("line-height", 24, 16, 1);
        color: #FFFFFF;
        max-width: 400px;
        text-align: left;
    }

    &__episodes-count {
        font-weight: 500;
        @include adaptiv-value("font-size", 14, 12, 1);
        @include adaptiv-value("line-height", 18, 16, 1);
        color: #FFFFFF;
        max-width: 400px;
        text-align: left;

        background: #BE123C;
        padding: 5px 10px;
    }

    &__seasons {
        display: flex;
        gap: 10px;
        flex-wrap: wrap;
        align-items: center;
    }

    &__seasons-text {
        font-weight: 500;
        @include adaptiv-value("font-size", 20, 13, 1);
        @include adaptiv-value("line-height", 24, 16, 1);
        color: #FFFFFF;
        max-width: 400px;
        text-align: left;
    }

    &__seasons-count {
        font-weight: 500;
        @include adaptiv-value("font-size", 14, 12, 1);
        @include adaptiv-value("line-height", 18, 16, 1);
        color: #FFFFFF;
        max-width: 400px;
        text-align: left;

        background: #BE123C;
        padding: 5px 10px;
    }

    &__type {}

    &__type-text {
        background: #000;
        padding: 5px 10px;
        color: #fff;
        @include adaptiv-value("font-size", 18, 12, 1);
        @include adaptiv-value("line-height", 21, 14, 1);
        border: 1px solid #BE123C;
        transition: background 0.3s;
    }
}

@media (min-width: 1920px) {
    .more-info {
        max-width: 1750px !important;
        min-width: unset !important;
    }
}

@media (max-width: 1500px) {
    .more-info__img {
        width: 30%;
    }
    .more-info__inner {
        max-width: 60%;
    }
}
@media (max-width: 1200px) {
    .more-info__img {
        width: 20%;
    }
    .more-info__inner {
        max-width: 75%;
    }
}

@media (max-width: 900px) {
    .more-info__img {
        width: 0%;
    }
    .more-info__inner {
        max-width: 100%;
    }
}

@media (max-width: 700px) {
    .more-info {
        max-width: 95%;
        max-height: 95%;
        min-width: 95%;
    }
}
</style>