<script>
import AppModal from './components/Modal.vue'
import ImageContainer from './components/image.vue'
import topnav from './components/topnav.vue';
import { provide,ref} from 'vue';
export default {
  name: 'App',
  components: {
    AppModal,
    ImageContainer,
    topnav
  },
  
  setup(){
    let userdata=ref({pimg:"./profile.jpg",username:"cicikuş",description:"Cici"});
     
    const usermod=(profileimage,username,description)=>{
      userdata.value.pimg=profileimage;
   userdata.value.username=username;
   userdata.value.description=description;
       }

    provide('usermod', usermod);

    return {
      userdata
    }
  },
  data(){
    return {
      picaddmodal:false,
      mode:0,
      defaultindex:0,
      defaultvalues:{},
      pics:[]
    };
  },
  methods:{
   showmodal()
   {
   this.picaddmodal=true;
   },
   closemodal()
   {
   this.picaddmodal=false;
   },
   findbyid(id)
   {
    for(let i=0;i<this.pics.length;i++)
    {
      if(id===this.pics[i].id)
      return i;
    }
    return -1;
   },
   addpic(img)
   {
    this.pics.push(img);
   },
   modpic(id,img)
   {
    this.pics.splice(this.findbyid(id),1,img);
   },
   delpic(id)
   {   
    this.pics.splice(this.findbyid(id),1);
   },
   
   modmodalopen(img)
   {
   this.mode=1;
   this.defaultvalues=img;
   this.showmodal();
   }
   
  }
}
</script>
<template>
  <AppModal v-if="picaddmodal"  :mode=this.mode :defaultvalues=this.defaultvalues @close="closemodal()" @addpic="addpic" @modpic="modpic"/>
  <topnav :userdata=this.userdata  :uploadedtimes=this.pics.length />
  <div class="images"  >
    <img class="imageadd" src="./assets/imageadd.jpg" @click="this.mode=0;showmodal()"/>
  
   <ImageContainer v-for="pic in pics" :key="pic.id" :img=pic @delpic="delpic(pic.id)" @modmodal="modmodalopen(pic)"></ImageContainer>
  </div>
 
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 0px;
}
.images{
  display:flex;
  flex-wrap: wrap;
  margin-top: 20px;
}
.imageadd{
  width:200px;
  height: 200px;
  cursor:pointer;
  box-shadow: RGBA(0,0,0,0.2) 2 2 10px;
}
.imageadd:hover{
  filter:opacity(0.8);
}
</style>
