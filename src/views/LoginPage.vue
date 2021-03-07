<template>
  <div>
    joao
    <br />
    <br />
    <div>
      <input ref="input" v-model="fullString" type="textarea" />
      <div v-html="fullHTML"></div>
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
      fullHTML: "",
      htmlChunks: [],
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
      // //console.log(event.keyCode);
      if (event.keyCode === 13) {
        this.$refs.input.focus();
        // //console.log(this.fullString.slice(0, this.fullString.indexOf("@")), "ultimo");
        this.htmlChunks[this.htmlChunks.length - 1] = this.chosenOption;

        let lastSpacePosition = null;

        for (let i = this.fullString.length; i > 0; i--) {
          if (this.fullString[i] === " " && !lastSpacePosition) {
            lastSpacePosition = i;
            console.log("for loop, i:", i, "lastSpacePostion");
          }
        }

        console.log({
          fullString: this.fullString,
          lastSpacePosition,
          chosenOption: this.chosenOption,
        });

        this.fullString =
          this.fullString.slice(0, lastSpacePosition + 1) +
          this.querying +
          this.chosenOption +
          " ";

        console.log({
          fullString: this.fullString,
          lastSpacePosition,
          chosenOption: this.chosenOption,
        });
        this.querying = false;

        return true;
      }
    },
  },
  watch: {
    chosenOption: function () {
      window.addEventListener("keydown", this.handleKeyDown);
    },
    fullString: function (newValue) {
      //console.log("new value", newValue);

      function filterChunk(chunkToFilter, arrayToSearch) {
        if (chunkToFilter !== "") {
          let newArray = [];
          arrayToSearch.filter((word) => {
            if (chunkToFilter === word.slice(0, chunkToFilter.length)) {
              //console.log(word, "minerva");

              newArray.push(word);
            }
          });
          //console.log(newArray);
          return newArray;
        }
        return false;
      }

      if (newValue[newValue.length - 1] === "#") {
        alert("reberti");
      }
      this.htmlChunks = this.fullString.split(" ");
      this.fullHTML = "";
      if (this.htmlChunks[this.htmlChunks.length - 1].indexOf("@") !== -1) {
        this.querying = "@";
        //console.log("filterChunk");

        this.queryComponents = filterChunk(
          this.htmlChunks[this.htmlChunks.length - 1].slice(1),
          this.listComponents
        );
        if (this.queryComponents.length > 0) {
          this.$refs.select.focus();
        }
      }
      this.htmlChunks.map((chunk) => {
        if (chunk[0] === "@") {
          this.fullHTML =
            this.fullHTML +
            "<span style='color: red;'>" +
            chunk.slice(1, chunk.length) +
            " </span>";
        } else {
          this.fullHTML = this.fullHTML + "<span>" + chunk + " </span>";
        }
      });
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
