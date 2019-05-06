<template>
<v-container grid-q-md text-xs-center>
  <v-card class="">
    <v-toolbar color="purple darken-4" dark flat>
      <v-toolbar-title>텍스트변경</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-sm-and-down">
        <v-btn flat>Link One</v-btn>
        <v-btn flat>Link Two</v-btn>
        <v-btn flat>Link Three</v-btn>
      </v-toolbar-items>
    </v-toolbar>
    <v-layout row wrap class="pa-3">
        <v-flex xs12>
          <v-textarea
          name="defaultText"
          label="기본 텍스트"
          v-model = "defaultText"
          v-on:keyup ="changeText"
          ></v-textarea>          
        </v-flex>
        <v-flex xs12>
            <v-spacer></v-spacer>
            <v-btn>리셋</v-btn>
        </v-flex>
    </v-layout>
    <v-layout class="purple lighten-5 pa-3">
        <v-flex xs12  sm12 md6 class="pr-1">
            <v-card>
                <v-card-title>대문자변경</v-card-title>
                <v-card-text>
                    <v-textarea
                    name="uppertText"
                    label="대문자 텍스트"
                    v-model = "uppertText"
                    ></v-textarea>                     
                </v-card-text>
                <v-card-actions class="text-xs-right">
                    <v-spacer></v-spacer>
                    <v-btn outline flat large color="purple darken-3" @click="copyContent" v-if="uppertText != null">
                    <v-icon>fas fa-copy</v-icon>
                    <span  class="mr-1"></span> 복사
                    </v-btn>  
                </v-card-actions> 
            </v-card>
        </v-flex>
        <v-flex xs12  sm12 md6 class="pl-1">
            <v-card>
                <v-card-title>소문자변경</v-card-title>
                <v-card-text>
                    <v-textarea
                    name="lowerText"
                    label="소문자 텍스트"
                    v-model = "lowerText"
                    ></v-textarea>                     
                </v-card-text>
                <v-card-actions class="text-xs-right">
                    <v-spacer></v-spacer>
                    <v-btn outline flat large color="purple darken-3" @click="copyContent" v-if="lowerText != null">
                    <v-icon>fas fa-copy</v-icon>
                    <span  class="mr-1"></span> 복사
                    </v-btn>  
                </v-card-actions> 
            </v-card>
        </v-flex>
    </v-layout>
  </v-card>
</v-container>
</template>

<script>
export default {
    data (){
        return {
            defaultText : null,
            uppertText : null,
            lowerText : null
        }
    },
    methods : {
        copyContent(){

        },
        changeText(){
            this.uppertText = this.defaultText.toUpperCase();
            this.lowerText = this.defaultText.toLowerCase();
        }
    }
}
</script>

<style>

</style>
