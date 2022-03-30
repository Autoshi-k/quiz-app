<template>
  <div class="header"> 
    <h3>Correct answres: <span>1/4</span></h3>
    <button class="btn-pink">Reset Count</button>
  </div>
</template>

<style scoped>
  .header {
    width: 100vw;
    min-height: 3rem;
    display: flex;
    align-items: center;
    border-bottom: 2px solid palevioletred;
  }
  h3 {
    color: rgb(218, 60, 152);
    width: fit-content;
    display: inline-block;
    padding: 0 2rem;
    font-weight: 600;
  }
  .header button {
    height: 2rem;
    padding: 0 1rem;
    width: fit-content;
  }
</style>