<script>
export default {
   name: "ButtonCommand",
};
</script>

<template>
   <button class="btn__command" @click="$emit('btn-function')">
      <slot></slot>
   </button>
</template>

<style scoped>
.btn__command {
   border-radius: 16px;
   background-color: #4b5efc;
   font-size: 22px;

   color: #fff;
   border: none;
}
.btn__command:hover {
   background-color: #6473fe;
   transform: scale(1.03);
   transition: 0.1s;
}
</style>
