<script setup lang="ts">

</script>

<template>
    <!-- <div class="overlay"> -->
        <slot name="header" />
        <a href="" class="btn btn-noborder btn-icon"><i class="lpi-close"></i><span>Close</span></a>
        <slot name="body" />
        <slot name="footer" />
    <!-- </div> -->
</template>

<style>
  .modal-wrapper {
    width: '50%'
  }
</style>