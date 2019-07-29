<template>
    <div id="ifbox" >
        <!-- <div class="closebox" v-show="closeShowData" :style={opacity} >X</div> -->
        
        <iframe :src="msg" frameborder="0" width="100%" @mousemove="msm">
        </iframe>
    </div>
</template>

<script>
import { clearTimeout, setTimeout } from 'timers';
export default {
  name: 'ifrome',
  data(){
      return {
          closeShowData:false,
          opacity:0
      }
  },
  props: {
    msg: String
  },
  methods:{
      msm(e){
          this.closeShowData = true;
          setTimeout(() => {
            this.opacity = 1
          }, 0);
          clearTimeout(closeShow)
          var closeShow = setTimeout(() => {
            this.opacity = 0
            setTimeout(()=>{
                this.closeShowData = false;
            },1000)
          }, 3000);
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#ifbox{
    width: 100%;
    height: 90vh;
}
.closebox{
    position: absolute;
    top: 0;
    right: 0;
    background:#fff;
    font-size: 18px;
    width: 30px;
    height: 30px;
    line-height: 30px;
    text-align: center;
    transition: all 0.5s;
    opacity: 0;
    
}
iframe{
    margin: 0;
    padding:0;
    height: 90vh;
}
</style>
