<template>
  <div class="card position-relative bg-light" :class="{'mt-4' : customClass , 'mb-4' : !customClass }">
    <div class="card-body pt-4" :class="{'bg-white' : customClass}">
      <slot name="title"></slot>
      <slot name="inputData"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "slotCard",
  props: ['customClass']
};
</script>

<style scoped></style>
