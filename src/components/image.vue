<script>

export default {
  name: 'AppImageContainer',
  props: {
    img:{}
  },
  data(){
  return {selectedimg:"./image.svg"}
  },
  methods: {
    delpic(id)
    {
    this.$emit('delpic',id);
    },
    modpic(img)
    {
    this.$emit('modmodal',img);
    }
  }
}
</script>
<template>
  <div className="imgcon">
    
    <img className="img"  :src=img.src />
    <span @click="delpic(img.id)">x</span>
    <span @click="modpic(img)">≡</span>
    <div className="comment"> {{img.content}}</div>
    
    </div>
    
</template>



<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.imgcon{
    border-radius: 5px;
    margin:2%;
    padding:10px;
    box-shadow: RGBA(0,0,0,0.1) 0 0 10px;
    width:200px;
}
.imgcon .img{
    max-width:100%;
    max-height: 100%;
    cursor:pointer;
}
.imgcon .comment{
    padding:10px;
    width: 80%; 
}

.imgcon span{
    float:right;
    margin:3px;
    padding:1%;
    font-size: large;
    border-radius: 2px;
    cursor: pointer;  
}
.imgcon span:hover{
    color:gray;
    background-color: rgba(210, 208, 208,0.1);
}
.imgcon span:active{
    color:black;
    background-color: rgba(210, 208, 208,0.5);
}

</style>
