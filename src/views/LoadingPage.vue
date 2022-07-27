<template>
  <div class="main">
    <h1>LOADING</h1>
    <ul>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "LoadingPage"
}


</script>

<style scoped>
html {
  min-height: 100%;
  background: -webkit-radial-gradient(center, ellipse cover,  rgba(41,42,45,1) 0%,rgba(0,0,0,1) 100%); /* Chrome10+,Safari5.1+ */
  background: -o-radial-gradient(center, ellipse cover,  rgba(41,42,45,1) 0%,rgba(0,0,0,1) 100%); /* Opera 12+ */
  background: -ms-radial-gradient(center, ellipse cover,  rgba(41,42,45,1) 0%,rgba(0,0,0,1) 100%); /* IE10+ */
  background: radial-gradient(ellipse at center,  rgba(41,42,45,1) 0%,rgba(0,0,0,1) 100%); /* W3C */
}

h1{

}
ul {
  margin: auto;
  height: 10px;
  width: 500px;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  list-style: none;
  padding: 0;
}

li {
  display: block;
  float: left;
  width: 90px;
  height: 10px;
  margin-right: 10px;
}

li:nth-child(-n+3) {
  background: rgba(255,255,255,0.9);
  box-shadow: inset 0px 0px 10px 2px rgba(117,182,255,0.5),
  0px 0px 20px rgba(117,182,214,0.5);
}

li:nth-child(n+4) {
  box-shadow: inset 0px 0px 10px 1px rgba(117,182,255,0.4),
  0px 0px 20px rgba(117,182,255,0.1);
}

li:nth-child(3) {
  -webkit-animation: pulse 1s alternate infinite;
  -moz-animation: pulse 1s alternate infinite;
}

@-webkit-keyframes pulse {
  0% {
    background: rgba(255,255,255,1);
    box-shadow: inset 0px 0px 10px 2px rgba(117,182,255,0.5),
    0px 0px 40px 2px rgba(105,135,255,1);
  }
  100% {
    background: rgba(255,255,255,0);
    box-shadow: inset 0px 0px 10px 2px rgba(117,182,255,0.5),
    0px 0px 30px 2px rgba(105,135,255,0.3);
  }
}

@-moz-keyframes pulse {
  0% {
    background: rgba(255,255,255,1);
    box-shadow: inset 0px 0px 10px 2px rgba(117,182,255,0.5),
    0px 0px 40px 2px rgba(105,135,255,1);
  }
  100% {
    background: rgba(255,255,255,0);
    box-shadow: inset 0px 0px 10px 2px rgba(117,182,255,0.5),
    0px 0px 30px 2px rgba(105,135,255,0.3);
  }
}
</style>