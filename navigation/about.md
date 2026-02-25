---
layout: post
title: About
permalink: /about/
comments: true
---

## As a conversation Starter

I have visited many places during my lifetime.
<comment>
Flags are made using Wikipedia images
</comment>

<style>
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
        gap: 10px;
    }

    .grid-item {
        text-align: center;
    }

    .grid-item img {
        width: 100%;
        height: 100px;
        object-fit: contain;
    }

    /* Caption color changed to black */
    .grid-item p {
        margin: 5px 0;
        color: #000;
    }

    .image-gallery {
        display: flex;
        flex-wrap: nowrap;
        overflow-x: auto;
        gap: 10px;
    }

    .image-gallery img {
        max-height: 150px;
        object-fit: cover;
        border-radius: 5px;
    }

    /* Likes grid */
    .likes-grid {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
        gap: 15px;
        margin-top: 10px;

        border: 2px solid #ccc;
        border-radius: 12px;
        padding: 15px;
        background-color: #fafafa;
    }

    .likes-item {
        text-align: center;
    }

    .likes-item img {
        width: 100%;
        height: 150px;
        object-fit: cover;
        border-radius: 8px;
    }

    /* Caption color changed to black */
    .likes-item p {
        margin-top: 6px;
        font-size: 0.9rem;
        color: #000;
    }
</style>

<div class="grid-container" id="grid_container"></div>

<script>
    var container = document.getElementById("grid_container");

    var http_source = "https://upload.wikimedia.org/wikipedia/commons/";
    var living_in_the_world = [
        {"flag": "4/41/Flag_of_India.svg", "greeting": "Hey", "description": "India - 5 times"},
        {"flag": "d/d9/Flag_of_Canada_%28Pantone%29.svg", "greeting": "Hi", "description": "Canada - 5 times"},
        {"flag": "b/be/Flag_of_England.svg", "greeting": "Alright mate", "description": "England - 2 times"},
        {"flag": "e/ef/Flag_of_Hawaii.svg", "greeting": "Aloha", "description": "Hawaii - 4 times"}
    ];

    for (const location of living_in_the_world) {
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";

        var img = document.createElement("img");
        img.src = http_source + location.flag;
        img.alt = location.description + " Flag";

        var description = document.createElement("p");
        description.textContent = location.description;

        var greeting = document.createElement("p");
        greeting.textContent = location.greeting;

        gridItem.appendChild(img);
        gridItem.appendChild(description);
        gridItem.appendChild(greeting);

        container.appendChild(gridItem);
    }
</script>

.likes-grid .likes-item p {
    color: #000 !important;
    opacity: 1 !important;
}

### Journey through Life

My life so far:

- 🏫 Went to Morning Creek elementary school from K–2  
- 🚙 Moved to 4S Ranch and went to Stone Ranch elementary school from 3–5  
- 🎓 Graduated from Stone Ranch elementary school and went to Oak Valley middle school  
- 🏫 Spent 6th, 7th, and 8th grade at Oak Valley Middle School  
- 🎓 Graduated from Oak Valley middle school and went to Del Norte High School  

### Culture, Family, and Fun
- There are 4 people in my family. We are all from India, but my brother and I were born here.

<div class="image-gallery">
    <img src="{{site.baseurl}}/images/about/IMG_2832.jpg" alt="Family photo">
    <img src="{{site.baseurl}}/images/about/fampic.jpg" alt="Family photo2">
</div>

### Things I like:
<div class="likes-grid">
    <div class="likes-item">
        <img src="https://upload.wikimedia.org/wikipedia/commons/6/60/Sushi_platter.jpg" alt="Sushi">
        <p style="color:#000 !important; opacity:1 !important;">Sushi</p>
    </div>

    <div class="likes-item">
        <img src="https://upload.wikimedia.org/wikipedia/commons/4/42/Polistil_Video_Games_V.G.2_%281%29.jpg" alt="Video Games">
        <p style="color:#000 !important; opacity:1 !important;">Video Games</p>
    </div>

    <div class="likes-item">
        <img src="https://upload.wikimedia.org/wikipedia/commons/3/3e/Tennis_Racket_and_Balls.jpg" alt="Tennis">
        <p style="color:#000 !important; opacity:1 !important;">Tennis</p>
    </div>

    <div class="likes-item">
        <img src="https://upload.wikimedia.org/wikipedia/commons/0/0b/RedDot_Burger.jpg" alt="Burger">
        <p style="color:#000 !important; opacity:1 !important;">Burgers</p>
    </div>
</div>



