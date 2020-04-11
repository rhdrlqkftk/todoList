<template>
    <div>
        <v-card  
        class= "pa-3 mb-1" 
        :class="{'done': list.status ==='done'}"
        pd-3
        v-for="(list,index) in todoLt"
        :key="index">
        <!--만약 list.status==='done'라면 done 이라는 style이 적용  -->
        <!-- 키로 index를 쓰는 이유는 그 객체의 
        위치값을 알기위해서 저렇게 써준다.
        class = " " 해줘야 기능이 2개일 때 처먹는다.   
        -->
            <p>{{list.memo}}</p>
            
            <v-btn 
                v-if="list.status ==='created'"
                @click="$emit('statusControl', index, 'done')"
                fab small flat color ="green">
                OK
            </v-btn> 
            <!-- fab는 동그라미, flat은 클릭되야만 활성화-->
            
            <v-btn 
            v-else
            @click="$emit('statusControl',index, 'created')"
            fab small flat color ="gray"> R E</v-btn>
            
            <v-btn 
            @click="$emit('listDelete',index)"
            fab small flat color ="red">
            DEL
            </v-btn> 

            <v-btn 
            @click="listEt(list.memo, index)"
            v-if="list.status==='created'"
            fab small flat color ="yellow">
            EDIT
            </v-btn>     

        </v-card>
    </div>
</template>

<script>
import {eventBus} from "../main.js"
export default {
    props:["todoLt"],
     //부모로부터 받아옴.
    methods:
    {
        listEt(memo, index)
        {
            eventBus.listEdit(memo, index)

        }
    }
}
</script>
<style scoped>
/* list.vue에서만 작동을 함. */
.done{
    background-color: rgba(0,0,0,0.1);
}
.done p
{
    text-decoration: line-through; 
    color:  rgba(0,0,0,0.5);

}
</style>