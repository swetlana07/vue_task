<script>
export default{
      
      data(){
        return{
          is_del:false,
          name:'',
          list:[],
        }
      },
      
      methods:{
        sort(){
          this.list.sort((a, b)=> a.title >= b.title ? 1: -1);
        },
        del(){
        const allFor = document.getElementsByClassName("checkbox");
        for (let i = allFor.length; i >0 ; --i) {
                console.log(allFor[i-1].checked);
                if(allFor[i-1].checked){
                  this.list.splice(i-1,1);
                }
        }
        for (let i = allFor.length; i >0 ; --i) {
                if(allFor[i-1].checked){
                  allFor[i-1].checked=false;
                }
        }
        this.is_del=false;
      },
      put(index){
            let nm=this.list.at(index).title;
            console.log(nm);
          
            let allFor = document.getElementsByClassName("checkbox");
            
            this.is_del=false;
            for (let i = 0; i < allFor.length; i++) {
              console.log(i);
                console.log(allFor[i].checked);
                if(allFor[i].checked){
                  console.log(allFor[i]);
                  this.is_del=true;
                  break;
                }
                
            }
            console.log(this.is_del);
        },
        say(){
          const obj={"userId": 1,
         "id": this.list.length,
         "title": this.name,
         "completed": false  };
          this.list.push(obj);
          console.log(obj.title);
        }
      },
     
      mounted(){
      fetch( 'https://jsonplaceholder.typicode.com/todos')
      .then(response =>response.json())
      .then((json) => (this.list=json));

  }
}
</script>

<template>
 <div class="content">
    <h1  class="H1">Список задач</h1>
    <p>Здесь можно записать свои задачи.</p>
    <hr>
    <input id="inp" type="text" placeholder="Введите имя" v-model="name"><br>
    <button  v-if="name=='' " disabled>Введите задачу</button>
    <button  v-else @click=" say()">Добавить в список</button><br>
    <button  @click=" sort()" >Сортировка</button>
    <button  v-if="is_del!=false"  @click="del()">Удалить выделенное</button>
    
    <div  class="for"
    v-for="(it, ind) in list" @click="put(ind)">
         {{ind+1}}.  {{ it.title }}
         <input class="checkbox" type="checkbox"  >  
   
  </div>

  </div>
 
</template>

<style scoped>
body{
  padding: 0;
  margin: 0;
  text-align: center;
  background-color: rgb(166, 185, 245);
}
.content{
  width: 500px;
  height: 80%;
  border-radius: 40px;
  text-align: center;
  margin-top: 50px;
  background-color: rgb(174, 211, 243);
}
h1{
  text-align: center;
}
p{
  text-align: center;
}
button{
  margin-top: 10px;
  align-self: left;
}
.for{
  margin-left: 20px;
  text-align: left;
  list-style-type: none;
}
.for:hover{
  background-color: rgb(250, 249, 249);
  margin-left: 20px;
  text-align: left;
  list-style-type: none;
}
.for:active{
  background-color: rgb(236, 150, 45);
  margin-left: 20px;
  text-align: left;
  list-style-type: none;
}

</style>
