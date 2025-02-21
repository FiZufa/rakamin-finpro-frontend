<template>
    <footer class="footer">
      <div class="footer-container">
        <div class="footer-content">
          <p>&copy; 2025 Airbnb. All rights reserved.</p>
          <div class="footer-links">
            <a href="/about">About Us</a>
            <a href="/contact">Contact</a>
            <a href="/privacy">Privacy Policy</a>
          </div>
        </div>
      </div>
    </footer>
  </template>
  
  <script>
  export default {
    name: 'Footer',
  }
  </script>
  
  <style scoped>
  .footer {
    background-color: #fff;
    color: #000;
    padding: 20px 0; 
    text-align: center;
    font-size: 14px;
    border-top: #ccc solid 1px;
  }
  
  .footer-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
  }
  
  .footer-content {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  .footer-links {
    margin-top: 10px;
  }
  
  .footer-links a {
    color: #000;
    margin: 0 15px;
    text-decoration: none;
  }
  
  .footer-links a:hover {
    text-decoration: underline;
  }
  </style>
  