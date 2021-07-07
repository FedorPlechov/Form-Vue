<template>
  <the-form></the-form>
</template>

<script>
import TheForm from '@/components/form/TheForm'

export default {
  name: 'App',
  components: {
    TheForm
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Noto Sans KR', sans-serif;
}
.button {
  margin-top: 2rem;
  height: 2.5rem;
  background: rgba(127, 255, 212, 0.62);
  color: rgba(21, 90, 67, 0.91);
  font-size: 1.1rem;
  border-color: bisque;
  border-radius: 10px;
}
.button:hover,
.button:active {
  color: aliceblue;
  background: #39c467;
}

</style>
