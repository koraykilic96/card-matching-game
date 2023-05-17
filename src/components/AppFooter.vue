<template>
    <footer>
      <div class="footer-content">
        <p>&copy; {{ currentYear }} Koray Kılıç. Tüm hakları saklıdır.</p>
      </div>
    </footer>
  </template>
  
  <script>
  export default {
    name: 'AppFooter',
    data() {
      return {
        currentYear: new Date().getFullYear(),
      };
    },
  };
  </script>
  
  <style scoped>
  footer {
    background-color: #f2f2f2;
    padding: 20px;
    margin-top: 20px;
    position: fixed;
    bottom: 0;
    width: 97%;
  }
  
  .footer-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
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
  