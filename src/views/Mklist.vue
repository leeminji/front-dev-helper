
<template>
<v-container grid-q-md text-xs-center>
  <v-card class="pb-3">
    <v-toolbar color="purple darken-4" dark flat>
      <v-toolbar-title>리스트만들기</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-sm-and-down">
        <v-btn flat>Link One</v-btn>
        <v-btn flat>Link Two</v-btn>
        <v-btn flat>Link Three</v-btn>
      </v-toolbar-items>
    </v-toolbar>
    
    <v-layout row wrap class="pa-3">
       <v-flex xs3 class="pa-1">
         <v-btn block depressed large @click="changeCode('a')">&lt;a&gt;</v-btn>
       </v-flex>
       <v-flex xs3 class="pa-1">
         <v-btn block depressed large @click="changeCode('li')">&lt;li&gt;</v-btn>
       </v-flex>
       <v-flex xs3 class="pa-1">
         <v-btn block depressed large @click="changeCode('p')">&lt;p&gt;</v-btn>
       </v-flex>
       <v-flex xs3 class="pa-1">
         <v-btn block depressed large @click="changeCode('td')">&lt;td&gt;</v-btn>
       </v-flex>
    </v-layout>
    <v-divider></v-divider>
    <v-layout class="pa-3">
      <v-flex xs3>
      <v-checkbox
        v-model="is_number"
        label="번호추가"
        color="purple"
        value="T"
        hide-details
      ></v-checkbox>
      </v-flex>
      <v-flex xs3>
      <v-checkbox
        v-model="is_span"
        label="텍스트에 <span>추가"
        color="purple"
        value="T"
        hide-details
      ></v-checkbox>
      </v-flex>
    </v-layout>
    <v-divider></v-divider>
    <v-layout row wrap class="pa-3">
      <v-flex xs6 sm3 md3 class="pa-1">
        <v-text-field
          ref="prevCode"
          label="내용이전태그"
          v-model="prevCode"
        ></v-text-field>
      </v-flex>       
      <v-flex xs6 sm3 md3 class="pa-1">
        <v-text-field
          ref="nextCode"
          label="내용다음태그"
          v-model="nextCode"
        ></v-text-field>
      </v-flex>
      <v-flex xs6 sm3 md3 class="pa-1">
        <v-btn depressed large block dark color="purple darken-2" @click="changeContent">
          코드만들기 <v-icon right dark>fas fa-code</v-icon>
      </v-btn>  
      </v-flex>
      <v-flex xs6 sm3 md3 class="pa-1">
        <v-btn depressed large block dark color="purple lighten-3" @click="chageReset">
          취소 <v-icon right dark>fas fa-redo</v-icon>
        </v-btn>  
      </v-flex>
    </v-layout>
    <v-divider></v-divider>
    <v-layout row wrap class="pl-3 pr-3">
      <v-flex xs6>
        <v-card flat class="pa-1">
          <v-card-text class="px-0">
            <v-textarea
              ref="text"
              name="preText"
              label="변경할내용"
              v-model="content"
              hint="Hint text"
              ></v-textarea>            
          </v-card-text>
          <v-card-actions>
          </v-card-actions>
        </v-card>
      </v-flex>    
      <v-flex xs6>
        <v-card flat class="pa-1">
          <v-card-text class="px-0">
            <v-textarea
              id="resultText"
              ref = "resultText"
              name="resultText"
              label="변경완료"
              v-model="resultContent"
              hint="해당 태그가 적용된 텍스트입니다."
              ></v-textarea>            
          </v-card-text>
          <v-card-actions class="text-xs-right px-0">
            <v-spacer></v-spacer>
            <v-btn outline flat large color="purple darken-3" @click="copyContent" v-if="resultContent != null">
              <v-icon>fas fa-copy</v-icon>
              <span  class="mr-1"></span> 복사
            </v-btn>  
          </v-card-actions>      
        </v-card>
      </v-flex>      
    </v-layout>  
    <AlertComponent :msg="msg" :state="alertState" @resetAlert="resetAlert" />
  </v-card>     
</v-container>
</template>

<script>
import AlertComponent from '@/components/common/Alert'
export default {
  components : {
    AlertComponent
  },
  data (){
    return {
      msg : null,
      alertState : null,
      code : null,
      content : null,
      resultContent : null,
      is_number : true,
      prevCode : null,
      nextCode : null,
      is_span : null,
    }
  },
  methods : {
    copyContent(){
      if( this.resultContent != null){
        const resultContent = document.getElementById("resultText");
        resultContent.select();
        try {
          var successful = document.execCommand('copy');
          var msg = successful ? 'successful' : 'unsuccessful';
          this.msg = "복사하였습니다.";
          this.alertState = "info";     
        } catch (err) {
          this.msg = "복사 실패하였습니다.";
          this.alertState = "error";     
        }        
      }
    },
    resetAlert(){
      setTimeout(()=>{this.alertState = null},1000);
    },
    changeCode(_code){
      this.code = _code;
      if( this.code != null && this.code == "a"){
        this.prevCode = "<a href='#'>";
      }else{
        this.prevCode = "<"+this.code+">";
      }
      this.nextCode = "</"+this.code+">";
    },
    chageReset(){
      this.code = null;
      this.prevCode = null;
      this.nextCode = null;
      this.resultContent = null;
      this.content = null;
    },
    changeContent(){
      let output = [];

      if( this.prevCode == null ){
        this.msg = "바꿀 태그를 선택하거나 작성해주세요.";
        this.alertState = "error";
        this.$refs.prevCode.focus();
        return;
      }
      if (this.content != null){
        output = this.content.split("\n");

        let result = output.map((line, index)=>{
          let str = this.prevCode;
          if( this.is_number == "T"){
            str += "<span class='numberic'>"+(index+1)+"</span>";
          }
          if( this.is_span == "T" ){
            str += "<span>"+line.trim()+"</span>";
          }else{
            str += line.trim();
          }          
          str += this.nextCode;
          return str;
        });
        
        this.resultContent = result.join("\n");
        this.msg = "코드변경이 완료되었습니다.";
        this.alertState = "success";
        this.$refs.resultText.focus();        
      }else{
        this.$refs.text.focus();
        this.msg = "변경할 내용을 작성해주세요.";
        this.alertState = "error";
      }
    },    
  },
  computed : {

  }

}
</script>

<style>

</style>
