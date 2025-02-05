<template>
    <div class="overlay">
      <div class="predict-box">
        <p>The predicted price is <span class="price">{{ predicted_price }}</span></p>
        <p>Rent the room with this predicted price?</p>
        <div class="button-group">
          <button class="set-price-btn">No, set my own price</button>
          <button class="rent-now-btn">Yes, rent now</button>
          <button class="cancel-btn">Cancel</button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      predicted_price: Number // Accept predicted price as a prop
    }
  };
  </script>
  
  <style>
  /* Background overlay to darken the screen */
  .overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5); /* Semi-transparent black */
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  /* Centered pop-up box */
  .predict-box {
    background: white;
    padding: 20px;
    border-radius: 12px;
    width: 350px;
    text-align: center;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
    animation: fadeIn 0.3s ease-in-out;
  }
  
  /* Predicted price styling */
  .price {
    font-weight: bold;
    color: #FF385C;
    font-size: 1.5rem;
  }
  
  /* Button styles */
  .button-group {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-top: 15px;
  }
  
  button {
    padding: 10px 15px;
    border: none;
    border-radius: 8px;
    font-size: 1rem;
    cursor: pointer;
    transition: all 0.3s;
  }
  
  .set-price-btn {
    background: #FFCC00;
    color: black;
  }
  
  .rent-now-btn {
    background: #FF385C;
    color: white;
  }
  
  .cancel-btn {
    background: #ccc;
    color: black;
  }
  
  button:hover {
    opacity: 0.8;
  }
  
  /* Fade-in animation */
  @keyframes fadeIn {
    from {
      opacity: 0;
      transform: translateY(-20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  </style>
  