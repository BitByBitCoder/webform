<script setup>
import { ref } from "vue";

const email = ref("");
const password = ref("");
let role = ref("");
const checkbox = ref("false");
let tempSkill = "";
let skill = ref([]);
let passwordError = ref("");

function addSkill(e) {
  console.log(e);
  if (e.key === "," && tempSkill) {
    if (!skill.value.includes(tempSkill)) {
      skill.value.push(tempSkill);
    }
    tempSkill = "";
  }

  console.log(skill);
}

function deleteSkill(skills) {
  skill.value = skill.value.filter((item) => {
    return skills !== item;
  });
}

function handleSubmit() {
  //validate password
  console.log("handle submit");
  passwordError.value =
    password.value.length > 5 ? "" : "Password must be 6 character long";
  if (!passwordError.value) {
    console.log("hello");
  }
}
</script>
<template>
  <div>
    <h1>hellow</h1>
    <form @submit.prevent="handleSubmit">
      <label for="">Name:</label>
      <input v-model="email" type="email" required />
      <br />
      <label for="">Password:</label>

      <input v-model="password" type="password" required />
      <div v-if="passwordError">{{ passwordError }}</div>
      <br />
      <label>Role</label>
      <select v-model="role">
        <option value="developer">web dev</option>
        <option value="programmer">Programmer</option>
      </select>

      <label for="">Skills</label>
      <input type="text" v-model="tempSkill" @keyup.alt="addSkill" />
      <div v-for="skill in skill" :key="skill">
        <span @click="deleteSkill(skill)">{{ skill }}</span>
      </div>
      <br />
      <label>Accept term and condition</label>
      <input v-model="checkbox" type="checkbox" required />
      <br />
      <button type="submit">submit</button>
    </form>
    <h1>{{ email }}</h1>
    <h1>{{ password }}</h1>
    <h1>Role: {{ role }}</h1>
    <h1>{{ checkbox }}</h1>
    <h1>skills:{{ skill }}</h1>
  </div>
</template>

<style></style>
