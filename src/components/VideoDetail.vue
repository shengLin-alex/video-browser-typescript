<template>
    <div v-if="selectedVideo" class="col-md-8">
        <div class="embed-responsive embed-responsive-16by9">
            <iframe class="embed-responsive-item" :src="videoUrl" frameborder="0" allowfullscreen></iframe>
        </div>
        <div class="details">
            <h4>{{ selectedVideo.snippet.title }}</h4>
            <p>{{ selectedVideo.snippet.description }}</p>
        </div>
    </div>
</template>

<script lang="ts">
    import { Component, Vue, Prop } from 'vue-property-decorator';

    /**
     * 影片說明與播放器
     */
    @Component
    export default class VideoDetail extends Vue {

        /**
         * 清單中選中的影片
         */
        @Prop(Object) selectedVideo: any;

        /**
         * 影片實際網址
         */
        public get videoUrl(): string {
            return `https://www.youtube.com/embed/${ this.selectedVideo.id.videoId }`;
        }
    }
</script>

<style scoped>
    .details {
        margin-top: 10px;
        padding: 10px;
        border: 1px solid #ddd;
        border-radius: 4px;
    }
</style>