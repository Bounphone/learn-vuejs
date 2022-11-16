<script>
import { ref } from "@vue/reactivity";
export default {
  name: "App",
  data() {
    return {
      firtName: "olay",
      lastName: "KOSADA",
      nickName: "None",
      age: 15,
      address: "<strong>Vientiane capital</strong>",
      picture: "https://cdn-icons-png.flaticon.com/512/1077/1077012.png",
      size: 150,
      social: "https://netchainlao.com",
      hobby: ["Listen music", "Play game", "Write blog"],
      general: {
        gender: "Male",
        height: 179,
      },
      isVisible: true,
      salaray: 10000
    };
  },
  /// Method
  methods: {
    showDialog() {
      alert(this.firtName);
    },
    increasement(val) {
      this.age += val;
    },
    onSubmit(e) {
      this.nickName = this.$refs.nicknameRef.value;
    },
    toggleVisible() {
      this.isVisible = !this.isVisible;
    },
    addSalary(val){
      this.salaray += val;
    }
  },
  /// Compute
  computed: {
    getFullName() {
      return this.firtName + " " + this.lastName;
    },
    getInCome(){
      return this.salaray * 12;
    },
    getPosition(){
      if(this.salaray < 20000){
        return "Programmer"
      } else {
        return "PM"
      }
    },
  },
  /// Watcher
  watch:{ 
    salaray(value){
      if(value >= 50000){
        alert('Your salary cannot more 50.000')
        setTimeout(() =>{
          this.salaray = 20000
        }, 2000)
      }
    }
  }
};
</script>

<template>
  <section>
    <img :src="picture" alt="" :width="size" :height="size" />
    <form @submit.prevent="onSubmit">
      Enter your nickname: <input type="text" ref="nicknameRef" />
      <button type="submit">Summit</button>
    </form>
    <h1>Salary: {{salaray}} B</h1>
    <h1>Salary per year: {{getInCome}} B</h1>
    <h1>Position: {{getPosition}}</h1>
    <button @click="addSalary(5000)">Add salary</button>
    <button @click="toggleVisible">{{ isVisible ? "Hide" : "Show" }}</button>
    <article v-show="isVisible">
      <h1>Student name: {{ getFullName }}</h1>
      <h1>Student nickName: {{ nickName }}</h1>
      <h1>Student lastName: {{ lastName }}</h1>
      <h1>Student age: {{ age }}</h1>
      <h1>Student address: <span v-html="address"></span></h1>
      <a :href="social">Website</a>

      <h1 v-if="hobby.length === 0">No hobby</h1>
      <div v-else>
        <h1>Hobby:</h1>
        <ul>
          <li v-for="(item, index) in hobby" :key="index">
            {{ index + 1 }}
            {{ item }}
          </li>
        </ul>
      </div>
      <div>
        <h1>Hobby:</h1>
        <ul>
          <li v-for="(item, key) in general" :key="key">
            {{ item }}
          </li>
        </ul>
      </div>
      <button @click="showDialog">Show data</button>
      <button @click="increasement(5)">Increase</button>
    </article>
  </section>
</template>

<style></style>
