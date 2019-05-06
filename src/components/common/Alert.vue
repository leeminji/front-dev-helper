<template>
     <div>
      <transition name="fade">
      <v-alert
        class="ma-3"
        v-show = "showError"
        :value = "true"
        :type = "state"
        outline>
        {{msg}}
      </v-alert>
      </transition>
    </div>   
</template>

<script>
//success, info, error, warning
export default {
    props : ['msg', 'state'],
    data(){
        return {
   
        }
    },
    mounted(){

    },
    methods : {
        resetAlert(){
            setTimeout(()=>{
               this.$emit('resetAlert');
            }, 2000);
        }    
    },
    computed : {
        showError(){
            if( this.state != null ){
                this.resetAlert();
                return true;
            }else{
                return false;
            }
        }
    }
}
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
