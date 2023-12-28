<script>
export default {
   name: "ButtonNumber",
};
</script>

<template>
   <button class="btn__number" @click="$emit('btn-function')">
      <slot></slot>
   </button>
</template>

<style scoped>
.btn__number {
    border-radius: 16px;
    background-color: #2e2f38;
    font-size: 22px;
 
    color: #fff;
    border: none;
 }
 .btn__number:hover {
    background-color: #464856;
    transform: scale(1.03);
    transition: 0.1s;
 }
</style>
