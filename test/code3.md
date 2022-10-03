---
sort : 14
---

# Code 3


5555 .

<style>
#container {
  width: 400px;
  height: 400px;
  position: relative;
  background: yellow;
}
#animate {
  width: 50px;
  height: 50px;
  position: absolute;
  background-color: red;
}
</style>


<p><button onclick="myMove()">Click Me</button></p> 

<div id ="container">
  <div id ="animate"></div>
</div>


<script>
function myMove() {
  let id = null;
  const elem = document.getElementById("animate");   
  let pos = 0;
  clearInterval(id);
  id = setInterval(frame, 5);
  function frame() {
    if (pos == 350) {
      clearInterval(id);
    } else {
      pos++; 
      elem.style.top = pos + "px"; 
      elem.style.left = pos + "px"; 
    }
  }
}
</script>





<br><br><br><br><br><br><br><br><br>




<link rel="stylesheet" href="../assets/css/My CSS/test.css">


<h1>Custom Range Slider</h1>
<p>Drag the slider to display the current value.</p>

<div class="slidecontainer">
  <input type="range" min="1" max="100" value="50" class="slider" id="myRange">
  <p>Value: <span id="demo"></span></p>
</div>


<!-- <script type="text/javascript" src="../assets/js/My JS/test.js"></script> -->


<script>
var slider = document.getElementById("myRange");
var output = document.getElementById("demo");
output.innerHTML = slider.value; 

slider.oninput = function() {
  output.innerHTML = this.value;
} 
</script>