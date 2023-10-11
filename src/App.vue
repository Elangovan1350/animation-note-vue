<script setup>
import { ref, reactive } from 'vue'
const notes = ref([

])
const newNote = ref("")
const addNote = () => {
  if (newNote.value.length >= 10) {
    notes.value.push({
      id: Math.floor(Math.random() * 100000000),
      note: newNote.value,
      bgColor: `hsl(${Math.floor(Math.random() * 350)},85%,85%)`,
      done: false

    })
    newNote.value = ""
  }

}


const elo = (index) => {
  notes.value.splice(index, 1)
}


</script>

<template>
  <div>
    <div class="addtext">
      <textarea rows="5" type="text" v-model.trim="newNote" placeholder="Add Note Here" @keydown.enter="addNote"> </textarea>
      <button @click="addNote">Add Note</button>
    </div>
    <section>
      <TransitionGroup name="list">
        <div v-for="(i, index) in notes" :key="i.id" :style="{ backgroundColor: i.bgColor }">
          <p :style="{ textDecoration: i.done ? 'line-through  2px' : '' }">{{ i.note }}</p>
          <div class="button1">
          <button @click="i.done = !i.done">done</button>
          <button @click="elo(index)">delete</button>
        </div>
        </div>
      </TransitionGroup>
    </section>

  </div>
</template>

<style scoped>
.button1{
  display: flex;
  justify-content: space-around;
  align-items: center;
  height: 50px;
  
}
textarea {
  width: 700px;
  margin-top: 10px;
  margin-bottom: 10px;
  padding: 10px;
}

.addtext {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

button {
  padding: 10px 20px;
  background-color: transparent;
}

section {
  display: flex;
  flex-wrap: wrap;
  overflow: hidden;
}

section>div {
  margin: 20px;
}

p {

  padding: 20px;
  width: 200px;
  height: 200px;
  font-size: large;
  font-weight: 500;
  color: gray;
  text-decoration-color: rgb(255, 0, 0);
}

.list-enter-from {
  opacity: 0;
  scale: 0;
  translate: 500px 0;
  rotate: 360deg;
}

.list-enter-to {
  opacity: 1;
  scale: 1;
  rotate: 0deg;

}

.list-enter-active {
  transition: all 1s ease;
}

.list-leave-from {
  translate: 0px 0;
  opacity: 1;
  scale: 1;
  rotate: 0deg;

}

.list-leave-to {
  opacity: 0;
  scale: 0;
  rotate: 360deg;

}

.list-leave-active {
  transition: all 1s ease;
}

@media screen and (max-width: 720px) {
  textarea {
    width: 100%;
  }
  section{
    justify-content: center;
  }

}
</style>