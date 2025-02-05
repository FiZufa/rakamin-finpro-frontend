<template>
    <div class="overlay">
      <div class="predict-box">
        <p>The predicted price is <span class="price">€{{ formattedPrice }}</span></p>
        <p>Rent the room with this predicted price?</p>
        <div class="button-group">
            <button class="rent-now-btn">Yes, rent now</button>
          <button class="set-price-btn">No, set my own price</button>
          <button class="cancel-btn" @click="$emit('close')">Cancel</button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      predicted_price: Number
    },
    computed: {
    formattedPrice() {
      return this.predicted_price ? this.predicted_price.toFixed(2) : "0.00";
    }
  }
  };
  </script>
  
  <style>
  /* Centered popup with overlay */
  .overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  /* Styled pop-up box */
  .predict-box {
    background: white;
    padding: 20px;
    border-radius: 12px;
    width: 350px;
    text-align: center;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
  }

  .price {
    color: #FF385C;
    font-weight: bold;
    font-size: 20px;
  }
  
  /* Button styling */
  .button-group {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-top: 15px;
  }
  
  button {
    padding: 10px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.3s;
  }
  
  .set-price-btn {
    background: #FFCC00;
  }
  
  .rent-now-btn {
    background: #FF385C;
    color: white;
  }
  
  .cancel-btn {
    background: #ccc;
  }
  
  button:hover {
    opacity: 0.8;
  }
  </style>
  