<script>
import CalculateDisplay from "./components/CalculateDisplay.vue";
import ButtonsNumbers from "./components/ButtonsNumbers.vue";
import ButtonsCommands from "./components/ButtonsCommands.vue";

export default {
   components: {
      CalculateDisplay,
      ButtonsNumbers,
      ButtonsCommands,
   },
   data: () => {
      return {
         numbers: ["7", "8", "9", "4", "5", "6", "1", "2", "3"],
         operations: ["x", "+", "-", "="],
         expression: "",
         result: 0,
         numOneStr: "",
         numTwoStr: "",
         command: "",
      };
   },
   methods: {
      addValue(value) {
         if (this.command == "" || this.command == "=") {
            if (this.command == "=") {
               this.command = "";
               this.numOneStr = "";
            }
            if (value == ".") {
               if (this.numOneStr == "") {
                  this.numOneStr = "0";
               } else if (this.numOneStr.includes(".")) {
                  return;
               }
            }
            if (this.numOneStr == "0" && value != ".") {
               this.numOneStr = value;
            } else {
               this.numOneStr = this.numOneStr.toString() + value.toString();
            }
            this.result = this.numOneStr;
         } else if (this.numOneStr != "" && this.command != "") {
            if (value == ".") {
               if (this.numTwoStr == "") {
                  this.numTwoStr = "0";
               } else if (this.numTwoStr.includes(".")) {
                  return;
               }
            }
            if (this.numTwoStr == "0" && value != ".") {
               this.numTwoStr = value;
            } else {
               this.numTwoStr = this.numTwoStr.toString() + value.toString();
            }
            this.result = this.numTwoStr;
         }
      },
      setCommand(value) {
         if (this.numOneStr == "") {
            return;
         }
         if (this.numTwoStr == "") {
            this.command = value;
            return;
         }
         if (this.command == "=") {
            this.numTwoStr = "";
            return;
         }

         this.expression = this.numOneStr + this.command + this.numTwoStr;

         if (this.command == "+") {
            this.numOneStr =
               parseFloat(this.numOneStr) + parseFloat(this.numTwoStr);
         } else if (this.command == "-") {
            this.numOneStr =
               parseFloat(this.numOneStr) - parseFloat(this.numTwoStr);
         } else if (this.command == "x") {
            this.numOneStr =
               parseFloat(this.numOneStr) * parseFloat(this.numTwoStr);
         } else if (this.command == "÷") {
            if (parseFloat(this.numOneStr) % parseFloat(this.numTwoStr) !== 0) {
               this.numOneStr = (
                  parseFloat(this.numOneStr) / parseFloat(this.numTwoStr)
               ).toFixed(4);
            } else {
               this.numOneStr =
                  parseFloat(this.numOneStr) / parseFloat(this.numTwoStr);
            }
         }

         this.result = this.numOneStr;
         this.numTwoStr = "";
         this.command = "";
      },
      clearAll() {
         this.numOneStr = "";
         this.numTwoStr = "";
         this.command = "";
         this.expression = "";
         this.result = 0;
      },
      deleteLastSymbol() {
         if (this.command == "" || this.command == "=") {
            let numberStr = this.numOneStr.toString();
            this.numOneStr =
               numberStr.length == 1 ? "0" : numberStr.slice(0, -1);
            this.result = this.numOneStr;
         }
         if (this.numOneStr != "" && this.command != "") {
            let numberStr = this.numTwoStr.toString();
            this.numTwoStr =
               numberStr.length == 1 ? "0" : numberStr.slice(0, -1);
            this.result = this.numTwoStr;
         }
      },
   },
};
</script>

<template>
   <div class="calculate">
      <CalculateDisplay :expressionValue="expression" :resultValue="result" />
      <div class="calculate__buttons">
         <ButtonCommand class="btn__clear" @btn-function="clearAll">C</ButtonCommand>
         <ButtonCommand class="btn__delete" @btn-function="deleteLastSymbol">⌫</ButtonCommand>
         <ButtonCommand class="btn__division" @btn-function="setCommand('÷')">÷</ButtonCommand>
         <ButtonsNumbers :numbersList="numbers" :addValue="addValue" />
         <ButtonsCommands :operationsList="operations" :setCommand="setCommand" />
      </div>
   </div>
</template>

<style>
.calculate {
   width: 375px;
   height: 600px;
   margin: 50px auto;

   border-radius: 20px;
   box-shadow: 5px 5px 20px #7d7d85;
   background-color: #fff;

   display: flex;
   flex-direction: column;
   align-items: center;
}
.calculate__buttons {
   width: 85%;
   margin-top: 20px;
   display: grid;
   grid-template-columns: repeat(4, 65px);
   grid-template-rows: repeat(5, 65px);
   grid-gap: 20px;
}
.btn__delete {
   width: 95px;
   margin-left: 28px;
}
.btn__division {
   width: 95px;
   margin-left: 56px;
}

.btn__clear {
   width: 95px;
}
</style>
