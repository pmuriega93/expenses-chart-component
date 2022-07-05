<template>
  <ExpensesChart />
</template>

<script>
import ExpensesChart from './components/ExpensesChart.vue';

export default {
  components: {
    ExpensesChart
  },

  
}

</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;700&display=swap');

:root {
  --primary-soft-red:  hsl(10, 79%, 65%);
  --primary-cyan: hsl(186, 34%, 60%);

  --neutral-dark-brown: hsl(25, 47%, 15%);
  --neutral-medium-brown: hsl(28, 10%, 53%);
  --neutral-cream: hsl(27, 66%, 92%);
  --neutral-very-pale-orange: hsl(33, 100%, 98%);
}

* {
  position: relative;
}

*,
*::after,
*::before {
    margin: 0;
    padding: 0;
    box-sizing: inherit;
}

html {
    font-size: 62.5%;
    font-family: 'DM Sans', sans-serif;
}

body {
    box-sizing: border-box;
    padding: 3rem;
    background-color: var(--neutral-cream);
    font-size: 1.8rem;
}
</style>
