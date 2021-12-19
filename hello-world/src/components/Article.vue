<template>
    <div>
        <h2>Article Component</h2>
        <h2 v-bind="$attrs">{{title}}</h2>
        <h2>{{like}}</h2>
        <h2>{{isPublished}}</h2>
    </div>
</template>

<script>
    export default {
        name: 'Article',
        props: {
            title: {
                String,
                required: true,
                default: 'Article'
            },
            like: Number,
            isPublished: Boolean
        },
        inheritAttrs: false 
    }
</script>
