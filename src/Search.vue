<template>
    <form ref="serchPanel" @click="showSearchPanel" class="header-top__form header-top-form" action="#">
        <input @input="findResult" v-model="searchTerm" class="header-top-form__input" type="text"
            placeholder="What do you want to watch?">
        <button @click="addClassToParent" class="header-top-form__btn" type="submit">
            <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path
                    d="M14 14L10 10M11.3333 6.66667C11.3333 9.244 9.244 11.3333 6.66667 11.3333C4.08934 11.3333 2 9.244 2 6.66667C2 4.08934 4.08934 2 6.66667 2C9.244 2 11.3333 4.08934 11.3333 6.66667Z"
                    stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
            </svg>
        </button>
        <button @click="addClassToParent" class="header-top-form__close">
            <svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" clip-rule="evenodd"
                    d="M5.58377 6.99662L0 12.583L1.41388 13.9976L6.99765 8.41117L12.5814 13.9976L13.9953 12.583L8.41153 6.99662L13.9917 1.41382L12.5778 -0.000732422L6.99765 5.58207L1.41748 -0.000730515L0.00360322 1.41382L5.58377 6.99662Z"
                    fill="white" fill-opacity="0.2" />
            </svg>
        </button>
        <ul ref="searchlist" class="header-top-form__list">
            <li class="header-top-form__list-item" v-for="word in this.filteredWords" :key="word.id">
                <SearchItemVue :word="word" @sendInfoToParent="sendInfoToParent"
                    :moviesInfo="this.dataOfmovies.value.titles[word.id]" />
            </li>
        </ul>
    </form>
</template>
  
<script>

import SearchItemVue from './Search-item.vue';

export default {
    inject: ['dataOfmovies'],
    name: "Search",
    components: {
        SearchItemVue
    },
    data() {
        return {
            searchTerm: "",
            words: [],
            sortedWords: [],
            searchTermSorted: '',
            sortedWordsIndex: 0,
        };
    },
    computed: {
        filteredWords() {

            let localWords = this.words

            let arrayWithResults = []

            for (let item of this.sortedWords) {
                for (let word of item[0].value) {
                    if (this.searchTermSorted != '') {
                        if (word == this.searchTermSorted) {
                            arrayWithResults.push({ value: [localWords[this.sortedWords.indexOf(item)]], id: item[1].id })

                        }
                    } else {
                        if (item[0].value.indexOf(word) == 1) {
                            arrayWithResults.push({ value: [localWords[this.sortedWords.indexOf(item)]], id: item[1].id })
                        }
                    }
                }
            }
            return arrayWithResults
        },
    },
    inject: ['dataOfmovies'],
    mounted() {

        let wordsArr = []

        for (let item of this.dataOfmovies.value.titles) {
            wordsArr.push(item.jawSummary.title)
        }

        this.words = wordsArr

        // // // 

        let symbolsArr = []
        for (let item of wordsArr) {
            symbolsArr.push([...item.toLowerCase()])
        }

        let symbolsArrResult = []
        let idOfWords = 0
        for (let item of symbolsArr) {
            this.sortedWordsIndex = this.sortedWordsIndex++
            symbolsArrResult.unshift([{ value: [] }, { id: idOfWords }])
            idOfWords = ++idOfWords
            let letters = ''
            for (let letter of item) {
                letters += letter
                symbolsArrResult[this.sortedWordsIndex][0].value.push(letters)
            }
        }
        this.sortedWords = symbolsArrResult.reverse()
    },
    methods: {
        findResult() {
            let localSearchTerm = [...this.searchTerm.toLowerCase()]

            if (localSearchTerm.length > 1) {
                let str = ''
                for (let item of localSearchTerm) {
                    str += item
                }
                this.searchTermSorted = str.split()
            } else {
                this.searchTermSorted = localSearchTerm
            }
        },
        showSearchPanel() {
            if ( this.$refs.searchlist.classList.contains('search-list--active') ) {
                this.$refs.searchlist.classList.remove('search-list--active')
            } else {
                this.$refs.searchlist.classList.add('search-list--active')
            }
        
        },
        sendInfoToParent(elem) {
            this.$emit('sendInfoToParent', elem)
        },
        addClassToParent() {
            if ( this.$refs.serchPanel.classList.contains('form--active') ) {
                this.$refs.serchPanel.classList.remove('form--active')
            } else {
                this.$refs.serchPanel.classList.add('form--active')
            }
        }
    }
};
</script>

<style lang="scss">
@import './assets/scss/vars';

.header-top-form {
    width: 525px;
    height: 40px;
    position: relative;
    border: 2px solid rgba(#fff, 0.1);
    border-radius: 6px;
    background: rgba(#000, 1);
    &__close {
        display: flex;
        justify-content: center;
        align-items: center;
        position: absolute;
        right: 10px;
        top: 50%;
        transform: translateY(-50%);
        svg {
            width: 13px;
            height: 13px;
            path {
                fill: #9CA3AF;
                fill-opacity: 1;
            }
        }
    }
    &__list {
        height: 500px;
        max-height: 500px;
        position: absolute;
        background: rgba(0, 0, 0, 0.7);
        border-radius: 0 0 20px 20px;
        padding: 10px 10px;
        top: 37px;
        width: 99%;
        overflow-y: auto;
        left: 50%;
        transform: translateX(-50%);
        display: flex;
        justify-content: center;
        align-items: flex-start;
        flex-direction: column;
        border: 2px solid rgba(255, 255, 255, 0.1);
        display: none;
    }

    &__list-item {
        color: #fff;
    }

    &__list-link {
        font-weight: 500;
        @include adaptiv-value("font-size", 14, 12, 1);
        @include adaptiv-value("line-height", 18, 16, 1);
        color: #FFFFFF;
        transition: color 0.3s;

        &:hover {
            color: #9CA3AF;
        }
    }

    &__input {
        padding-left: 10px;
        width: 90%;
        height: 100%;

        @include adaptiv-value("font-size", 16, 14, 1);
        @include adaptiv-value("line-height", 24, 16, 1);
        color: #FFFFFF;
        background: transparent;

        &::placeholder {
            @include adaptiv-value("font-size", 16, 13, 1);
            @include adaptiv-value("line-height", 24, 15, 1);
            color: #9CA3AF;
        }
    }

    &__btn {
        position: absolute;
        top: 50%;
        right: 30px;
        width: 16px;
        height: 16px;
        transform: translateY(-50%);

        svg path {
            stroke: #9CA3AF;
        }
    }
}

.search-list--active {
    display: block;
}


@media (max-width: 900px) {
    .header-top-form__close {
        display: none;
    }
    .search-list--active {
        display: none;
    }
    .form--active {
        position: unset;
    
        .header-top-form__input {
            position: absolute;
            width: 100%;
            display: block;
            background: #000;
            left: 0;
            top: 0px;
            right: 0;
            padding-right: 95px;
            border-bottom: 2px solid rgba(255, 255, 255, 0.1);
        }
    
        .header-top-form__list {
            border-top: 2px solid rgba(255, 255, 255, 0.1) !important;
            background: #000;
            @include adaptiv-value("top", 75, 67, 1);
            width: 100%;
            left: 0;
            right: 0;
            transform: unset;
            border: unset;
            display: block;
        }
    
        .header-top-form__close {
            display: flex !important;
            width: 25px !important;
            height: 25px !important;
            svg {
                width: 15px;
                height: 15px;
                path {
                    fill-opacity: 1 !important;
                    stroke: unset !important;
                }
            }
            margin-left: auto;
            top: unset;
            bottom: unset;
            left: unset !important;
            right: 15px !important;
            transform: unset !important;
            position: absolute;
        }
        .header-top-form__btn {
            width: 25px !important;
            height: 25px !important;
            margin-left: auto;
            top: unset;
            bottom: unset;
            left: unset !important;
            right: 45px !important;
            transform: unset !important;
            justify-content: center;
            align-items: center;
            display: flex;
            svg {
                width: 19px !important;
                height: 19px !important;
            }
        }
    }
}
</style>