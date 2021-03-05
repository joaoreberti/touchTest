<template>
  <div>
    joao
    <br />
    <br />
    <div>
      <input ref="input" v-model="fullString" type="textarea" />
      <select v-model="chosenOption" :size="queryComponents.length" ref="select">
        <option v-for="(option, i) in queryComponents" :value="option" :key="i">
          {{ option }}
        </option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  name: "LoginPage",
  data: function () {
    return {
      fullString: "",
      listComponents: ["andre", "joao", "reberti", "joana", "sofia", "minerva", "rui"],
      listBudgets: ["300", "400", "900", "quinhentos", "mil"],
      queryComponents: [],
      queryBudgets: [],
      chosenOption: "",
      querying: false,
    };
  },
  methods: {
    handleKeyDown: function (event) {
      console.log(event.keyCode);
      if (event.keyCode === 13) {
        console.log(this.fullString.slice(0, this.fullString.indexOf("@")), "ultimo");
        this.fullString =
          this.fullString.slice(0, this.fullString.indexOf("@")) + this.chosenOption;

        return true;
      }
    },
  },
  watch: {
    chosenOption: function () {
      window.addEventListener("keydown", this.handleKeyDown);
    },
    fullString: function (newValue) {
      console.log("new value", newValue);

      if (newValue[newValue.length - 1] === "@") {
        this.querying = "@";
      }

      if (this.querying === "@") {
        let chunk = newValue.slice(newValue.indexOf("@") + 1, newValue.length);

        if (chunk !== "") {
          let newArray = [];
          this.listComponents.filter((word) => {
            if (chunk === word.slice(0, chunk.length)) {
              console.log(word, "minerva");

              newArray.push(word);
            }
          });
          console.log(newArray);
          this.queryComponents = newArray;
          this.$refs.select.focus();
        }
      }
      if (newValue[newValue.length - 1] === "#") {
        alert("reberti");
      }
    },
  },
};
</script>

<style lang="scss" scoped>
input {
  background-color: black;
  color: white;
  font-size: 30px;
}
</style>
