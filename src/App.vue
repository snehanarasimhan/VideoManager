<template>
	<div class="container">
		<SearchBar @searchTerm="onTermChange"></SearchBar>
		<div class="row">
			<VideoDetail :video="selectedVideo"></VideoDetail>
			<VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
		</div>
	</div>
</template>

<script>
	import axios from 'axios';
	import SearchBar from './components/search-bar';
	import VideoList from './components/video-list';
	import VideoDetail from './components/video-detail';

	const API_KEY = 'AIzaSyCaZqK25942y4TKIbjHq5HkOMLvbmT1uDM';
	export default {
		name: 'App', 
		components: {
			SearchBar,
			VideoList,
			VideoDetail
		},
		data() {
			return {
				videos: [],
				selectedVideo: null
			};
		},
		methods: {
			onVideoSelect(video){
				this.selectedVideo = video;
			},
		onTermChange(searchTerm){			
			axios.get('https://www.googleapis.com/youtube/v3/search', {
			params: {
			key: API_KEY,
			type: 'video',
			part: 'snippet',
			q: searchTerm
		}
		})
		.then(response => {
			this.videos = response.data.items;	 
		}); 
		}
	}
	};
</script>