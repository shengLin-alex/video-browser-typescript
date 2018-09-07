<template>
    <li class="list-group-item media" @click="onVideoSelect">
        <img class="mr-3" :src="thumbnailUrl" />
        <div class="media-body">
            {{ video.snippet.title }}
        </div>
    </li>
</template>

<script lang="ts">
    import { Component, Prop, Vue } from 'vue-property-decorator';

    /**
     * 影片清單項目元件
     */
    @Component
    export default class VideoListItem extends Vue {

        /**
         * 影片物件
         */
        @Prop(Object) video;

        /**
         * 縮圖網址
         */
        public get thumbnailUrl(): string {
            return this.video.snippet.thumbnails.default.url;
        }

        /**
         * 點擊該項目的事件 handler
         */
        public onVideoSelect(): void {
            this.$emit('videoSelect', this.video);
        }
    }
</script>

<style scoped>
    li {
        display: flex;
        cursor: pointer;
    }

    li:hover {
        background-color: #eee;
    }
</style>