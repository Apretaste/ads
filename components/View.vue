<template>
	<div>
		<!-- image -->
		<img v-if="image" class="img-fluid mb-3 delete-if-no-image" :src="image" alt="Imagen">

		<!-- description -->
		<div v-html="description" class="mb-4"></div>

		<!-- list -->
		<ap-list v-if="listData().length > 0" :data="listData()" class="mb-4"></ap-list>

		<div v-if="gallery.length > 0" class="row">
			<div class="col-6" v-for="image in gallery">
				<ap-image class="mb-4" :data="galleryData(image)"></ap-image>
			</div>
		</div>

		<!-- floating action button -->
		<ap-fab class="tutorial-fab" :data="fab"></ap-fab>

		<!-- button -->
		<ap-button v-if="showButton" :data="button"></ap-button>
	</div>
</template>

<script>
module.exports = {
	data: function () {
		return {
			image: apretaste.request.image,
			description: apretaste.request.description,
			gallery: apretaste.request.gallery,
			showButton: apretaste.request.btnCaption != "",
			button: {
				icon: 'fas fa-arrow-circle-right',
				caption: apretaste.request.btnCaption,
				size: 'large',
				isPrimary: true,
				onTap: function(){window.open(apretaste.request.btnLink,'_blank')}
			},
			fab: [{
				icon:'fas fa-arrow-left', 
				onTap:function(){apretaste.back()}
			}]
		}
	},
	methods: {
		galleryData(image) {
			return {
				src: image.img,
				actions: [],
				square: true,
				radius: '.25rem'
			};
		},
		listData() {
			var data = [];
			// facebook
			if(apretaste.request.facebook) {
				data.push({
					icon: 'fab fa-facebook',
					title: 'Facebook',
					actions: [{icon:'fas fa-arrow-right', onTap: function(){window.open(apretaste.request.facebook,'_blank')}}]
				})
			}
			// twitter
			if(apretaste.request.twitter) {
				data.push({
					icon: 'fab fa-twitter',
					title: 'Twitter',
					actions: [{icon:'fas fa-arrow-right', onTap: function(){window.open(apretaste.request.twitter,'_blank')}}]
				})
			}
			// instagram
			if(apretaste.request.instagram) {
				data.push({
					icon: 'fab fa-instagram',
					title: 'Instagram',
					actions: [{icon:'fas fa-arrow-right', onTap: function(){window.open(apretaste.request.instagram,'_blank')}}]
				})
			}
			// email
			if(apretaste.request.email) {
				data.push({
					icon: 'fas fa-envelope',
					title: apretaste.request.email,
					actions: [{icon:'fas fa-arrow-right', onTap: function(){window.open('mailto:'+apretaste.request.email,'_blank')}}]
				})
			}
			// phone
			if(apretaste.request.phone) {
				data.push({
					icon: 'fas fa-phone',
					title: apretaste.request.phone
				})
			}
			return data;
		}
	}
}
</script>

<style scoped>
</style>
