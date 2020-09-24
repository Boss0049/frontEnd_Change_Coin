<template>
  <div class="hello">
    <label id="coin"
      ><input for="coin" type="number" v-model="coin" />EUR</label
    >
    <vSelect :options="options" v-model="currency"></vSelect>
    <h1>{{ sum }}</h1>
    <button v-on:click="getData">SUBMIT</button>
  </div>
</template>

<script>
import axios from "axios";
import vSelect from "vue-select";
import "vue-select/dist/vue-select.css";

export default {
  name: "HelloWorld",
  components: { vSelect },
  data() {
    return {
      coin: "",
      sum: "",
      currency: "",
      options: ["THB", "USD", "JPY"],
    };
  },
  computed: {},
  methods: {
    getData() {
      axios
        .post("http://localhost:8000", {
          coin: this.coin,
          currency: this.currency,
        })
        .then((res) => {
          this.sum = res.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
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
