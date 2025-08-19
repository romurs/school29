<script setup lang="ts">
defineProps({
  text: String,
})
</script>

<template>
  <div class="footer_text">
    <slot name="icon">
      <div class="icon"></div>
    </slot>
    <p>{{text}}</p>
  </div>
</template>

<style scoped lang="scss">
.footer_text{
  display: flex;
  align-items: center;
}

p{
  margin: 0.2rem;
  font-weight: 500;
  color: #fff;
}

.icon{
  width: 13px;
  height: 13px;
}
</style>