<template>
    <div :class="$style.ThingsPreview">
        <ThingsList
            :things="filteredThings"
            @select-item="$emit('delete-thing', $event)"
        />
        <div v-if="!singleItem">{{ `selected: ${filteredThings.length}/${maxCount}` }}</div>
    </div>
</template>

<script>
import ThingsList from '@/components/ThingsList.vue';

export default {
    name: 'ThingsPreview',
    components: { ThingsList },
    props: {
        maxCount: {
            type: Number,
            default: 10,
        },
        things: {
            type: Array,
            required: true,
        },
        singleItem: {
            type: Boolean,
            default: false,
        },
    },
    computed: {
        /**
         * Возвращает отфильтрованные элементы в зависимости от maxCount.
         * @returns {Array} Отфильтрованные элементы.
         */
        filteredThings() {
            return this.things.slice(0, this.maxCount);
        },
    },
}
</script>

<style lang="scss" module>
.ThingsPreview {
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    align-items: center;
    gap: 16px;
    min-height: 140px;
    padding: 16px;
    border: 2px solid #000;
    border-radius: 12px;
}
</style>
