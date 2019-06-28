<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"></SearchBar>
        <div class="row">
            <VideoDetail :selectedVideo="selectedVideo"></VideoDetail>
            <VideoList :videos="videos" @videoSelect="onVideoSelect"></VideoList>
        </div>
    </div>
</template>

<script lang="ts">
    import { Component, Vue } from 'vue-property-decorator';
    import axios from 'axios';
    import SearchBar from './components/SearchBar.vue';
    import VideoDetail from "./components/VideoDetail.vue";
    import VideoList from "./components/VideoList.vue";

    /**
     * App主元件
     */
    @Component({
        components: {
            VideoList,
            VideoDetail,
            SearchBar
        }
    })
    export default class App extends Vue {

        /**
         * 搜尋完成的影片列表
         */
        public videos: Array<any> = [];

        /**
         * 被點擊的影片
         */
        public selectedVideo = null;

        /**
         * @event onTermChange 搜尋列輸入字元時觸發事件
         * @param searchTerm 鍵入的搜尋字串
         */
        public onTermChange(searchTerm: string): void {

            // YOUTUBE API KEY
            const API_KEY = process.env.VUE_APP_YOUTUBE_APIKEY;

            axios.get(
                'https://www.googleapis.com/youtube/v3/search',
                {
                    params: {
                        key: API_KEY,
                        type: 'video',
                        part: 'snippet',
                        q: searchTerm
                    }
                }
            ).then(res => this.videos = res.data.items);
        }

        /**
         * @event onVideoSelect 影片選定時觸發事件
         * @param video 被選定的影片
         */
        public onVideoSelect(video: any): void {
            this.selectedVideo = video;
        }
    }
</script>
