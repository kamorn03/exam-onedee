<template>
  <div class="form">
   form
  </div>
</template>

<script>
// import { Field, Form } from "vee-validate";
export default {
  components: {
    // Field,
    // Form,
  },
  methods: {
    isRequired(value) {
      return value ? true : "This field is required";
    },
  },
  name: "FormPage",
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
