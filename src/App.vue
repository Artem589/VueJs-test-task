<template >
  <v-app>
    <v-data-table
    :headers="headers"
    :items="desserts"
    class="elevation-1 text-rigth"
    disable-pagination
    hide-default-footer
    >
     <template v-slot:[`item.button`]="{ item }">
     <v-btn class="mx-auto" @click="deleteRow(item)" v-html="item.button"></v-btn>
    </template>
</v-data-table>
<v-btn color="red" class="my-8 mx-auto" rigth="fixed" outlined="true" width="400" height="60" @click="addArray">Тыкни в меня</v-btn>
  </v-app>
 </template>

<script>
  export default {
    
    data () {
      return {
        title: 'click me',
        text: '<h1>кнопка</h1>',
        headers: [
          { text: 'Random Date', value: 'date'},
          { text: 'Random Number', value: 'rNum' },
          { text: 'Rundom Number * PI', value: 'rPI' },
          { text: 'Clear', value: 'button' },
        ],
        desserts: [
          {
            date: '01/01/2022',
            rNum: 159,
            rPI: 6.0,
            button: 'delete'
          },
        ],
      }
    },

methods: {
generateDate() {
  let start = new Date(2022,0,1)
  let end = new Date(2022,11,31)
  return new Date(start.getTime() + Math.random() * (end.getTime() - start.getTime()))
},
addArray() {
  const randomDate = `${this.generateDate().getDate()}/${this.generateDate().getMonth() + 1}/${this.generateDate().getFullYear()}`
  const randomNumber = Math.ceil(Math.random() * (100 - (-100) + 1) - 100)
  const randomPi = Math.ceil(randomNumber*Math.PI)
  return this.desserts.push(
    {
      date: randomDate,
      rNum: randomNumber,
      rPI: randomPi,
      button: 'delete'
    }
  )
},
deleteRow(item) {
  this.desserts = this.desserts.filter(obj => obj != item)
}
 },
}
</script>






<!-- добавить условие в месяц и день .поставить 0 впереди -->
<!-- // generateNum() {
  //   const convertDate = `${this.randomDate().getDate()}.${this.randomDate().getMonth() + 1}.${this.randomDate().getFullYear()}`
  //   return {
  //             date: convertDate,
  //             rNum: Math.ceil(Math.random() * (100 - (-100) + 1) - 100),
  //             rPI: Math.ceil(this.desserts[0].rNum * Math.PI),        
  //   }
  // }, -->


<!-- //  computed: {
  //    filteredShoes(){
  //    let des = this.desserts
  
  //       for(let i = 0; i < des.length; i++){ 
  //         des[i].rPI = des[i]*Math.PI
  //        } // assuming you're modifying each object here
  //        return des
     
  //    },
  // } -->


<!-- 
// xcode
// homebrew
// comands
// git -->
[1,2,3,4]
