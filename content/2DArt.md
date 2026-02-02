---
title: 2D Art
date: 2021-12-18T11:10:36+08:00
draft: false
language: en
description: Tailwind Typography @tailwindcss/typography & Prose
---
<script src="https://cdn.tailwindcss.com"></script>
<head>
  <div class="not-prose relative h-[1600px] w-screen z-0" style="margin-left: calc(-50vw + 50%);">
    <div> <!--section 1-->
      <div id="pic1" class="kite top-0 right-[250px] absolute"></div>
      <div id="pic2" class="kite top-[200px] right-[630px] absolute"></div>
    </div>
    <div> <!--section 2-->
      <div id="pic3" class="kite top-[400px] left-[250px] absolute"></div>
      <div id="pic4" class="kite top-[600px] left-[630px] absolute"></div>
    </div>
    <div> <!--section 3-->
      <div id="pic5" class="kite top-[800px] right-[250px] absolute"></div>
      <div id="pic6" class="kite top-[1000px] right-[630px] absolute"></div>
    </div>
    <div> <!--section 3-->
      <div id="pic7" class="kite top-[1200px] left-[250px] absolute"></div>
    </div>
  </div>
</head>

<style>
  .kite {
    width: 670px;
    height: 350px;
    background-color: black;
    clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
  }
</style>