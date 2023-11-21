<script>
import useroptions from './useroptions.vue';
export default {
    name: 'TopNav',
    data() {
        return {
        usermodal:false
        };
    },
    components:{
        useroptions
    },
    props: {
        userdata:Object,
        uploadedtimes:Number        
        },
    methods: {
        openmodal()
        {
        this.usermodal=true;
        },
        closemodal()
        {
        this.usermodal=false;
        },  
            
    }
}
</script>
<template>
    <useroptions v-if="usermodal" :userdata=this.userdata   @close="closemodal"></useroptions>
    <div className='topbar'>
        <div className='profilediv'>
            <img alt="profileimg" className='profileimg' :src=this.userdata.pimg @click="openmodal()"/>
        </div>
        <label className='profilename'>{{ this.userdata.username }}</label>
        <q className='description'>{{ this.userdata.description }}</q>
        <div className='uploadedtimes'>
            <img alt="optionsbtn" className='optionsbtn' src="../assets/options.svg" 
            @click="openmodal()"/>
            <p>Uploaded {{ uploadedtimes }} images</p>
        </div>
    </div>
</template>

<style scoped>
.topbar {
    display: grid;
    grid-template-columns: auto 3fr;
    grid-template-rows: 1fr 1fr auto;
    gap: 5px 15px;
    margin: 1px;
    padding: 1%;
    background-color: RGBA(200, 200, 200, 0.2);
    box-shadow: RGBA(0, 0, 0, 0.2) 1px 1px 10px;
    font-size: large;
    color: rgb(0, 100, 38);
}

@media screen and (max-width: 600px) {
    .topbar {
        display: flex;
        flex-wrap: wrap;
    }

    .uploadedtimes {
        position: relative;
        left: 60%;
    }

}

.profilediv {
    grid-area: 1 / 1 / 3 / 2;
}

.profileimg {
    border-radius: 5px;
    width: 150px;
    height: 150px;
    cursor:pointer;
}

.profilename {
    grid-area: 1 / 2 / 2 / 3;
    font-size: x-large;
}

.description {
    grid-area: 2 / 2 / 3 / 3;
    font-size: 1em;
    width: 30%;
    font-family: Open Sans;
    font-style: italic;
    color: #555555;
    padding: 5px 5px;
    border-radius: 5px;
    line-height: 1.0;
    position: relative;
    background: linear-gradient(180deg, rgba(233, 233, 233, 1) 0%, rgba(233, 233, 233, 0.75) 5%, rgba(233, 233, 233, 0.75) 95%, rgba(233, 233, 233, 1) 100%);
}

.uploadedtimes {
    text-align: right;
    font-size: 12pt;
    grid-area: 2 / 2 / 3 / 3;
}

.optionsbtn {
    width: 20px;
    height: 20px;
    cursor: pointer;
}

.optionsbtn:hover {
    opacity: 0.2;
}</style>
