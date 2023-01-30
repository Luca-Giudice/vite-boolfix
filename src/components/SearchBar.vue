<script>
export default {
    name: 'SearchBar',
    data: () => ({ term: ''}),
    props: {
        placeholder: String,
        buttonLabel: String,
    },
    emits: ('term-change', 'form-submit')
};
</script>

<template>
<form @submit.prevent="$emit('form-submit')">
<input type="text" v-model.trim="term" @keyup="$emit('term-change')" :placeholder="placeholder || 'cerca' ">
<button type="submit">{{ buttonLabel || 'Cerca'}}</button>

</form>

</template>