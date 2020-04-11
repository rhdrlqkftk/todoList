<template>
<v-container>
  <v-layout row wrap> 
    <v-flex xs12 text-xs-center>
    <h1> To Do List </h1>
    <p>전체 할일:{{todoList.length}},  완료된 할일:{{ countDone }},  남은 할일:{{ (todoList.length - countDone)}} </p>
    </v-flex>
    <v-flex xs6 pa-2>
      <ListAdd 
      @listJW="listAdd"
      @listEdit="listEditJW"
      ></ListAdd> 
    </v-flex>
    <v-flex xs6 pa-2>
      <List
      :todoLt="todoList"
      @statusControl="statusControl"
      @listDelete="listDel"
      ></List> 
       <!--:todoLt란 이름으로 todoList의 내용을 자식으로 보내줌  -->
      <!-- statusControl이란 이름으로 자식으로 부터 내용을 받음 -->
      <!-- statusControl()를 붙이면 안된다. 인자값이 없는건 상관없지만, 받아올때, 
      받아올 떄 인자값이 있는 경우, ()를 쓰면 빈값으로 인식하기 때문에. 
       -->
     
      <!-- <List/> -->
    </v-flex>
  </v-layout>
</v-container>
</template>

<script>
import List from './List'
import ListAdd from './ListAdd'


export default {
  data() {
    return {
      todoList: []
    }
  },
  methods: {
    listAdd(memo) {
      console.log("받았어!")
      this.todoList.push({ memo: memo, status:"created"})
      // 
    },
    statusControl(index, status)
    {
      this.todoList[index].status = status
    }, 
    listDel(index)
    {
        this.todoList.splice(index,1);
        //인덱스에서 하나만 삭제한다는 의미. 
    }
    ,
    listEditJW(memo, index)
    {
        this.todoList[index].memo =memo;
    }
  },
  computed:
  {
      countDone()
      {
          let count =0; 
          this.todoList.forEach(list=>
          {
            if(list.status==='done')
            {
              count++;
            }
          })
          return count
      }
  },
  components:
  {
    List, 
    ListAdd
  }

//data에 기본 정의를 해주어야 된다. 
//그래야 undefined가 안뜬다. 
// 프롭스 캡퍼 
}
</script>