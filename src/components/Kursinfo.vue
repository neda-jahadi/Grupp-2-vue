<template>
  <div>
    <div class="filter-header">
       <input type="text" placeholder="Skriv vad du vill söka efter..." @keyup="handleKeyUp" />
    </div>
    <div class="sort-header">
       <h3>Hur vill du sortera listan?</h3>
       
         <button @click="sorteringsNyckel='title'">Title</button>
         <button  class="contentInMobile" @click="sorteringsNyckel='content'">Content</button>
         <button @click="sorteringsNyckel='date'">Date</button>
       
    </div>
    <div class="info-container">
      <div class="header-info">
          <div class="head head-date">Date</div>
          <div class="head head-title">Title</div>
          <div class="head head-content">Content</div>
      </div>
      <kursinfoRad v-for="info in sorteradeKursinfo" :key="info.id" :info="info" @handle-delete="deleteRow"/>

    </div>
  </div>
</template>

<script>
import kursinfoRad from './KursinfoRad.vue'
export default {
    data: ()=> ({
        kursinfo: [{id:1,date:7,title:'Serverkommunikation med Observables',content:'När en synkron funktion körs så är resten av JavaScript-appen synkroniserad med den. Ingen annan kod kan köras samtidigt.'},
                   {id:2,date:9,title:'Routing',content:'Routing används för att visa olika URL i en SPA. Den har stöd för webbläsarens bakåt- och framåt-knappar.'},
                   {id:3,date:12,title:'Formulär och validering',content:'Vi har sett hur man använder ngModel för att låta användaren ändra data i en komponent. (Dubbelriktad data binding)'},
                   {id:4,date:14,title:'Asyncronous programming',content:'Asynkrona operationer (till exempel AJAX) tar tid innan de är klara. Vi vill att våra appar ska kunna göra annat medan de väntar på resultatet. '},
                   {id:5,date:1,title:'Moduler',content:'En modul är en klass som är dekorerad med @NgModuleBootstrapping innebär att vi talar om hur appen ska startas.'},
                   {id:6,date:11,title:'Listor',content:'Vi kan använda frågetecken-operatorn för att få olika värden, beroende på ett villkor. Det är ett mer komprimerat sätt att göra en if-sats. Den används mycket i JavaScript-ramverk.'},
                   {id:7,date:23,title:'Introduktion till Vue',content:'Vue å andra sidan ger mycket mera frihet åt utvecklarna. Det är viktigt att ditt team har en kodstandard, så att man förstår varandras kod. Vue har inte behov av ett verktyg för att skapa filer'}
                   ],
        sorteringsNyckel: 'date',
        filter: ''
    }),
    components: {
        kursinfoRad
    },
    computed: {
		sorteradeKursinfo() {
			let copy = [ ...this.kursinfo ]; 
			if( this.filter == '' ) {
                console.log('Ingen filtering');
			} else {
				copy = this.filtreraKursinfo(copy);
			}
			if( this.sorteringsNyckel == 'title' ) {
				let sorterad = copy.sort( (a, b) => {
					if( a.title.toLowerCase() < b.title.toLowerCase() ) return -1;
					else if( a.title.toLowerCase() > b.title.toLowerCase() ) return 1;
					else return 0;
				} )
                console.log('title sortering is done');
                return sorterad;
            } 
            else if(this.sorteringsNyckel == 'content') {
				let sorterad = copy.sort( (a, b) => {
					if( a.content.toLowerCase() < b.content.toLowerCase() ) return -1;
					else if( a.content.toLowerCase() > b.content.toLowerCase() ) return 1;
					else return 0;
				} )
               console.log('content sortering is done');
               return sorterad;     
            }else {
				let sorterad = copy.sort( (a, b) => {
					if( a[this.sorteringsNyckel] < b[this.sorteringsNyckel] ) return -1;
					else if( a[this.sorteringsNyckel] > b[this.sorteringsNyckel] ) return 1;
					else return 0;
				} )
				return sorterad;
			}
    
        } // sorteradeKursinfo
	},  // computed
    methods: {
        deleteRow(value) {
            this.kursinfo=this.kursinfo.filter(item=>item.id!==value);

        },
        filtreraKursinfo(lista) {
            return lista.filter(info => info.title.toLowerCase().includes(this.filter.toLowerCase()));
        },
        handleKeyUp(event) {
			this.filter = event.target.value;
		}
    }

}
</script>

<style>
.sort-header {
    display: flex;
    margin: 0.5em;
}
.sort-header > * {
    margin: 0.2em;
}
.filter-header input {
    padding: 1em;
    border-radius: 5px;
    width: 50%;
}
.sort-header  button {
    background-color:powderblue;
    border: none;
}
.sort-header > button:hover {
    background-color: gray;
}
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
            .sort-header {
                flex-direction: row;
            }
            .head-content, .head-title, .head-date { 
                display: block; 
            } 
            .header-info {
               grid-template-columns: 1fr 1fr 1fr;
            }
        }
   /* Check if the screen size is at least 320px and at most 480px */ 
        @media only screen and (max-width: 480px){ 
            .contentInMobile {
                display: none;
            }
            .sort-header {
                flex-direction: column;
                margin-bottom: 2em;
            }
            .head-date, .head-title { 
                display: block; 
            } 
            .header-info {
               grid-template-columns: 1fr 1fr;
            }
        }  
  
</style>
