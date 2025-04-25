<template>
    <div
        :class="$style.ThingItem"
        @click="$emit('click', thing)"
    >
        <p >{{`name: ${thing?.name}`}}</p>
        <p >{{`id: ${thing?.id}`}}</p>
    </div>
</template>

<script>
export default {
    name: 'ThingItem',

    props: {
        thing: {
            type: Object,
            required: true
        },
    },

    methods: {
        onclick(event) {
            console.log(event);
        },
    },

}
</script>

<style lang="scss" module>
.ThingItem {
    padding: 12px;
    border: 2px solid #000;
    border-radius: 12px;
    transition: background-color .3s;
    cursor: pointer;

    &:hover {
        background-color: #f1f1f1;
    }
}
</style>
