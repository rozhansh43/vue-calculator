<template>
  <div>
    <div class="buttons" >
      <button  @click="$emit('myfunction')">
        {{ x }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['x']
}
</script>