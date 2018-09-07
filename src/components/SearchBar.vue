<template>
    <div>
        <input title="Search" @input="onInput"/>
    </div>
</template>

<script lang="ts">
    import { Vue, Component } from 'vue-property-decorator';

    /**
     * 上方搜尋列
     */
    @Component
    export default class SearchBar extends Vue {

        /**
         * @event onInput 輸入事件 handler
         * @param event 事件
         */
        public onInput(event): void {
            this.$emit('termChange', event.target.value)
        }
    }
</script>

<style scoped>
    input {
        width: 75%;
    }

    div {
        text-align: center;
        margin: 20px;
    }
</style>