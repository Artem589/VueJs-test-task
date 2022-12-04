<template>
  <v-app>
    <v-data-table
    :headers="headers"
    :items="desserts"
    class="elevation-1 text-rigth text-center"
    disable-pagination
    hide-default-footer
    @click:row="rowClick"
    >
  <template v-slot:[`item.dog`]="{ item }"> 
    <v-row justify="center">
      <v-btn
      color="blue"
      dark
      @click="dogDialogWin(item); element = item"
      v-html="item.dog"
      >
    </v-btn>
    
    <v-dialog
      v-model="dogDialog"
      max-width="450"
      max-heigth="500"
      :retain-focus="false" 
      
    >
      <v-card>
        <v-card-title class="text-center text-h5 px-0">
          Ты любишь собак?
        </v-card-title>
        <v-img
          :src='linkImg'
          aspect-ratio="1.7"
          contain
          max-height="400"
          min-height="400"
        ></v-img>
        <v-card-text class="text-center text-h5">Им очень не хватает твоего внимания!</v-card-text>
        <v-card-actions class="mt-4 justify-center">
            <v-btn
            color="green darken-1"
            text
            @click="dogDialogWin()"
            class="ml-20"
            outlined
            rounded
          >
            Давай ещё
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
  
    </template>
    
    <template v-slot:[`item.button`]="{ item }">
<v-row justify="center">
      <v-btn
      color="red"
      dark
      @click="openWin(); element = item"
      v-html="item.button"
    >
  </v-btn>
    <v-dialog
      v-model="dialog"
      max-width="350"
      max-heigth="350"
      :retain-focus="false" 
    >
      <v-card>
        <v-card-title class="text-h5 ml-8">
         Ты хорошо подумал?
        </v-card-title>
        <v-card-actions class="mt-4">
          <v-btn
            color="green darken-1"
            text
            @click="openWin()"
          >
            Неа
          </v-btn>
          <v-spacer></v-spacer>
          <v-btn
            color="green darken-1"
            text
            @click="deleteRow()"
          >
            Ага
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>
</v-data-table>
  <v-btn 
  color="green" 
  class="my-8 mx-auto" 
  rigth="fixed" 
  outlined width="400" 
  height="60" 
  @click="addArray"
  
  >
  Тыкни в меня
</v-btn>

  </v-app>
 </template>

<script>

  export default {
    
    data () {
      return {
        dogs: [],
        linkImg: '',
        index: 0,
        count: 0,
        dogDialog: false,
        dialog: false,
        element: '',
        headers: [
          { text: 'Random Date', value: 'date'},
          { text: 'Random Number', value: 'rNum' },
          { text: 'Rundom Number * PI', value: 'rPI' },
          { text: 'DOG', value: 'dog' },
          { text: 'Clear', value: 'button' },
          
        ],
        desserts: [
          {
            date: '01/01/2022',
            rNum: 159,
            rPI: 6.0,
            dog: 'Пёсики',
            button: 'Удалить'
          },
        ],
      }
    },

  created() {
    fetch("https://dog.ceo/api/breeds/image/random/20")
    .then(response => response.json())
    .then(data => data.message.forEach(doglink => this.dogs.push(doglink)))
    .catch(err => console.log(err));
    },

methods: {
openWin() {
    this.dialog = !this.dialog;
  },
generateDate() {
  let start = new Date(2022,0,1)
  let end = new Date(2022,11,31)
  return new Date(start.getTime() + Math.random() * (end.getTime() - start.getTime()))
},
addArray() {
  const randomDate = `${this.generateDate().getDate()}/${this.generateDate().getMonth() + 1}/${this.generateDate().getFullYear()}`
  const randomNumber = Math.ceil(Math.random() * (100 - (-100) + 1) - 100)
  const randomPi = Math.ceil(randomNumber*Math.PI)
  this.desserts.push(
    {
      date: randomDate,
      rNum: randomNumber,
      rPI: randomPi,
      dog: 'Пёсики',
      button: 'Удалить'
    }
  )
},
deleteRow() {
  this.dogs = this.dogs.filter(dog => dog != this.dogs[this.index])
  this.desserts = this.desserts.filter(obj => obj != this.element)
  this.openWin()
},
rowClick(item,row) {
  console.log(row.index)
    this.index = row.index
    this.linkImg = this.dogs[this.index]
     
},
dogDialogWin(item){
  console.log(item)
    this.dogDialog = !this.dogDialog
  },
 },

}
</script>


<style>
.v-card__title {
    display: flex;
    justify-content: center;
}
.v-application--is-ltr .v-data-table > .v-data-table__wrapper > table > tbody > tr > th, .v-application--is-ltr .v-data-table > .v-data-table__wrapper > table > thead > tr > th, .v-application--is-ltr .v-data-table > .v-data-table__wrapper > table > tfoot > tr > th {
    text-align: center !important;
}
.v-application .text-start {
    text-align: center !important;
}
.v-application .green--text.text--darken-1 {
    border-radius: 10px;
    width: 120px;
    background-color: #43A047;
    color: white!important;
    caret-color: #43A047 !important;
}
.v-btn.v-size--default {
    font-size: 0.8rem;
}
.v-btn:not(.v-btn--round).v-size--default {
    height: 28px;
    min-width: 55px;
    padding: 0 16px;
    border-radius: 20px;
}
.v-data-table__wrapper > table > thead > tr > th, .v-data-table > .v-data-table__wrapper > table > tfoot > tr > th {
    -webkit-user-select: none;
    -moz-user-select: none;
    user-select: none;
    font-size: 0.87rem;
    height: 48px;
}
</style>







