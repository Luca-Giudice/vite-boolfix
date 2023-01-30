<script>
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
        {{ item.original_language }}
    </li>
    <li>
        {{ item.vote_avarage }}
    </li>
</ul>


</template>