<template>
    <MDBCard>
      <MDBCardBody>
        <MDBCardTitle>{{ task.name }}</MDBCardTitle>
        <div class="abso">
            <span class="ribbon" :class="{green: props.task.status == 'completed' }">{{ props.task.status == 'completed' ? 'done' : 'To Do' }}</span>
        </div>
        <MDBCardText>
            {{ task.desc }}
        </MDBCardText>
        <div class="flexer">
            <MDBBtn @click="completeFn" color="primary">{{props.task.status != 'completed' ? 'Complete' : 'Undo'}}</MDBBtn>
            <MDBBtn @click="$emit('edit', ['edit',index])" color="warning">Edit</MDBBtn>
            <MDBBtn @click="$emit('delete', [index, true])" color="danger">Delete</MDBBtn>
        </div>
      </MDBCardBody>
    </MDBCard>
  </template>

<script setup>
  import party from "party-js";
  import { MDBCard, MDBCardBody, MDBCardTitle, MDBCardText, MDBBtn } from "mdb-vue-ui-kit";
  import { defineProps, defineEmits } from "vue"
    const props = defineProps({
      task: Object,
      index: Number
    })
    const emit = defineEmits(['delete','completed','edit'])
    const completeFn = ($event) => {
        const final = props.task.status == 'completed' ? 'pending' : 'completed'
        emit('completed', [props.index, final])
        if(final == 'completed'){
            party.confetti($event, {
                count: party.variation.range(20, 40),
            });
        }
    }
</script>

<style scoped>
.ribbon {
  width: 60px;
  font-size: 14px;
  padding: 4px;
  position: absolute;
  right: -25px;
  bottom: 0;
  text-align: center;
  border-radius: 25px;
  transform: rotate(20deg);
  background-color: red;
  color: white;
}
.ribbon.green {
    background-color: green;
}
.card {
    max-width: 30%;
    min-height: 183px;
    @media(max-width:1150px){
        width: 50vw
    }

    @media(max-width:900px){
        width: unset;
        max-width: 90% !important;
        margin: 1.5rem auto;
    }
    .flexer {
        @media(max-width:900px){
            display: flex;
        }
        @media(max-width:400px){
            display: block;
        }
    }
}
.abso {
    position: absolute;
    top: 20px;
    right: 10px;
}
.btn {
    @media(max-width:1150px){
        display: block;
        margin-top: 0.5rem;
    }
    
}
.arrow-left {
  width: 0; 
  height: 0; 
  border-top: 10px solid transparent;
  border-bottom: 10px solid transparent; 
  
  border-right:10px solid blue; 
}
</style>

/* Same but with options API */

/* 
<!--
<template>
    <MDBCard>
      <MDBCardBody>
        <MDBCardTitle>{{ task.name }}</MDBCardTitle>
        <div class="abso">
            <span class="ribbon" :class="{green: taskStatus}">{{ taskStatus ? 'Done' : 'To Do' }}</span>
        </div>
        <MDBCardText>
            {{ task.desc }}
        </MDBCardText>
        <div class="flexer">
            <MDBBtn @click="completeFn" color="primary">{{!taskStatus ? 'Complete' : 'Undo'}}</MDBBtn>
            <MDBBtn @click="$emit('edit', ['edit',index])" color="warning">Edit</MDBBtn>
            <MDBBtn @click="$emit('delete', [index, true])" color="danger">Delete</MDBBtn>
        </div>
      </MDBCardBody>
    </MDBCard>
  </template>

<script>
  import party from "party-js";
  import { MDBCard, MDBCardBody, MDBCardTitle, MDBCardText, MDBBtn } from "mdb-vue-ui-kit";
  export default {
    components: {
      MDBCard,
      MDBCardBody,
      MDBCardTitle,
      MDBCardText,
      MDBBtn
    },
    data(){
        return {
            isComplete: false
        }
    },
    props: ['task','index'],
    emits: ['delete','completed','edit'],
    methods: {
        completeFn($event){
            this.isComplete = !this.taskStatus
            this.$emit('completed', [this.index, this.isComplete])
            if(this.isComplete){
                party.confetti($event, {
                    count: party.variation.range(20, 40),
                });
            }
        }
    },
    computed:{
        taskStatus(){
            return this.task.status == 'completed'
        }
    }
  };
</script>

<style scoped>
.ribbon {
  width: 60px;
  font-size: 14px;
  padding: 4px;
  position: absolute;
  right: -25px;
  bottom: 0;
  text-align: center;
  border-radius: 25px;
  transform: rotate(20deg);
  background-color: red;
  color: white;
}
.ribbon.green {
    background-color: green;
}
.card {
    max-width: 30%;
    min-height: 183px;
    @media(max-width:1150px){
        width: 50vw
    }

    @media(max-width:900px){
        width: unset;
        max-width: 90% !important;
        margin: 1.5rem auto;
    }
    .flexer {
        @media(max-width:900px){
            display: flex;
        }
        @media(max-width:400px){
            display: block;
        }
    }
}
.abso {
    position: absolute;
    top: 20px;
    right: 10px;
}
.btn {
    @media(max-width:1150px){
        display: block;
        margin-top: 0.5rem;
    }
    
}
.arrow-left {
  width: 0; 
  height: 0; 
  border-top: 10px solid transparent;
  border-bottom: 10px solid transparent; 
  
  border-right:10px solid blue; 
}
</style>
-->
*/