<script>
import {pics} from '../../data'
export default {
    name: 'ProductionCard',
    props:{
        item: Object
    },
    computed: {
        title(){
            return this.item.title || this.ite.name;
        },
        originalTitle(){
            return this.item.original_title || this.item.original_name;
        },
        hasFlag(){
            const flags = ['it', 'en'];
            return flags.includes(this.original_language);
        },
        flagSrc(){
            const url = new Url(`../../asset/img/${this.item.original_language}.png`, import.meta.url);
            return url.href;
        },
        posterPath(){
            return pics.baseUrl + this.item.poster_path;
        }, 
        vote(){
            return Math.ceil (this.item.vote_average / 2)
        }


    },
    methods:{
        setStarClass(n){
            n <= this.vote ? 'fa-solid' : 'fa-regular'
        }
    }
    };



</script>


<template>
<ul>
    <li>
        {{ item.title }}
    </li>
    <li>
        {{ item.original_title }}
    </li>
    <li>
        <img v-if="hasFlag" :src="flagSrc" :alt="item.original_language">
        <div v-else>{{ item.original_language }}</div>
    </li>
    <li>
        <img :src="posterPath" alt="title">
    </li>
    <li>
        <i v-for="n in 5" :class="setStarClass(n)" class="fa-star"></i>
    </li>
</ul>


</template>