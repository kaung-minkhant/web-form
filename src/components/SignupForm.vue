<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email" />

    <label>Password:</label>
    <input type="password" required v-model="password" />
    <div v-if="passwordError" class="text-input-error">{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <!-- keyboard events -->
    <label>Skills: (Comma seperated)</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill" />
    <div
      v-for="skill in skills"
      :key="skill"
      class="pill"
      @click="removeSkill(skill)"
    >
      {{ skill }}
    </div>

    <!-- checkbox 1: single checkbox -->
    <div class="terms">
      <input type="checkbox" required v-model="terms" />
      <label>Accept terms and conditions</label>
    </div>

    <!-- checkbox 2: group of checkboxes -->
    <div>
      <input type="checkbox" value="shunn" v-model="names" />
      <label>Shunn</label>
    </div>
    <div>
      <input type="checkbox" value="kaung" v-model="names" />
      <label>Kaung</label>
    </div>
    <div>
      <input type="checkbox" value="shally" v-model="names" />
      <label>Shally</label>
    </div>

    <div class="submit">
      <button>Create an Account</button>
    </div>
  </form>

  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms Accepted: {{ terms }}</p>
  <p>Names: {{ names }}</p>
  <p>Skills: {{ skills }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: "mario@gmail.com",
      password: "abcd",
      role: "developer",
      terms: true,
      names: [],
      tempSkill: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        let tempSkill = this.tempSkill.substring(0, this.tempSkill.length - 1);
        if (!this.skills.includes(tempSkill)) {
          this.skills.push(tempSkill);
        }
        this.tempSkill = "";
      }
    },
    removeSkill(skill) {
      // let index = this.skills.indexOf(skill)
      // this.skills.splice(index, 1)

      this.skills = this.skills.filter((item) => item !== skill);
    },
    handleSubmit() {
      // validate password
      this.passwordError =
        this.password.length > 5
          ? ""
          : "Password must be at least 5 characters!";

      if (!this.passwordError) {
        console.log("email: ", this.email);
        console.log("password: ", this.password);
        console.log("role: ", this.role);
        console.log("skills: ", this.skills);
        console.log("terms accepted: ", this.terms);
      }
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background-color: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.9em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}

input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: -1px;
}

/* .pill {
    display: inline-block;
    margin-top: 1rem;
    margin-right: 0.5rem;
    padding: 0.2rem 1rem;
    border-radius: 1.5rem;
    background-color: aquamarine;
    color: red;
} */

.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background-color: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}

button {
  background-color: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
  cursor: pointer;
}

.submit {
  text-align: center;
}

.text-input-error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8rem;
  font-weight: bold;
}
</style>