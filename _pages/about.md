---
permalink: /
excerpt: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---
<style>
    .bio-paragraph{
     position: relative;
     width: 320px;
     float: left;
     padding: 5px;
    } 
  
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
        font-size:52px;
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



<div style="text-align:left; float: left;">
  <div class="bio-paragraph">
    <p>Currently a rising second year Computer Science MS student at Georgia Tech, specialized in Machine Learning.Interests include NLP, Machine Learning, and how we can create        better-structued knolwege graphs to help us learn, teach, and recreate. I am really excited about how NLP can push both our limits of cultural exchange and our limits of        understanding of this complex world.<br>
       Before stuying computer science, I also stuidied Architectural Design in Columbia University and worked as an architectural designer in one of the top architectural firms        in the world Kohn Pedersen Fox designing a supertall office tower. My design background gives me a new way of looking the world, and makes me wonder how AI agent can learn      to be creative in the design process.<br>
       In my life, I enjoy swimming, travelling, and exploring different cultures. Feel free to write me at ymou32@gatech.edu and thanks for stopping by!</p>
  </div>
</div>



<div style="text-align:center; float: left;">
  
  <a href='https://yingjun-mou.github.io/projects/'>
    <div class="content_img">
      <img src="../images/Icon_coding.png"/>
      <div style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);">
        <h1 class="icontext">CODING</h1>      
      </div>
    </div>
  </a>  
  
  <a href='https://yingjun-mou.github.io/publications/'>
    <div class="content_img">
      <img src="../images/Icon_research_red.jpg"/>
      <div style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);">
        <h1 class="icontext">RESEARCH</h1>      
      </div>
    </div>
  </a> 

</div>

<div style="text-align:center; float: left;">
  
  <a href='https://yingjun-mou.github.io/projects/#start_Design'>
    <div class="content_img">
      <img src="../images/Icon_design_red.jpg"/>
      <div style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);">
        <h1 class="icontext">DESIGN</h1>      
      </div>
    </div>  
  </a> 

  <a href='https://yingjun-mou.github.io/travel/'>
    <div class="content_img">
      <img src="../images/Icon_travel_red.jpg"/>
      <div style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);">
        <h1 class="icontext">TRAVEL</h1>      
      </div>
    </div>
  </a> 

</div>
