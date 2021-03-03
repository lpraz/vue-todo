<template>
  <div>
    <li>{{text}}</li>
  </div>
</template>

<script>
export default 
{
    name: "TodoItem",
    props: ["text"]
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>