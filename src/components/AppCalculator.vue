<template>
  <div id="calculator">
    <div class="container">
      <table>
        <tr>
          <td colspan="5">
            <div id="screen">
              <span id="screen_top" v-text="display"></span>
              <div id="screen_bottom">
                <span id="operand1" v-text="display_num">0</span>
                <span id="operator"></span>
                <span id="operand2"></span>
              </div>
              <!-- <span id="screen_bottom">0</span> -->
            </div>
          </td>
        </tr>
        <tr>
          <td>
            <button type="button" class="btn btn-warning">MC</button>
          </td>
          <td>
            <button type="button" class="btn btn-warning">MR</button>
          </td>
          <td>
            <button type="button" class="btn btn-warning">M-</button>
          </td>
          <td>
            <button type="button" class="btn btn-warning">M+</button>
          </td>
          <td>
            <button @click="clearNumber()" type="button" class="btn btn-light">
              <i class="fa fa-long-arrow-right" aria-hidden="true"></i>
            </button>
          </td>
        </tr>
        <tr>
          <td>
            <button @click="inputNumber(7)" type="button" class="btn btn-light">
              7
            </button>
          </td>
          <td>
            <button @click="inputNumber(8)" type="button" class="btn btn-light">
              8
            </button>
          </td>
          <td>
            <button @click="inputNumber(9)" type="button" class="btn btn-light">
              9
            </button>
          </td>
          <td>
            <button
              @click="calculate('div')"
              type="button"
              class="btn btn-secondary"
            >
              ÷
            </button>
          </td>
          <td>
            <button @click="changeNumber()" type="button" class="btn btn-light">
              +/-
            </button>
          </td>
        </tr>
        <tr>
          <td>
            <button @click="inputNumber(4)" type="button" class="btn btn-light">
              4
            </button>
          </td>
          <td>
            <button @click="inputNumber(5)" type="button" class="btn btn-light">
              5
            </button>
          </td>
          <td>
            <button @click="inputNumber(6)" type="button" class="btn btn-light">
              6
            </button>
          </td>
          <td>
            <button
              @click="calculate('mul')"
              type="button"
              class="btn btn-secondary"
            >
              x
            </button>
          </td>
          <td>
            <button
              @click="calculate('sub')"
              type="button"
              class="btn btn-secondary"
            >
              -
            </button>
          </td>
        </tr>
        <tr>
          <td>
            <button @click="inputNumber(1)" type="button" class="btn btn-light">
              1
            </button>
          </td>
          <td>
            <button
              v-on:click="inputNumber(2)"
              type="button"
              class="btn btn-light"
            >
              2
            </button>
          </td>
          <td>
            <button
              v-on:click="inputNumber(3)"
              type="button"
              class="btn btn-light"
            >
              3
            </button>
          </td>
          <td rowspan="2">
            <button
              @click="calculate('add')"
              type="button"
              class="btn btn-secondary long-btn"
            >
              +
            </button>
          </td>
          <td rowspan="2">
            <button
              @click="equal()"
              type="button"
              class="btn btn-primary long-btn"
            >
              =
            </button>
          </td>
        </tr>
        <tr>
          <td>
            <button @click="clear()" type="button" class="btn btn-danger">
              C
            </button>
          </td>
          <td>
            <button @click="inputNumber(0)" type="button" class="btn btn-light">
              0
            </button>
          </td>
          <td>
            <button @click="pointNumber()" type="button" class="btn btn-light">
              .
            </button>
          </td>
        </tr>
      </table>
    </div>
    <div class="alert alert-danger" id="message_panel" role="alert">
      something wrong here
    </div>
  </div>
</template>

<script>
export default {
  name: "AppCalculator",
  data() {
    return {
      display_num: 0,
      display: "",
      type: "",
      old_type: "",
      first_num: 0,
      result: 0.1,
    };
  },

  methods: {
    inputNumber: function (number) {
      if (typeof this.display_num == "string") {
        this.display_num = this.display_num + number;
        console.log(this.display_num);
      } else {
        this.display_num = this.display_num * 10 + number;
        console.log(this.display_num);
      }
    },

    pointNumber: function () {
      this.display_num = this.display_num + ".";
      console.log(typeof this.display_num);
    },

    calculate: function (type) {
      if (typeof this.display_num == "string") {
        this.display_num = parseFloat(this.display_num);
        this.first_num = this.display_num;
        this.display = this.first_num.toString();
        this.display_num = 0;
      } else if (this.display_num != 0) {
        this.first_num = this.display_num;
        this.display = this.first_num.toString();
        this.display_num = 0;
      }
      this.old_type = type;
    },

    equal: function () {
      if (typeof this.display_num == "string") {
        this.display_num = parseFloat(this.display_num);
      }
      if (this.old_type == "sub") {
        this.display += " - " + this.display_num.toString() + "=";
        this.result = this.first_num - this.display_num;
        this.display_num = this.result;
      } else if (this.old_type == "add") {
        this.display += " + " + this.display_num.toString() + "=";
        this.result = this.first_num + this.display_num;
        this.display_num = this.result;
      } else if (this.old_type == "mul") {
        this.display += " x " + this.display_num.toString() + "=";
        this.result = this.first_num * this.display_num;
        this.display_num = this.result;
      } else if (this.old_type == "div") {
        this.display += " / " + this.display_num.toString() + "=";
        this.result = this.first_num / this.display_num;
        this.display_num = this.result;
      }

      this.old_type = "";
    },
    changeNumber: function () {
      if (this.display_num > 0) {
        this.display_num = this.display_num * -1;
      } else {
        this.display_num = this.display_num * -1;
      }
    },
    clearNumber: function () {
      this.display_num = 0;
    },
    clear: function () {
      this.display_num = 0;
      this.first_num = 0;
      this.result = 0;
      this.display = "";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css");
.container {
  margin-top: 10em;
  width: 300px;
  border: 1px solid black;
  padding-top: 20px;
  padding-bottom: 20px;
}
table {
  border-spacing: 7px;
  border-collapse: separate;
}
#screen {
  border: 1px solid black;
  padding: 7px;
  width: 100%;
  height: 4em;
}
#screen_top {
  display: block;
  font-size: 0.8rem;
}
#screen_bottom {
  font-size: 1.8rem;
  display: block;
  text-align: right;
}
#operand2 {
  background-color: skyblue;
}
#operator {
  background-color: rosybrown;
}
.button-row {
  display: flex;
  justify-content: space-between;
}
button {
  width: 45px;
}
.long-btn {
  display: inline-block;
  height: 80px;
}

/* Message panel */
#message_panel {
  width: 300px;
  margin-top: 1em;
  display: none;
  margin-left: auto;
  margin-right: auto;
}
</style>
