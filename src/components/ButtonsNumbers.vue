<script>
export default {
   name: "ButtonsNumbers",
   props: {
      numbersList: {
         type: Array,
         requared: true,
      },
      addValue: {
         type: Function,
         requared: true,
      },
   },
};
</script>

<template>
   <div class="btns__numbers">
      <ButtonNumber
         v-for="number in numbersList"
         @btn-function="addValue(number)"
      >
         {{ number }}
      </ButtonNumber>
      <ButtonNumber class="btn__dot" @btn-function="addValue('.')">
         .
      </ButtonNumber>
      <ButtonNumber class="btn__zero" @btn-function="addValue('0')">
         0
      </ButtonNumber>
   </div>
</template>

<style scoped>
.btns__numbers {
   grid-column-start: 1;
   grid-column-end: 4;
   grid-row-start: 2;
   grid-row-end: 9;

   display: grid;
   grid-template-columns: repeat(3, 65px);
   grid-template-rows: repeat(4, 65px);
   grid-gap: 20px;
}
.btn__zero {
   width: 107px;
   margin-left: 43px;
}
.btn__dot {
   width: 107px;
}
</style>
