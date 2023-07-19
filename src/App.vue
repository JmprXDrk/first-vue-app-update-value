<template>
  <div class="app">
    <h1>First VueJS App: Update Value</h1>
    <div
      @click="showModalWindow(student)"
      class="students"
      v-for="(student, index) in students"
      :key="index"
    >
      <div><strong>Student Name: </strong>{{ student.name }}</div>
      <div class="info"><strong>Student Info: </strong>{{ student.value }}</div>
    </div>
    <custom-modal v-model:isShow="modalWindow" :student="modalData">
      <form @submit.prevent="updateValue(value, modalData)">
        <h3>Update {{ modalData.name }} Info</h3>
        <input
          class="input"
          type="text"
          v-bind:value="modalData.value"
          @input="value = $event.target.value"
        />
        <div class="buttons">
          <button class="btn">Save</button>
          <button class="btn" @click="notUpdateValue">Cancel</button>
        </div>
      </form>
    </custom-modal>
  </div>
</template>

<script>
const students = [
  {
    name: 'Carl',
    value: 'course 1',
  },
  {
    name: 'Sarah',
    value: 'course 3',
  },
  {
    name: 'Tom',
    value: 'course 1',
  },
  {
    name: 'Robert',
    value: 'course 5',
  },
  {
    name: 'Ivan',
    value: 'course 1',
  },
  {
    name: 'Nick',
    value: 'course 2',
  },
  {
    name: 'Rachel',
    value: 'course 3',
  },
  {
    name: 'John',
    value: 'course 2',
  },
  {
    name: 'Beth',
    value: 'course 4',
  },
  {
    name: 'Tim',
    value: 'course 6',
  },
  {
    name: 'Luke',
    value: 'course 1',
  },
  {
    name: 'Barry',
    value: 'course 2',
  },
  {
    name: 'Dan',
    value: 'course 3',
  },
  {
    name: 'Elizabeth',
    value: 'course 5',
  },
  {
    name: 'Gabby',
    value: 'course 2',
  },
  {
    name: 'Sam',
    value: 'course 3',
  },
  {
    name: 'Jessica',
    value: 'course 4',
  },
  {
    name: 'Igor',
    value: 'course 1',
  },
  {
    name: 'Daisy',
    value: 'course 5',
  },
  {
    name: 'Alex',
    value: 'course 6',
  },
]

export default {
  data() {
    return {
      students,
      value: '',
      modalWindow: false,
      modalData: null,
    }
  },
  mounted() {
    if (localStorage.getItem('students')) {
      try {
        this.students = JSON.parse(localStorage.getItem('students'))
      } catch (error) {
        localStorage.removeItem('students')
      }
    }
  },
  methods: {
    updateValue(value, data) {
      this.students.forEach((student) => {
        if (student === data) student.value = value
      })
      const parsedStudent = JSON.stringify(this.students)
      localStorage.setItem('students', parsedStudent)
      this.modalWindow = false
    },
    notUpdateValue() {
      this.students = JSON.parse(localStorage.getItem('students'))
      this.modalWindow = false
    },
    showModalWindow(student) {
      this.modalData = student
      this.modalWindow = true
    },
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Josefin+Sans:ital,wght@0,400;0,700;1,400');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
a {
  text-decoration: none;
}
:root {
  --index: calc(1vh + 1vw);
}
h1 {
  text-align: center;
  color: rgb(248, 143, 6);
  margin-top: 15px;
}
.students {
  margin: auto;
  margin-top: var(--index);
  margin-bottom: var(--index);
  background-color: rgb(57, 202, 84);
  width: 70vw;
  padding: var(--index);
  border: 3px solid rgb(252, 210, 23);
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.4s ease, box-shadow 0.4s ease;
  font-size: calc(var(--index) * 1.25);
  font-family: 'Josefin Sans', sans-serif;
  line-height: calc(var(--index) * 1.5);
}
.students > button {
  cursor: pointer;
}
.students:hover {
  background-color: rgb(7, 153, 153);
  box-shadow: rgb(252, 210, 23) 5px -5px 10px;
}
.info {
  word-break: break-all;
}
.students > div > strong {
  margin-right: 10px;
}
form {
  font-size: calc(var(--index) * 1.25);
  font-family: 'Josefin Sans', sans-serif;
  line-height: calc(var(--index) * 1.5);
}
form > h3 {
  text-align: center;
}
.input {
  width: 100%;
  height: calc(var(--index) * 1.5);
  border-radius: 8px;
  padding: 12px 10px;
  margin: 8px 0;
  box-sizing: border-box;
  font-size: medium;
}
.buttons {
  display: flex;
  justify-content: center;
  margin-top: 4px;
}
.btn {
  height: 5vh;
  width: 5vw;
  border-radius: 8px;
  background: #1b68e3;
  margin-left: 5px;
  cursor: pointer;
  transition: height 0.4s ease, width 0.4s ease, background-color 0.4s ease;
}
.btn:hover {
  height: 5.25vh;
  width: 5.25vw;
  background: #658bc8;
}
</style>
