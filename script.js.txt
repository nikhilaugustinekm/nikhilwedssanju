// =============================
// Wedding Countdown
// =============================

const weddingDate = new Date("November 15, 2026 00:00:00").getTime();

const days = document.getElementById("days");
const hours = document.getElementById("hours");
const minutes = document.getElementById("minutes");
const seconds = document.getElementById("seconds");

function updateCountdown(){

    const now = new Date().getTime();
    const distance = weddingDate - now;

    if(distance <= 0){

        days.innerHTML="000";
        hours.innerHTML="00";
        minutes.innerHTML="00";
        seconds.innerHTML="00";

        startFireworks();

        return;
    }

    const d = Math.floor(distance / (1000*60*60*24));
    const h = Math.floor((distance % (1000*60*60*24))/(1000*60*60));
    const m = Math.floor((distance % (1000*60*60))/(1000*60));
    const s = Math.floor((distance % (1000*60))/1000);

    days.innerHTML=d;
    hours.innerHTML=h.toString().padStart(2,"0");
    minutes.innerHTML=m.toString().padStart(2,"0");
    seconds.innerHTML=s.toString().padStart(2,"0");

}

updateCountdown();
setInterval(updateCountdown,1000);


// =============================
// Loader
// =============================

window.addEventListener("load",()=>{

    setTimeout(()=>{

        const loader=document.getElementById("loader");

        loader.style.opacity="0";

        loader.style.pointerEvents="none";

        setTimeout(()=>{

            loader.remove();

        },800);

    },1200);

});


// =============================
// Scroll To Top
// =============================

const topBtn=document.getElementById("top");

window.addEventListener("scroll",()=>{

    if(window.scrollY>400){

        topBtn.style.opacity=1;

    }

    else{

        topBtn.style.opacity=0;

    }

});

topBtn.onclick=()=>{

    window.scrollTo({

        top:0,

        behavior:"smooth"

    });

};


// =============================
// Music Button
// =============================

const song=document.getElementById("song");

const music=document.getElementById("music");

let playing=false;

music.onclick=()=>{

    if(!playing){

        song.play();

        playing=true;

        music.innerHTML='<i class="fa-solid fa-pause"></i>';

    }

    else{

        song.pause();

        playing=false;

        music.innerHTML='<i class="fa-solid fa-music"></i>';

    }

};


// =============================
// Fade in Sections
// =============================

const observer=new IntersectionObserver(entries=>{

entries.forEach(entry=>{

if(entry.isIntersecting){

entry.target.animate([

{

opacity:0,

transform:"translateY(60px)"

},

{

opacity:1,

transform:"translateY(0)"

}

],{

duration:1000,

fill:"forwards"

});

}

});

},{threshold:.15});

document.querySelectorAll("section").forEach(sec=>{

observer.observe(sec);

});


// =============================
// Gallery Click Effect
// =============================

document.querySelectorAll(".grid img").forEach(img=>{

img.onclick=()=>{

const overlay=document.createElement("div");

overlay.style.position="fixed";
overlay.style.top="0";
overlay.style.left="0";
overlay.style.width="100%";
overlay.style.height="100%";
overlay.style.background="rgba(0,0,0,.9)";
overlay.style.display="flex";
overlay.style.justifyContent="center";
overlay.style.alignItems="center";
overlay.style.zIndex="99999";
overlay.style.cursor="zoom-out";

const image=document.createElement("img");

image.src=img.src;
image.style.maxWidth="90%";
image.style.maxHeight="90%";
image.style.borderRadius="20px";
image.style.boxShadow="0 20px 50px rgba(0,0,0,.5)";

overlay.appendChild(image);

overlay.onclick=()=>overlay.remove();

document.body.appendChild(overlay);

};

});


// =============================
// Fireworks
// =============================

function startFireworks(){

const canvas=document.getElementById("fireworks");

const ctx=canvas.getContext("2d");

canvas.width=window.innerWidth;
canvas.height=window.innerHeight;

const particles=[];

function Particle(x,y,color){

this.x=x;
this.y=y;

this.radius=Math.random()*3+2;

this.dx=(Math.random()-.5)*10;
this.dy=(Math.random()-.5)*10;

this.alpha=1;

this.color=color;

}

Particle.prototype.draw=function(){

ctx.globalAlpha=this.alpha;

ctx.beginPath();

ctx.arc(this.x,this.y,this.radius,0,Math.PI*2);

ctx.fillStyle=this.color;

ctx.fill();

}

Particle.prototype.update=function(){

this.x+=this.dx;
this.y+=this.dy;

this.dy+=0.05;

this.alpha-=0.01;

this.draw();

}

setInterval(()=>{

const x=Math.random()*canvas.width;

const y=Math.random()*canvas.height/2;

const colors=["#FFD700","#FF69B4","#87CEFA","#FFFFFF","#FF4500"];

for(let i=0;i<80;i++){

particles.push(new Particle(x,y,colors[Math.floor(Math.random()*colors.length)]));

}

},600);

function animate(){

requestAnimationFrame(animate);

ctx.clearRect(0,0,canvas.width,canvas.height);

for(let i=particles.length-1;i>=0;i--){

particles[i].update();

if(particles[i].alpha<=0){

particles.splice(i,1);

}

}

}

animate();

}


// =============================
// Mouse Glow
// =============================

const glow=document.createElement("div");

glow.style.position="fixed";
glow.style.width="250px";
glow.style.height="250px";
glow.style.borderRadius="50%";
glow.style.pointerEvents="none";
glow.style.background="radial-gradient(circle,rgba(255,215,120,.18),transparent 70%)";
glow.style.transform="translate(-50%,-50%)";
glow.style.zIndex="0";

document.body.appendChild(glow);

window.addEventListener("mousemove",(e)=>{

glow.style.left=e.clientX+"px";
glow.style.top=e.clientY+"px";

});


// =============================
// Parallax
// =============================

window.addEventListener("scroll",()=>{

const bg=document.querySelector(".background-image");

bg.style.transform=`scale(1.15) translateY(${window.scrollY*.15}px)`;

});


// =============================
// End
// =============================