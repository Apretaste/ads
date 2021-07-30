<template>
	<div>
		<!-- title -->
		<ap-title :data="{text:'Anuncios'}"></ap-title>

		<!-- text -->
		<ap-text class="mb-3" :data="text"></ap-text>

		<!-- list -->
		<ap-list :data="listData"></ap-list>
	</div>
</template>

<script>
module.exports = {
	data() {
		return {
			text: {
				text: 'A continuación los grupos, negocios y mensajes que se anuncian en la app. Contáctenos si desea que su anuncio aparezca aquí.'
			}
		}
	},
	computed: {
		listData() {
			var data = [];
			apretaste.request.ads.forEach(function(item) {
				data.push({
					image: item.icon,
					title: item.title,
					text: item.subtitle,
					actions: [{
						icon:'fas fa-arrow-right', 
						onTap: function() {
							apretaste.send({
								command: 'ANUNCIOS VIEW', 
								data: {id: item.id}
							})
						}
					}]
				})
			})
			return data;
		}
	}
}
</script>

<style scoped>
</style>
