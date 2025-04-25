<template>
    <div id="app" :class="$style.app">
        <div :class="$style.preview">
            <ThingsPreview
                :things="selectedUserThings"
                :max-count="6"
                @delete-thing="onDeleteSelectedUserThing"
            />
            <ThingsPreview
                :things="selectedThingOfChoose"
                single-item
                @delete-thing="onDeleteSelectedThingsOfChoose"
            />
        </div>

        <div :class="$style.cart">
            <ThingsList
                :things="userThings"
                :class="$style.list"
                @select-item="onSelectUserThings"
            />
            <ThingsList
                :things="thingsOfChoose"
                :class="$style.list"
                @select-item="onSelectThingsOfChoose"
            />
        </div>
    </div>
</template>

<script>
import { userThings, thingsOfChoose } from '@/assets/js/mock/mockData';
import ThingsList from '@/components/ThingsList.vue';
import ThingsPreview from '@/components/ThingsPreview.vue';

export default {
    name: 'App',
    components: {
        ThingsPreview,
        ThingsList,
    },
    data() {
        return {
            thingsOfChoose: thingsOfChoose || [],
            userThings: userThings || [],
            allSelectedUserThings: [],
            selectedThingOfChoose: [],
        };
    },
    methods: {
        /**
         * Добавляет элемент в список выбранных пользовательских элементов.
         * @param {Object} value - Выбранный элемент.
         */
        onSelectUserThings(value) {
            this.allSelectedUserThings.push(value);
        },

        /**
         * Устанавливает выбранный элемент для выбора.
         * @param {Object} value - Выбранный элемент.
         */
        onSelectThingsOfChoose(value) {
            this.selectedThingOfChoose = [value];
        },

        /**
         * Удаляет элемент из списка выбранных пользовательских элементов.
         * @param {number} value - Объект удаляемого элемента.
         */
        onDeleteSelectedUserThing(value) {
            console.log(value.id);
            this.allSelectedUserThings = this.allSelectedUserThings.filter(thing => thing.id !== value.id);
        },

        /**
         * Удаляет элемент из списка выбранных элементов для выбора.
         */
        onDeleteSelectedThingsOfChoose( ){
            console.log('adsadsads');
            this.selectedThingOfChoose = [];
        },
    },
    computed: {
        /**
         * Возвращает уникальные выбранные пользовательские элементы.
         * @returns {Array} Уникальные выбранные пользовательские элементы.
         */
        selectedUserThings() {
            const set = new Set(this.allSelectedUserThings);
            return Array.from(set);
        },
    }
}
</script>

<style lang="scss" module>
*{
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    width: 100vw;
    height: 100vh;
}
.app {
    display: flex;
    flex-direction: column;
    gap: 24px;
    width: 100%;
    height: 100%;
    padding: 20px 48px;
}

.cart, .preview {
    display: flex;
    align-items: center;
    justify-content: space-between;

}

.cart{
    gap: 24px;
}

.list {
    padding: 24px;
    border: 2px solid #000;
    border-radius: 12px;
}
</style>
