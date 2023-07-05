<template>
	<ion-button color='light' expand='block' v-if='info' @click='$emit("clear-info")'>
		Clear
	</ion-button>
</template>
<script>
	export default{
		props:['info']
	}
</script>