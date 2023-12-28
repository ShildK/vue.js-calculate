<script>
export default {
   name: "CalculateDisplay",
   props: {
    expressionValue: {
        type: String
    },
    resultValue: {
        type: Number
    }
   }
};
</script>

<template>
   <div class="calculate__display">
      <div class="expression">{{ expressionValue }}</div>
      <div class="result">{{ resultValue }}</div>
   </div>
</template>

<style scoped>
.calculate__display {
   width: 85%;
   height: 150px;
   margin-top: 30px;
}
.expression {
   height: 40px;

   font-weight: 300;
   font-size: 32px;

   opacity: 0.4;
   text-align: right;
}
.result {
   height: 80px;
   font-size: 46px;
   text-align: right;

   margin-left: 30px;
   overflow: hidden;
}
</style>
