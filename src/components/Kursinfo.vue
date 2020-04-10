<template>
  <div class="info-container">
      <div class="header-info">
          <div>Date</div><div>Title</div><div>Content</div>
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
    grid-template-columns: 1fr 1fr 1fr;
    background-color: #D33A3A;
    padding: 1em;
}

  .info-container {
      border: 1px solid gray;
      background-color: #C4C4C4;
      color: black;

  }
  /*.info-container >div:nth-child(even){
      background-color: azure;
  }*/
</style>
