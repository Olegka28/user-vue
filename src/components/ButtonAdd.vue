<template>
  <button type="button" class="btn btn-primary" @click="showModalClick">
    Add new user
  </button>
</template>

<script>
export default {
  name: 'ButtonAdd',
  props: ['showModalClick'],
};
</script>

<style scope></style>
