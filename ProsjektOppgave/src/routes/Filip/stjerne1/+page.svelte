<script>
    //importerer ulike komponenter og funksjoner
    import AlleTannleger from "./alle_tannleger.svelte";
    import TannlegeFakta from "../tannlegeFaktaSide/tannlegeFakta.svelte";
    import { gjennomsnittAvListe } from "../../../utility/liste.util.js";
  
    //Lager ein liste over infoen om tannlegene
    let tannlegeListe = [
      {
        navn: "Anders Solheim",
        telefon: 90074233,
        adresse: "Tyttebærveien 2",
        id: "0",
        bildeUrl:
          "https://www.tannlegeolden.no/wp-content/uploads/2017/09/Tannlege-Olden-Erlend_export.jpg",
        vurderinger: [6, 7, 9],
      },
      {
        navn: "Torstein Hansen",
        telefon: 47388935,
        adresse: "langgata 8",
        id: "1",
        bildeUrl:
          "https://g.acdn.no/obscura/API/dynamic/r1/ece5/tr_1000_2000_s_f/0000/aker/2020/4/2/16/IMG_53381.jpg?chk=F478C8",
        vurderinger: [5, 4, 8],
      },
      {
        navn: "Ståle Fjellsbø",
        telefon: 47892391,
        adresse: "Prestveien 5",
        id: "2",
        bildeUrl:
          "https://strommentannlegesenter.no/wp-content/uploads/2021/01/Morten-Eliassen3.jpeg",
        vurderinger: [2, 5, 3],
      },
    ];
  
    //Ein reaktiv array som henter alle verdiene i kvart objekt til tannlegeListe og legger til gjennomsnitt på kvert objekt. 
    //map er ein aen måte å skriv forEach på. 
    $: gjennomsnittTannlegeListe = tannlegeListe.map((tannlege) => ({
      ...tannlege,
      gjennomsnitt: gjennomsnittAvListe(tannlege.vurderinger),
    }));
  
    //Ein reaktiv array som sorterer objektene etter gjennomsnittet
    $: sortertTannlegeListe = gjennomsnittTannlegeListe.sort((tannlege1, tannlege2) => tannlege2.gjennomsnitt-tannlege1.gjennomsnitt);
  
  
  
    //Definerer valgtTannlege som undefined
    let valgtTannlegeId = undefined;
  
    //Holder tannlegeobjekt som tilhører valgt tannlegeId
    $: valgtTannlege = sortertTannlegeListe.find((tannlege) => tannlege.id === valgtTannlegeId)
  
    //Funksjon som legger til nyeste vurdering i tannlegeListe
    const leggTilVurdering = (midlertidigVurdering) => {
      tannlegeListe[valgtTannlegeId].vurderinger = [
        ...tannlegeListe[valgtTannlegeId].vurderinger,
        midlertidigVurdering,
      ];
      console.log(tannlegeListe)
    };
  
    //Funksjon som tilbakestiller valgtTannlege til undefined, slik at ein kommer tilbake til framsida
    const tilbakestillTannlege = () => {
      valgtTannlegeId = undefined;
    };
  
    //Skifter side
    const velgNyTannlege = (tannlegeId) => {
      valgtTannlegeId = tannlegeId;
    };
  
  
  
  </script>
  
  <!----Måten ein bestemmer kva side ein skal vere på, utifra kva valgtTannlege er har som verdi---------------------------------------------->
  {#if valgtTannlegeId !== undefined}
    <TannlegeFakta
      tannlegeInfo={valgtTannlege}
      {tilbakestillTannlege}
      leggtilVurdering={leggTilVurdering}
    />
  {:else}
    <AlleTannleger tannleger={sortertTannlegeListe} {velgNyTannlege} />
  {/if}
  