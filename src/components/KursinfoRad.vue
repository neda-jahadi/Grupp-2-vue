<template>
 <div class="kursinfo-container">
   <div class="kursinfo" @click="clickableDiv">
      <div class="row date">{{info.date}}</div>
      <div class="row title">{{info.title}}</div>
      <div class="row contentInRow">{{info.content.substring(0,20)}}...</div>
   </div>
   <div class="content-container" v-show="contentShow">
       <div class="content" v-show="visaContent" @click="visaContent=false">{{info.content}}</div>
       <textarea v-show="!visaContent" type="text" v-model="info.content" @blur="visaContent=true" />
       <div class="button">
         <button @click="clickData">Delete!</button>
       </div>
    </div>

 </div>
</template>

<script>
export default {
  props: {
      info: Object(null),
  },
  data:()=>({
    contentShow: false,
    visaContent: true
  }),
  methods: {
      clickData() {
          this.$emit('handle-delete', this.info.id);
      },
      clickableDiv() {
          this.contentShow=!this.contentShow;
      }
  }
}
</script>

<style> 
textarea {
  width: 90%;
  padding: 1em;
}
.content:hover {
  cursor: pointer;
}
 .content-container {
     border: 1px solid gray;
     background-color: #979797;
     color: black;
     padding: 1em;
     text-align: left;
 }
.button {
  text-align: center;
}
  button {
      width: 20%;
    padding: 0.5em;
    background-color: #D33A3A;
    margin-top: 1em;
    border-radius: 5px;
}

  .kursinfo {
      border: solid 1px gray;
      padding: 1em;
      display: grid;
      

  }

  .kursinfo:hover {
      background-color:#737373;
      cursor: pointer;
  }
  .row {
    display: none;
  }
  /* Check if the screen size is at least 481px */ 
        @media only screen and (min-width: 481px) { 
            .contentInRow, .title, .date { 
                display: block; 
            } 
            .kursinfo {
               grid-template-columns: 1fr 1fr 1fr;
            }
        }
   /* Check if the screen size is at least 320px and at most 480px */ 
        @media only screen and (max-width: 480px){ 
            .date, .title { 
                display: block; 
            } 
            .kursinfo {
               grid-template-columns: 1fr 1fr;
            }
            button {
              width: 50%;
              padding: 0.3em;
              font-size: 1.1em;
      
            }
        }  
</style>
