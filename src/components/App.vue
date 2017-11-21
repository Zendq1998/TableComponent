<template>
<div>
  <table-component :content="message" v-on:update="SortParent"></table-component>
</div>
</template>
<script>
import mytable from './mytable.vue'
export default{
  data(){
    return{
      message:[['姓名','语文','数学','英语','总分'],
            ['小明',80,90,70,0],
            ['小红',90,60,70,0],
            ['小亮',60,100,70,0]]
    }
  },
  created: function() {    
    var l = this.message[0].length
    
    for(var i=1;i<this.message.length;i++){
        for(var j=1;j<l-1;j++){     
           this.message[i][l-1]+=this.message[i][j]
         }
      }
    
    },
  components: {
    'table-component':mytable
  },
  methods: {
    SortParent: function (key) {
//       this.message = [['姓名','语文','数学','英语','总分'],
//             ['小明',80,90,70,240],
//             ['小红',90,60,70,220],
//             ['小亮',60,100,70,230]]
      var colum = this.message[0].indexOf(key)
      var arr = []
      for(var i=1;i<this.message.length-1;i++){
        for(var j=i;j<this.message.length-1;j++){
          if(this.message[i][colum]<this.message[j+1][colum]){
            arr = this.message[i]
            this.$set(this.message, i, this.message[j+1])
            //this.message[i] = this.message[j+1]
            this.$set(this.message, j+1, arr)
            //this.message[j+1] = arr
          }
        }
      }
      console.log(this.message)
    }
  }
}
</script>



<style lang="scss">
.mytable,.mytable tr{
  border-collapse: collapse;
  border: 1px solid #dfebea;
  height: 60px;
}

.mytable thead{
  border:none;
  background-color:#c4dbd8
}

.mytable tbody{
  color:#7e8a8a
}

.mytable td , .mytable th{
  width: 150px;
  text-align:center;
}

</style>

