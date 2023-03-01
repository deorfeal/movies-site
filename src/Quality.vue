<template>
    <div class="main__quality quality">
        <div class="container">
            <h2 class="quality__title">
                Supported quality
            </h2>
            <div class="quality__inner">
                <a href="https://www.netflix.com/gb/" class="quality__link">
                    3D
                </a>
                <a href="https://www.netflix.com/gb/" class="quality__link">
                    51Audio
                </a>
                <a href="https://www.netflix.com/gb/" class="quality__link">
                    DolbyAtmos
                </a>
                <a href="https://www.netflix.com/gb/" class="quality__link">
                    DolbyVision
                </a>
                <a href="https://www.netflix.com/gb/" class="quality__link">
                    HDR
                </a>
                <a href="https://www.netflix.com/gb/" class="quality__link">
                    HDhasHD
                </a>
                <a href="https://www.netflix.com/gb/" class="quality__link">
                    UltraHD
                </a>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'Quality',
    data() {
        return {
        }
    },
}

</script>


<style lang="scss">
@import './assets/scss/vars';
.quality {

    &__title {
        font-weight: 700;
        @include adaptiv-value("font-size", 36, 20, 1);
        @include adaptiv-value("line-height", 47, 26, 1);
        color: #fff;
        text-align: center;
        margin-left: auto;
        margin-right: auto;
        @include adaptiv-value("margin-bottom", 30, 20, 1);
    }

    &__inner {
        display: flex;
        justify-content: center;
        @include adaptiv-value("gap", 20, 10, 1);
        @include adaptiv-value("margin-bottom", 30, 25, 1);
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