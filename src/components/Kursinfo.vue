<template>
  <div class="info-container">
      <div class="header-info">
          <div class="head head-date">Date</div>
          <div class="head head-title">Title</div>
          <div class="head head-content">Content</div>
      </div>
      <kursinfoRad v-for="info in kursinfo" :key="info.id" :info="info" @handle-delete="deleteRow"/>

  </div>
</template>

<script>
import kursinfoRad from './KursinfoRad.vue'
export default {
    data: ()=> ({
        kursinfo: [{id:1,date:'date1',title:'title1',content:'Lorem Ipsum is simply dummy text of the printing and typesetting industry.'},
                   {id:2,date:'date2',title:'title2',content:'Lorem Ipsum is simply dummy text of the printing and typesetting industry.'},
                   {id:3,date:'date3',title:'titel3',content:'Lorem Ipsum is simply dummy text of the printing and typesetting industry.'},
                   {id:4,date:'date4',title:'title4',content:'Lorem Ipsum is simply dummy text of the printing and typesetting industry.'},
                   {id:5,date:'date5',title:'title5',content:'Lorem Ipsum is simply dummy text of the printing and typesetting industry.'}
                   ]
    }),
    components: {
        kursinfoRad
    },
    methods: {
        deleteRow(value) {
            this.kursinfo=this.kursinfo.filter(item=>item.id!==value);

        }
    }

}
</script>

<style>
.header-info {
    display: grid;
    background-color: #D33A3A;
    padding: 1em;
}

  .info-container {
      border: 1px solid gray;
      background-color: #C4C4C4;
      color: black;
      text-align: center;
  }
  .head {
      display: none;
  }
  /* Check if the screen size is at least 481px */ 
        @media only screen and (min-width: 481px) { 
            .head-content, .head-title, .head-date { 
                display: block; 
            } 
            .header-info {
               grid-template-columns: 1fr 1fr 1fr;
            }
        }
   /* Check if the screen size is at least 320px and at most 480px */ 
        @media only screen and (max-width: 480px){ 
            .head-date, .head-title { 
                display: block; 
            } 
            .header-info {
               grid-template-columns: 1fr 1fr;
            }
        }  
  
</style>
