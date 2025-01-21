<template>
    <span class="error">{{ message }}</span>
  </template>
  
  <script>
  export default {
    name: 'ErrorDisplay',
    props: {
      message: {
        type: String,
        required: true,
      },
    },
  };
  </script>
  
  <style scoped>
  .error {
    color: red;
    font-size: 12px;
    margin-top: 5px;
    display: block;
  }
  </style>
  