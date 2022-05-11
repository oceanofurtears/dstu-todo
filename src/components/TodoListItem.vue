<template>
  <div class="todo">
    <div class="colorline" :class="{'colorLineDoneCompleted': !progress}"/>
    <div class="todobg"/>
    <div v-if="!editing">
      <div class="todotext" :class="{'textDoneCompleted': !progress}"> {{ content }}  </div>
      
      <div class="controlButtons">
        <button class="controlButtonEdit material-icons" @click="nowEditing">edit</button>
        <button class="controlButtonDone material-icons" :class="{'controlButtonDoneCompleted': !progress}" @click="toggleTodo">done</button>
        <button class="controlButtonCancel material-icons" @click="rem">cancel</button>
      </div>
    </div>
    <div v-else>
      <div class="todotext">
        <input class="todoinput" @keydown.enter="updateTodo" v-model="newContent"/>
        <input class="todoinput" @keydown.enter="updateTodo" v-model="newDate"/>
      </div>
      <div class="controlButtons">
          <button class="controlButtonAdd material-icons" @click="updateTodo">done</button>
          <button class="controlButtonCancel material-icons" @click="cancelUpdateTodo">cancel</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  props: ['content', 'id', 'progress', 'date'],
  emits: ['changedProgress', 'remmed', 'updatedContent'],
}
</script>

<style scoped>
.todo{
  position: relative;
  height: 100px;
  max-width: 1200px;
  margin: auto;
  text-align: center;

  display: flex;
}

.todobg{
  position: absolute;
  top: 0;
  left: 1%;
  z-index: -1;
  margin: auto ;
  background: whitesmoke;
  border-radius: 20px;
  height: 100%;
  width: 99%;

  max-width: 1200px;
  display: flex;

  border: 1px solid #c4c4c4;
}

.colorline{
  position: absolute;
  top: 2%;
  left: 0;
  margin: auto;
  z-index: -2;
  margin: auto ;
  background: coral;
  border-radius: 20px;
  height: 96%;
  width: 100%;


}

.colorLineDoneCompleted{
   background: green; 
}
.todotext{
  position: absolute;
  margin-left: 4%;
  display: flex;
  justify-content: left;
  text-align: left;
  align-items: center;
  height: 100%;
  max-width: 80%;

  font-size: 20px;
  word-wrap: break-word;
}
.tododate{
  position: absolute;
  margin-left: 5%;
  margin-top: 3%;
  display: flex;
  justify-content: left;
  text-align: left;
  align-items: center;
  height: 100%;
  width: 67%;

  color: grey;
}
.textDoneCompleted{
    text-decoration: line-through;
    color: #ff3232;
    opacity: 0.8;
}
.controlButtons{
  margin-right: 5%;
  position: absolute;
  top: 0;
  right: -5%;
  width: 12%;
  height: 100%;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}
.controlButtonDone,  .controlButtonCancel, .controlButtonEdit, .controlButtonAdd{
  color: black;
  cursor: pointer;
  padding: 0;
  margin: 0;
  border: none;
  text-align: center;
  background: whitesmoke;
  transition: all 0.2s ease;
}
.controlButtonDone:hover,  .controlButtonCancel:hover, .controlButtonEdit:hover, .controlButtonAdd:hover{
  transition: all 0.2s ease;
  transform: scale(1.2);
}
.controlButtonDoneCompleted, .controlButtonAdd{
  color: green;
}

.controlButtonCancel{
  color: red;
}
.todoinput{
    color: rgb(60, 60, 60);
    width: 100%;
    border-radius: 20px;
    border: 1px lightslategray solid;
    padding-top: 10px;
    padding-bottom: 10px;;
    padding-left: 10px;
    padding-right: 10px;
    transition: all 0.2s ease;
    background: whitesmoke;
}
.todoinput:focus{
    transition: all 0.2s ease;
    transform: scale(1.025);
    border: 2px lightslategray solid;
    outline: none;
}
</style>