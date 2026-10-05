# Refleksion – Figma til kode

**Gruppemedlemmer:** Julie Høyen & Sebastian Blicher.

# Refleksion

## Fallbacks og progressive enhancement

Vi skulle have arbejdet mere med fallbacks og progressive enhancement, da meget af vores CSS er bygget op af relativt mange nye metoder fra undervisningen. Det betyder, at vi har fundet ud af, at ikke alle vores løsninger virker i alle browsere.

### Hvorfor passer teknikken til problemet?

Det har vi valgt, fordi det kan have betydning for brugere, der benytter andre browsere som Firefox eller Safari, da ikke alle koder eller animationer er understøttet af browseren, så de også kan få en lige så god brugeroplevelse som dem, der benytter Chrome.

### Hvad testede I, og hvad viste testen?

Vi forsøgte at bruge fallback til donut-chartet, hvor animationerne understøttes på Chrome version 155.0.8059.26, men ikke Firefox 157.0.

For at løse problemet brugte vi en kombination af Developer Tools og AI til at finde frem til, hvilke koder der ikke understøttes. Her fandt vi frem til, at koden `animation-timeline` ikke er kompatibel med Firefox.

Eksempel fra `/src/components/Experience.astro`=

```CSS
.donut_section > figure {
--value: attr(data-value type(<number>));
 --value-string: attr(data-value);
--scroll-progress: 0;
animation: donut-progress 3s both;
  }

@supports (animation-timeline: view()) {
    .donut_section > figure {
      animation: donut-progress linear both;
      animation-timeline: --experience-scroll;
      animation-range: entry 0% cover 40%;
    }
  }
```

Vi sparrede derefter med AI om, at vi kunne bruge `animation`, som virker i ældre browsere, og sige, at koden skal have `donut-progress 3s both`, hvilket vil sige, at animationen skal køre i 3 sekunder på begge elementer.

Derefter lavede vi en fallback omkring dette, hvilket godt kunne få cirklen til at køre rundt, men vi mangler stadig en helt konkret fallback-løsning til resten af animationerne.

### Hvad ændrede I, eller hvad mangler stadig?

Vi skal undersøge, hvorvidt det er muligt at lave en helt konkret fallback-løsning, som også gør det muligt at se stregerne følge med cirklen, så brugerne kan få en tilsvarende oplevelse som Chrome brugerere.

Ved at teste med fallback har vi også lært, at selvom nyere funktioner ikke er understøttet i alle browsere, behøver vi ikke kun at tilpasse vores kode med ældre metoder. Vi har også mulighed for at splitte funktionaliteten op og tilpasse de enkelte dele, så vi kan løse problemerne for flere brugere.

---

## Global og lokal CSS

Vi havde en forventning om, at vi ville starte med at lave en global CSS, som kunne definere bredden på siden og opsætte grids, fontstørrelser og gøre fontstørrelserne responsive.

Dermed havde vi også et ønske om at lave en overordnet regel for `.section-text`, som kunne ligge i den globale CSS. På den måde kunne vi undgå at skulle bruge scoped styling i samtlige Astro-komponenter, hvor den bliver brugt.

Det viste sig dog, at der opstod problemer med globale og lokale CSS-regler, der overlappede hinanden. Det gjorde det sværere at styre, hvilke regler der skulle gælde i de enkelte komponenter. Derfor endte vi med at bruge scoped styling i stedet.

---

## Data fra API’et

API’et har drillet en del for Julie, da hun ikke har arbejdet så meget med det før. Da hun først fandt ud af, hvordan det fungerede, var det dog forholdsvis nemt at tilføje data til de komponenter, der skulle gøre brug af API’et.

Donut-chartet har dog drillet en del, da det både skulle hente værdien fra API’et og vise den inde i cirklen. Samtidig skulle værdien afspejles i procent rundt langs kanten af chartet. Derudover skulle en SVG-animation følge den hvide streg rundt i kanten, i takt med at man scroller ned på siden.

---

## Responsivt design

Det havde også været en fordel at arbejde med det responsive design tidligere i processen, blandt andet ved hjælp af container queries. På den måde var mobilversionen ikke blevet en eftertanke, men havde været en del af udviklingen fra starten.

---

## Mange ændringer samtidig

Det havde nok også været en fordel at teste færre ting ad gangen, når der blev lavet rettelser. Når mange ting bliver ændret samtidig, kan det være svært at finde ud af, hvilken ændring der har skabt en fejl.

Næste gang vil det være en fordel at man ikke lavde for mange ændringer af ad gangen og teste løbende, så det bliver nemmere at fejlfinde og bevare overblikket.

---

## Ekstra detalje

Som lidt ekstra lir har vi lavet et favicon, som er en sammensætning af de to forbogstaver, som er i logoet (AE). Vi har sat dem sammen med de hvide og gule farver og samme skrifttype som logoet, så det giver et mere overordnet professionelt syn på siden. Også selvom det ikke var en del af opgaven.

---

# Benspænd

## Classes og nesting

Vi har villet bruge så få classes som muligt og arbejde mere med nesting. Hvis vi havde mere tid, ville vi have gennemgået hele vores opgave og set, om vi kunne ændre classes til nesting.

## API frem for hardcode

Vi har også arbejdet med at få tekst og billeder fra API'er frem for at hardcode dem. Dog har det været at hardcode for at lave HTML-strukturen og style på det først.

## Subgrid

Sebastian havde et ønske om at have benyttet subgrid lidt mere i koden frem for at have forskellige grids i classes. Det har skyldtes, at jeg enten ikke kunne få det til at virke, eller også har jeg bedømt ud fra Figma-designet, at det ikke gav mening at benytte subgrids.

Der er blandt andet blevet brugt subgrid for at få hero-billedet til at være inde i hero-artiklen og have `.hero-content`-teksten på venstre side.

Eksempel fra `src/components/Hero.astro` =

```CSS
.hero > article {
  grid-column: full;
  display: grid;
  grid-template-columns: subgrid;
}
```

---

# Tekniske krav

## `tokens.css`

Vi har også arbejdet mere med `tokens.css`, som giver en mere generel strømlining igennem hele siden. Fx får websiden den samme padding, som giver den samme bredde på alle sider.

---

## Container query

Vi har arbejdet med container query i donut-chartet, så de ændrer sig fra at være i `grid-template-columns` til flex, når containeren bliver maks. 700px bred.

Eksempel fra `/src/components/Experience.astro`=

```CSS
section .donut_section {
  grid-column: middle / content-end;
  min-width: 0;
  display: grid;
  grid-template-columns: repeat(3, 11rem);
  gap: clamp(1.5rem, 2.5vw, 2.5rem);
  justify-content: center;
}

@container experience (max-width: 700px) {
  section > .section-text {
    grid-column: content-start / content-end;
    padding-inline-end: 0;
  }

  section .donut_section {
    grid-column: content-start / content-end;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}
```

---
