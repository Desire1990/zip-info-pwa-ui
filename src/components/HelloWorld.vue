<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>
          ZipInfo
        </ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <zip-search v-on:get-zip="getZipInfo"/>
      <zip-info :info="info"/>
      <clear-info :info="info" v-on:clear-info='clearInfo'/>
    </ion-content>
  </div>
</template>

<script>
import ZipSearch from "../components/ZipSearch"
import ZipInfo from "../components/ZipInfo"
import ClearInfo from "../components/ClearInfo"
import { alertController } from "@ionic/vue"
export default {
  name: 'HelloWorld',
  components:{ZipSearch, ZipInfo, ClearInfo},
  data(){
    return {
      info:null
    }
  },
  methods:{
    showAlert(){
        return alertController.create({
            header:"Enter Zipcode",
            message:"Please enter a valid US Zipcode",
            buttons:["Ok"]
          })
          .then(a => a.present());
      },
    clearInfo(){
      this.info=null;
    },
    async getZipInfo(zip){
      const res = await fetch(`https://api.zippopotam.us/us/${zip} `)
      if(res.status==404){
        this.showAlert()
      }
      this.info = await res.json()
      console.log(this.info)
    }
  }
}
</script>

