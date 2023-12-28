<script>
export default {
   name: "ButtonsCommands",
   props: {
      operationsList: {
         type: Array,
         requared: true,
      },
      setCommand: {
         type: Function,
         requared: true,
      },
   },
};
</script>

<template>
   <div class="btns__commands">
      <ButtonCommand
         class="btn__command"
         v-for="operation in operationsList"
         @btn-function="setCommand(operation)"
      >
         {{ operation }}
      </ButtonCommand>
   </div>
</template>

<style scoped>
.btns__commands {
   grid-column-start: 4;
   grid-column-end: 5;
   grid-row-start: 2;
   grid-row-end: 9;

   display: grid;
   grid-template-columns: repeat(1, 65px);
   grid-template-rows: repeat(4, 65px);
   grid-gap: 20px;
}
</style>
