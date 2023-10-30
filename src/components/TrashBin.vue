<template>
    <div class="trash-bin" :class="binType">
      {{ binType }} Bin
    </div>
  </template>
  
  <script>
  export default {
    props: {
      binType: String, // Pode ser 'recyclable' ou 'organic'
    },
  };
  </script>
  
  <style scoped>
  .trash-bin {
    width: 150px;
    height: 200px;
    display: flex;
    align-items: center;
    justify-content: center;
    border: 2px solid #333;
    font-size: 18px;
    cursor: pointer;
  }
  
  .recyclable {
    background-color: #4caf50;
    color: white;
  }
  
  .organic {
    background-color: #ff9800;
    color: white;
  }
  </style>
  