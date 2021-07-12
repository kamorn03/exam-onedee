<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <b-card title="Card Title" tag="article" style="padding 15px" class="mb-2">
      <form
        id="app"
        @submit="checkForm"
        action="https://vuejs.org/"
        method="post"
      >
        <p v-if="errors.length">
          <b>Form and Validations</b>
        </p>

        <p>
          <label for="firstname">First Name</label>
          <input
            id="firstname"
            v-model="firstname"
            type="text"
            name="firstname"
          />
        </p>

        <p>
          <label for="lastname">Last Name</label>
          <input id="lastname" v-model="lastname" type="text" name="lastname" />
        </p>

        <p>
          <label for="email">E-mail </label>
          <!-- validate emaila -->
          <input
            id="email"
            v-validate="'required|email'"
            v-model="email"
            type="text"
            name="email"
          />
        </p>

        <p>
          <label for="password">Password</label>
          <input id="password" v-model="password" type="text" name="name" />
        </p>

        <p>
          <label for="veri-password">Varify Password</label>
          <input
            id="veri-password"
            v-model="veri_password"
            type="number"
            name="veri-password"
            min="0"
          />
        </p>

        <!-- test error -->
        <p style="color: red">
          {{ errors.gender }}
        </p>

        <p>
          <label for="gender">Gender</label>
          <select id="gender" v-model="gender" name="gender">
            <option>male</option>
            <option>female</option>
          </select>
        </p>

        <p>
          <!-- <input type="submit" value="Submit" /> -->
          <b-button type="submit" value="Submit" variant="primary"
            >submit</b-button
          >
        </p>
      </form>
    </b-card>

    <div v-if="result">result ::</div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      errors: {
        firstname: "",
        lastname: "",
        email: "",
        password: "",
        veri_password: "",
        gender: "",
      },
      firstname: "",
      lastname: "",
      email: "",
      password: "",
      veri_password: "",
      gender: "",
      result: false,
    };
  },
  props: {
    msg: String,
  },
  methods: {
    checkForm(e) {
      // if (this.name && this.age) {
      //   return true;
      // }

      // this.errors = [];

      // if (!this.name) {
      // this.errors.push("Name required.");
      // }
      // if (!this.age) {
      // this.errors.push("Age required.");
      // }

      if (!this.gender) {
        this.errors.gender = "pls select gender.";
      } else {
        this.errors.gender = "";
      }

      // this.result = true

      e.preventDefault();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body {
  background-color: #eee;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
