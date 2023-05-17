<template>
    <header>
      <h1>{{ title }}</h1>
    </header>
  </template>
  
  <script>
  export default {
    name: 'AppHeader',
    data() {
      return {
        title: 'Kart Eşleştirme Oyunu',
      };
    },
  };
  </script>
  
  <style scoped>
  header {
    background-color: #f2f2f2;
    padding: 20px;
  }
  
  h1 {
    margin: 0;
  }
  
  nav ul {
    list-style-type: none;
    padding: 0;
  }
  
  nav ul li {
    display: inline-block;
    margin-right: 10px;
  }
  
  nav ul li:last-child {
    margin-right: 0;
  }
  
  a {
    text-decoration: none;
    color: #333;
  }
  
  </style>
  