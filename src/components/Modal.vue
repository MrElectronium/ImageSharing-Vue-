<script>
import { uuid } from 'vue-uuid';
export default {
  name: 'AppModal',
  props: {
    mode: Number,
    defaultvalues:{}
  },
  data(){
  return {
    selectedimg:"./image.svg",
  defaultid:0,
buttontitle:"Tamam"}
  },
  mounted(){
   this.contentarea=this.defaultvalues.content;
   if(this.defaultvalues.src)
   this.selectedimg=this.defaultvalues.src;
   this.defaultid=this.defaultvalues.id;
   if(this.mode==0)
   {
    this.buttontitle="Ekle";
   }
   else if(this.mode==1)
   {
    this.buttontitle="Güncelle";
   }
  },
  methods: {
    handleFileChange(event) {      
      this.selectedimg = URL.createObjectURL(event.target.files[0]);
    },
    closeModal()
    {
      this.$emit('close');
    },
    addpic(src,content)
    {
      let img={id:uuid.v1().replaceAll("-",""),src:src,content:content};
      this.$emit('addpic',img)
    },
    modpic(defaultid,src,content)
    {
      let img={src:src,content:content}
      this.$emit('modpic',defaultid,img);
    },
    openfilebox()
        {
            this.$refs.fileInput.click();
        },
  }
}
</script>
<template>
  <div class="modal">    
    <div class='modalcontainer'>
    <button class='extbtn' @click="closeModal()">x</button>       
       <div >
        <img alt="SelectedPicture" :src="selectedimg" class="selectedimg"
        @click="openfilebox" ><br/>
        <input type="file" ref="fileInput" @change="handleFileChange" accept="image/*" /><br/>
        <textarea v-model="contentarea" class='txtarea' placeholder="Resmin açıklaması..." ></textarea>
        <br/><button class="button" @click="()=>{
          if(mode==0)
          addpic(selectedimg,this.contentarea)
        else if(mode==1)
          modpic(defaultid,selectedimg,this.contentarea);
          closeModal();
        }">{{buttontitle}}</button>
       </div>
        </div>    
    </div>
</template>



<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.modal {
    position: fixed;
    z-index: 1;
    left: 0;
    top: 0;
    width: 100%;
    /* Full width */
    height: 100%;
    background-color: rgb(0, 0, 0);
    /* Fallback color */
    background-color: rgba(0, 0, 0, 0.4);
    /* Black w/ opacity */
}

.modalcontainer {
    background-color: #fefefe;
    border-radius: 5px;
    box-shadow: RGBA(0, 0, 0, 0.2) 0 0 10px;
    margin: 5% auto;
    /* 15% from the top and centered */
    padding: 20px;
    text-align: center;
    border: 1px solid #888;
    width: 40%;
    /* Could be more or less, depending on screen size */
}
@media screen and (max-width: 600px){
  .modalcontainer{
    width:80%;
    margin:1% auto;
  }
  
}
.txtarea{
    width:70%;
    height: 90px;
    box-shadow: rgba(9, 30, 66, 0.25) 0px 1px 1px, rgba(9, 30, 66, 0.13) 0px 0px 1px 1px;
}
.extbtn {
    background-color: transparent;
    box-shadow: RGBA(0, 0, 0, 0.2);
    padding:3px 5px 3px 5px;
    margin:3px;
    cursor:pointer;
    border-radius: 2px;
    border: none;
    font-weight: 600;
    float:right;
    color:red;
}

.extbtn:hover {
    background-color: RGBA(0, 0, 0, 0.2);
}
.button {
    background-color: initial;
    background-image: linear-gradient(-180deg, #FF7E31, #E62C03);
    border-radius: 2px;
    box-shadow: rgba(0, 0, 0, 0.1) 0 2px 4px;
    color: #FFFFFF;
    cursor: pointer;
    display: inline-block;
    font-family: Inter,-apple-system,system-ui,Roboto,"Helvetica Neue",Arial,sans-serif;
    height: 40px;
    line-height: 40px;
    outline: 0;
    overflow: hidden;
    padding: 0 10px;
    margin:3px;
    pointer-events: auto;
    position: relative;
    text-align: center;
    touch-action: manipulation;
    user-select: none;
    -webkit-user-select: none;
    vertical-align: top;
    white-space: nowrap;
    width: auto;
    border: 0;
    transition: box-shadow .2s;
  }
    .button:hover {
    box-shadow: rgba(253, 76, 0, 0.5) 0 3px 8px;
  }
  .button:active {
    box-shadow: rgba(253, 76, 0, 0.9) 0 3px 8px;
  }
  .selectedimg{
    width:200px;
    height: 200px;
    cursor:pointer;
  }
</style>
