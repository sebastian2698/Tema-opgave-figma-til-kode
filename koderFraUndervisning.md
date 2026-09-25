<!------------ scroll-snap ----------------*
<!-- **

/****** html'en *****/
<section>
  <div class="scroll-container">
    <div class="item"><span>Item 1</span></div>
    <div class="item"><span>Item 2</span></div>
    <div class="item"><span>Item 3</span></div>
    <div class="item"><span>Item 4</span></div>
    <div class="item"><span>Item 5</span></div>
    <div class="item"><span>Item 6</span></div>
    <div class="item"><span>Item 7</span></div>
    <div class="item"><span>Item 8</span></div>
    <div class="item"><span>Item 9</span></div>
  </div>
</section> -->

/**\*\*** css'en **\***/
html {
padding: 1rem 0;
}
.scroll-container {
gap: 1rem;
padding-block: 1rem;
}
.item {
background: #5000ca;
color: #fff;
padding: 1.5rem 1rem;
border-radius: 0.5rem;
}

.scroll-container {
padding-inline: 2rem;
scroll-padding-inline: 2rem;
overflow-inline: auto;
gap: 1rem;
display: flex;
scroll-snap-type: inline mandatory;

}
.item {
flex: 0 0 300px;
background-color: #4caf98;
scroll-snap-align: start;
scroll-snap-stop: always;

}

<!------------ scroll- knapper ----------------*
/****** js'en *****/
const scroller = document.querySelector("#scroller");

scroller.addEventListener("command", (e) => {
  if (e.command === "--scroll") {
    scroller.scrollBy({
      left: scroller.offsetWidth * e.source.value
    })
  }
});

function disableButtons() {
  const maxScroll = scroller.scrollWidth - scroller.offsetWidth;

  prev.disabled = scroller.scrollLeft <= 0;
  next.disabled = scroller.scrollLeft >= maxScroll - 1;
}

scroller.addEventListener("scroll", disableButtons);

disableButtons()


/****** html'en *****/
<button
  value="-.9"
  command="--scroll"
  commandfor="scroller">
  Prev
</button>




/***************** donot chart *************/
´´html

    <section>
  <h1>SVG-playground</h1>
  <article data-value="75">
    <svg viewBox="0 0 100 100">
      <circle class="track" />
        <circle class="progress" pathLength="100"/>
         <circle class="marker"/>
   
     </svg>
  </article>
</section>




section {
  --range: 300px, 500px;
  --p: progress(100cqw, var(--range));
  padding: calc(1rem + var(--p) * 1rem);
}

h1 {
  font-size: 3.25rem;
  font-size: calc(1.25rem + var(--p) * 2rem);
  font-weight: round(700 - var(--p) * 300, 50);
}

.lede {
  font-size: 1.5rem;
}

p {
  font-size: 1.25rem;
}












/******************* Doughnut chart *************/

body {
  display: grid;
  place-items: center;
  min-height: 400px;
  &:has(:checked) {
    background: repeating-conic-gradient(#eee 0 25%, #fff 0 50%) 0 / 40px 40px;
  }
}
div {
  width: 200px;
  height: 200px;
}

label {
  visibility: visible;
}

div {
  border: 10px solid #0000;
  background:
    conic-gradient(#fff) padding-box,
    conic-gradient(red 25%, blue 0) border-box;
  border-radius: 999px;
  @supports (background-clip: border-area) {
    background: conic-gradient(red 25%, blue 0) border-area;
  }
}

https: //www.joshwcomeau.com/svg/friendly-introduction-to-svg/
  <svg viewBox= "0 0 100 100" > <circle cx= "50" cy= "50" r= "50" / > </svg>;







  /********** ny donot ***********/  
   /**********  Mangler noget kode for at virker. Er skrevet ned fra undervisningen *******/



  section {
  display: grid;
  place-items: center;
  article {
    width: min(100%, 400px);
  }
}




article {
  --value: attr(data-value type(<number>));
  --value-sting();
    --value-sting-procent: ();
  
  dispay: grid;
  grid: "stack";
  place-itaems: center; 
  
  
  
  &::after {
    content: var (--value-sting) "%";
  }
}

svg {
  outline: 1px dashed var(--gray-400);
  rotate: -90deg;
  overflow: visible;
}
.track {
  --stroke-width: 4px;
  cx: 50px;
  cy: 50px;
  r: calc(50px - var(--stroke-width) / 2);

  fill: none;
   stroke: red;
  stroke-width: var(--stroke-width); 
}

.progress {
  stroke: #000;
  stroke-dasharray: 100;
    stroke-dashoffset:cal  (var(--value));
    stroke-line-cap: round;
}




.marker {
  r: 4;
  stroke: red;
  offset-path: circle(48px at 50px 50px);
  offset-disteance: ()
}

https://demos.cssxs.dev/topic/3sem/crafting-ui/tegn-med-kode/svg-og-doughnut-chart
https://demos.cssxs.dev/3sem/crafting-ui/data/svg-playground
