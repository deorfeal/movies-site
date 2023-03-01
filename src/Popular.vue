<template>
    <div class="main__popular popular">
        <div class="container">
            <h2 class="popular__title">
                Popular actors
            </h2>
            <div class="popular__inner">
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[16].jawSummary.cast[0].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[16].jawSummary.cast[1].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[16].jawSummary.cast[2].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[16].jawSummary.cast[3].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[16].jawSummary.cast[4].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[14].jawSummary.cast[0].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[14].jawSummary.cast[1].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[14].jawSummary.cast[2].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[14].jawSummary.cast[3].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[14].jawSummary.cast[4].name }}
                </a>

                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[12].jawSummary.cast[0].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[12].jawSummary.cast[1].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[12].jawSummary.cast[2].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[12].jawSummary.cast[3].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[12].jawSummary.cast[4].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[10].jawSummary.cast[0].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[10].jawSummary.cast[1].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[10].jawSummary.cast[2].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[10].jawSummary.cast[3].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[10].jawSummary.cast[4].name }}
                </a>

                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[8].jawSummary.cast[0].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[8].jawSummary.cast[1].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[8].jawSummary.cast[2].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[8].jawSummary.cast[3].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[8].jawSummary.cast[4].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[7].jawSummary.cast[0].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[7].jawSummary.cast[1].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[7].jawSummary.cast[2].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[7].jawSummary.cast[3].name }}
                </a>
                <a class="popular__link" href="https://www.netflix.com/gb/">
                    {{ this.dataOfmovies.value.titles[7].jawSummary.cast[4].name }}
                </a>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'Popular',
    inject: ['dataOfmovies'],
    data() {
        return {

        }
    },
}

</script>


<style lang="scss">
@import './assets/scss/vars';
.popular {

    &__title {
        font-weight: 700;
        @include adaptiv-value("font-size", 36, 20, 1);
        @include adaptiv-value("line-height", 47, 26, 1);
        color: #fff;
        text-align: center;
        margin-left: auto;
        margin-right: auto;
        @include adaptiv-value("margin-bottom", 45, 20, 1);
    }

    &__inner {
        display: flex;
        justify-content: center;
        @include adaptiv-value("gap", 20, 10, 1);
        @include adaptiv-value("margin-bottom", 80, 40, 1);
        flex-wrap: wrap;
    }

    &__link {
        background: #000;
        padding: 5px 10px;
        color: #fff;
        @include adaptiv-value("font-size", 18, 12, 1);
        @include adaptiv-value("line-height", 21, 14, 1);
        border: 1px solid transparent;
        transition: border 0.3s;
        &:hover {
            border: 1px solid #BE123C;
        }
    }
}
</style>