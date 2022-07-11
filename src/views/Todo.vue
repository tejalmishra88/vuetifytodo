<template>
<div class="home">
     <v-text-field
     v-model="newTaskTitle"
     @click:append ="addtask"
     @keyup.enter="addtask"
     class="pa-3"
            outlined
            label="Add Task"
            append-icon="mdi-plus"
            hide-detais
            clearable
          ></v-text-field>
    <v-list  class= "pt-0" flat >
    <div v-for="task in Tasks" :key="task.id">
      <v-list-item @click="donetask(task.id)"  :class="{'blue lighten-5' : task.done}">      
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox    :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title 
              :class= "{ 'text-decoration-line-through' :task.done}">
                {{task}}{{total}}</v-list-item-title>              
            </v-list-item-content>

             <v-btn  @click.stop="plusone(task.id)" class="mx-2"  fab  dark color="indigo"> <v-icon dark>  mdi-plus  </v-icon>  </v-btn>

        <v-list-item-action>
          <v-btn @click.stop="deleteTask(task.id)" icon>
            <v-icon color="primary lighten-1">mdi-delete</v-icon>
          </v-btn>
        </v-list-item-action>
          </template>
          </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
    
</div>
</template>
<script>
    export default{
        name:'home',
        data(){
            return{ total:0,
              newTaskTitle: 'hello',
                Tasks:[
                   {  id: 1, title:'Wake Up1', done:false, volume: 5 }, 
                   {  id: 2, title:'Wa2', done:false, volume:6 }, 
                   {  id: 3, title:'Wake Up3', done:false, volume: 4},
                    {  id: 4, title:'noo Up4', done:false, volume: 2}
                ]
            }
        },
        methods:{
          addtask(){
            let newtask ={
              id: Date.now(),
              title: this.newTaskTitle,
              done:false
            }
            this.Tasks.push(newtask)
            this.newTaskTitle = ''
          },
          donetask(id)
          { console.log('clicked id=',id)
            let t=this.Tasks.filter(c=> c.id=== id)[0]
            t.done = !t.done
            console.log('task=',t)
          },
          plusone(id){
             console.log('plus bbbclicked id=',id) 
             this.Tasks.forEach( onetask => {
                console.log('one task',onetask.volume)
                this.total=this.total + onetask.volume
                console.log('total=',this.total)
              }
             )
          },
          deleteTask(id){
            console.log('clicked id=',id)
            this.Tasks = this.Tasks.filter(task => task.id !==id)
          }
        }
    }
</script>