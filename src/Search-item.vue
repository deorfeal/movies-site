<template>
    <a class="header-top-form__list-link" data-fancybox href="#more-info" @click="sendInfoToParent">
        {{ this.word.value[0] }}
    </a>
</template>
  
<script>
export default {
    name: "Search-item.vue",
    props: ['word', 'moviesInfo'],
    data() {
        return {
        };
    },
    mounted() {
        // console.log( this.moviesInfo, this.word.id )
    },
    methods: {
        sendInfoToParent() {
            this.$emit('sendInfoToParent', this.moviesInfo)
        }
    }
};
</script>

<style lang="scss">
@import './assets/scss/vars';

.header-top-form__list-link {
    font-weight: 500;
    font-size: 14px;
    line-height: 18px;
    color: #FFFFFF;
    transition: color 0.3s;

    &:hover {
        color: #9CA3AF;
    }
}
</style>