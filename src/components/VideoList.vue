<template>
    <ul class="list-group col-md-4">
        <VideoListItem v-for="video in videos"
                       :video="video"
                       :key="video.etag"
                       @videoSelect="onVideoSelect">
        </VideoListItem>
    </ul>
</template>

<script lang="ts">
    import {Component, Prop, Vue} from 'vue-property-decorator';
    import VideoListItem from "./VideoListItem";

    /**
     * 影片搜尋清單
     */
    @Component({
        components: { VideoListItem }
    })
    export default class VideoList extends Vue {

        /**
         * 搜尋到的影片集合
         */
        @Prop(Array) videos: Array;

        /**
         * @event onVideoSelect 選中影片的點擊事件 handler
         * @param video 選中的影片
         */
        public onVideoSelect(video): void {
            this.$emit('videoSelect', video);
        }
    }
</script>