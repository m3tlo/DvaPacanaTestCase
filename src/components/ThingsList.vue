<template>
    <div :class="$style.ThingsList">
        <ThingItem
            v-for="item in things"
            :key="item.id"
            :class="$style.item"
            :thing="item"
            @click="handleItemClick"
        />
    </div>
</template>

<script>
import ThingItem from '@/components/ThingItem.vue';

export default {
    name: 'ThingsList',
    components: {ThingItem},

    props: {
        things: {
            type: Array,
            required: true
        },
    },

    methods: {
        handleItemClick(item) {
            this.$emit('select-item', item);
        },
    },

}
</script>

<style lang="scss" module>
.ThingsList {
    display: flex;
    flex-wrap: wrap;
    gap: 16px;

}
</style>
