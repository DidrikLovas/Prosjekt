
<!--Fil for alle tannleger sida-->
<script src="https://kit.fontawesome.com/5aea8750d8.js" crossorigin="anonymous">
    //Importerer komponenter og funksjoner
      import { rundAvEnDesimal } from "../../../utility/tall.util";
      import NavBar from "../navBar/navBar.svelte";
      import StjerneTilTannlegekort from "./stjerneTilTannlegekort/stjerneTilTannlegekort.svelte";
    
      //exporterer funksjoner og variabler
      export let tannleger;
      export let velgNyTannlege;
    
    </script>
    
    
    
    <div id="spillere-main">
      <!--Legger in navbar i toppen av dokumentet-->
      <NavBar />
      <h1 class="spillereOverskrift"><p>Tannleger</p></h1>
    
      <div id="containerSpillereStats">
        <!--Lager eit kort til kvert objekt i tannlegeListe-->
        {#each tannleger as tannlege}
          <a href="#" class="link" on:click={() => velgNyTannlege(tannlege.id)}>
            <div class="hovedSpillerKort" id={tannlege.id}>
              <div
                class="spillerKortBildeDiv"
                style="background-image: url({tannlege.bildeUrl});"
              >
                <div class="spillerNavnDiv">{tannlege.navn}</div>
              </div>
              <div class="sponsorDivClass">
                <!--Bruker ein importert funksjon som runder av talet til 1 deismal-->
                <h1 class="sponsetAv">Rating:  {rundAvEnDesimal(tannlege.gjennomsnitt)}</h1>
                <!--Legger inn stjerner som er importert frå ein anna fil-->
                <StjerneTilTannlegekort gjennomsnitt={rundAvEnDesimal(tannlege.gjennomsnitt)}></StjerneTilTannlegekort>
              </div>
            </div>
          </a>
        {/each}
      </div>
      <div id="leggtil_fjern_container">
        <div class="leggTilSpillerId leggTilSpillerStyle">
          <h1 class="leggTilSpillerId">Legg Til Tannlege</h1>
        </div>
        <div class="fjernSpillerId">
          <h1>Fjern Tannlege</h1>
        </div>
      </div>
    </div>
    
    <style>
      /*---------------------------tannleger------------------------------*/
      #spillere-main {
        flex-direction: column;
        align-content: center;
        height: 235vh;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
        position: absolute;
        margin: 0;
        background: url("https://wallpaperaccess.com/full/1805430.jpg") center;
        background-size: cover;
        background-attachment: fixed;
        align-items: center;
      }
      .spillereOverskrift {
        font-size: 7vh;
        font-weight: bolder;
        display: flex;
        justify-content: center;
        background-color: white;
        opacity: 0.5;
      }
      #containerSpillereStats {
        display: grid;
        grid-template-columns: auto auto;
        justify-content: center;
        grid-row-gap: 2vh;
        grid-column-gap: 5vh;
        margin: 50px;
      }
      .hovedSpillerKort {
        width: 40vh;
        height: 60vh;
        background: #d3d3d3;
        border: 4px solid #6b6565;
        border-radius: 10px;
        padding: 30px;
        display: flex;
        flex-direction: column;
        align-items: center;
        box-shadow: 10px 10px 30px rgba(0, 0, 0, 0.1);
        transition: 0.1s;
      }
      .hovedSpillerKort:hover {
        box-shadow: 10px 10px 30px rgba(0, 0, 0, 0.5);
        background: #bdbdbd;
        border: 6px solid #282626;
        padding: 28px;
      }
      .spillerKortBildeDiv {
        width: 100%;
        height: 100%;
        justify-content: flex-start;
        background-position: center;
        background-size: cover;
        border: 3px solid black;
      }
      .spillerNavnDiv {
        background: rgba(245, 245, 245, 0.8);
        color: black;
        font-family: fantasy;
        font-size: 4vh;
        padding: 1%;
        border-bottom-right-radius: 5vh;
        border-top-right-radius: 5vh;
        position: absolute;
        margin-top: 30vh;
        display: flex;
      }
      .sponsorDivClass {
        display: flex;
        flex-direction: column;
        align-items: center;
        border: 3px solid black;
        border-radius: 5px;
        margin: 10px;
        width: 50%;
        padding: 10px;
        background: rgba(171, 140, 111, 0.75);
      }
      
      #leggtil_fjern_container {
        display: flex;
        flex-direction: row;
        justify-content: space-evenly;
        padding: 50px;
      }
      .leggTilSpillerStyle {
        width: 50vh;
        height: 10vh;
        border: 10px solid #f3afb9;
        border-radius: 5px;
        display: flex;
        justify-content: center;
        color: #5b5c60;
        transition: 0.5s;
        box-shadow: 10px 10px 30px rgba(0, 0, 0, 0.1);
      }
      .leggTilSpillerStyle:hover {
        background: #f3afb9;
        border: 10px solid #ce969e;
        box-shadow: 10px 10px 30px rgba(0, 0, 0, 0.3);
      }
      .fjernSpillerId {
        width: 50vh;
        height: 10vh;
        border: 10px solid #4dbfa0;
        border-radius: 5px;
        display: flex;
        justify-content: center;
        color: #5b5c60;
        transition: 0.5s;
        box-shadow: 10px 10px 30px rgba(0, 0, 0, 0.1);
      }
      .fjernSpillerId:hover {
        background: #4dbfa0;
        border: 10px solid #42a48a;
        box-shadow: 10px 10px 30px rgba(0, 0, 0, 0.3);
      }
      .link {
        text-decoration: none;
        color: black;
      }
    </style>
    