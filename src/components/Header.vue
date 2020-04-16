<template>
<div>
  <b-nav>
    <b-nav-item disabled><b>Fancy Quize App</b></b-nav-item>
    <b-nav-item disabled>Counter: {{ numCorrect }}/{{ numTotal }}</b-nav-item>

  </b-nav>
</div>
    <!-- <h3>Header</h3> -->
</template>

<script>
export default {
  props: [
    'numTotal',
    'numCorrect'
  ]
}
</script>