<template>
  <div class="home">
    <horizontal-chart/>
  </div>
</template>

<script>
// @ is an alias to /src
import HorizontalChart from '../components/HorizontalChart.vue'

export default {
  name: 'Home',
  components: {
    HorizontalChart
  }
}
</script>
