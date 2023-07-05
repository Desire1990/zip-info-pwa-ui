<template>
	<ion-grid>
		<form @submit="onSubmit">
			<ion-col>
				<ion-item>
					<ion-input label='ZipCode :' :value='zip' @input='zip=$event.target.value' placeholder='Enter Us code' name='zip'></ion-input>
				</ion-item>				
			</ion-col>
			<ion-col>
				<ion-button type='submit' color='primary' expand='block'>Find</ion-button>
			</ion-col>
		</form>
	</ion-grid>
</template>
<script>
	import {alertController} from "@ionic/vue"
	export default {
		name:"ZipSearch",
		components:{},
		data(){
			return{
				zip:''				
			}
		},
		methods:{
			onSubmit(e){
				e.preventDefault();
				const isValidZip = /(^\d{5}$)|(^\d{5}-\d{4}$)/.test(this.zip);
				if(!isValidZip){
					this.showAlert();
					this.zip=""
				}
				else{
					this.$emit('get-zip', this.zip)
					this.zip=""
				}
			},
			showAlert(){
				return alertController.create({
						header:"Enter Zipcode",
						message:"Please enter a valid US Zipcode",
						buttons:["Ok"]
					})
					.then(a => a.present());
			}
		},
	}
</script>