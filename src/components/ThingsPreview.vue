<template>
    <div :class="[$style.ThingsPreview, classes]">
        <ThingsList
            :things="filteredThings"
            @select-item="$emit('delete-thing', $event)"
        />
        <div :class="$style.counter" v-if="!singleItem">{{ `selected: ${filteredThings.length}/${maxCount}` }}</div>
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

        classes() {
            return {
                [this.$style._isCounter]: !this.singleItem,
            }
        }
    },
}
</script>

<style lang="scss" module>
.ThingsPreview {
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    gap: 16px;
    min-width: 156px;
    min-height: 140px;
    padding: 16px;
    border: 2px solid #000;
    border-radius: 12px;

    &._isCounter {
        align-items: start;
        justify-content: space-between;
        min-width: 684px;
    }
}

.counter{
    align-self: flex-end;
}
</style>
