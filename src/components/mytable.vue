
<template>
  <table class="mytable">
     <thead>
       <tr>
         <th v-for="key in content[0]" 
         @click=content[0].indexOf(key)&&Sortby(key)>
           {{key}}
         </th>
       </tr>
     </thead>
     <tbody>
       <tr v-for="row in content" v-if="row!==content[0]">
         <td v-for="key in row">
           <div>
             {{key}}
           </div>
           <!-- <div v-if="key==row[row.length-1]">
             {{row[1]+row[2]+row[3]}}
           </div> -->
         </td>
       </tr>
    </tbody>
  </table>
</template>

<script>
  export default {
     props: {
        content: Array
      },
      methods:{
    Sortby:function(key){     
      this.$emit('update',key)
    }
  }
  }
</script>