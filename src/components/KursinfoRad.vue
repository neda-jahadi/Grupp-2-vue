<template>
 <div class="kursinfo-container">
   <div class="kursinfo" @click="clickableDiv">
      <div>{{info.date}}</div>
      <div>{{info.title}}</div>
      <div>{{info.content.substring(0,20)}}...</div>
   </div>
   <div class="content" v-show="contentShow">
       <div v-show="visaContent" @click="visaContent=false">{{info.content}}</div>
       <textarea v-show="!visaContent" type="text" v-model="info.content" @blur="visaContent=true" />
       <div>
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
          console.log('Div is clicked');
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
 .content {
     border: 1px solid gray;
     background-color: #979797;
     color: black;
     padding: 1em;
 }

  button {
      width: 20%;
    padding: 0.5em;
    background-color: #D33A3A;
    margin-top: 1em;
}

  .kursinfo {
      border: solid 1px gray;
      padding: 1em;
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;

  }

  .kursinfo:hover {
      background-color:#737373;
      cursor: pointer;
  }
</style>
