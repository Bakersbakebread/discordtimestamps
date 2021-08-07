<template>
<div id="snackbar">👍 Copied to clipboard</div>
</template>

<script>
export default {
}
</script>

<style>
/* The snackbar - position it at the bottom and in the middle of the screen */
#snackbar {
  font-weight: 800;
  opacity: 0;
  /* visibility: hidden;  */
  width: 100%;
  background-color: #57F287; 
  color: #202225; 
  text-align: center; 
  padding: 16px; 
  position: fixed; 
  z-index: 1;
  left: 0;
  bottom: 0; 
  border: solid 1px #202225;
  transition: all 0.5s;
}

/* Show the snackbar when clicking on a button (class added with JavaScript) */
#snackbar.show {
  /* visibility: visible; Show the snackbar */
  opacity: 1;
}
</style>