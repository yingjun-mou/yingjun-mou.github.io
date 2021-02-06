---
permalink: /
excerpt: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---
<style>
    .content_img{
     position: relative;
     width: 320px;
     float: left;
     padding: 5px;
    } 

    .content_img .icontext{
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        color: #2f4455;
        margin: 5px;
        font-size:54px;
        font-family: sans-serif;
        opacity: 1.0;
        <!---visibility: hidden;--->
        -webkit-transition: visibility 0s, opacity 0.5s linear; 
        transition: visibility 0s, opacity 0.5s linear;
    }
    
    .content_img:hover {
        cursor: pointer;
    }
    
    .content_img:hover .icontext{
        padding: 8px;
        visibility: visible;
        opacity: 0.7;
        color: gray;
        background-color: yellow;
    } 
</style>


<div style="text-align:center; float: left;">
  
  <div class="content_img">
    <a href="https://yingjun-mou.github.io/projects/"><img src="../images/Icon_coding.png"/></a>
    <div style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);">
      <h1 class="icontext">CODING</h1>      
    </div>
  </div>  
  
  <div class="content_img">
    <a href="https://yingjun-mou.github.io/publications/"><img src="../images/Icon_research_red.jpg"/></a>
    <div style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);">
      <h1 class="icontext">RESEARCH</h1>      
    </div>
  </div>

</div>

<div style="text-align:center; float: left;">
  
  <div class="content_img">
    <a href="https://yingjun-mou.github.io/projects/#start_Design"><img src="../images/Icon_design_red.jpg"/></a>
    <div style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);">
      <h1 class="icontext">DESIGN</h1>      
    </div>
  </div>  
  
  <div class="content_img">
    <a href="https://yingjun-mou.github.io/travel/"><img src="../images/Icon_travel_red.jpg"/></a>
    <div style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);">
      <h1 class="icontext">TRAVEL</h1>      
    </div>
  </div>

</div>
