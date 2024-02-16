<!--Eiga fil til stjerner-->
<script src="https://kit.fontawesome.com/5aea8750d8.js" crossorigin="anonymous">
   
    
      const alternativer = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10].reverse();
    
      let midlertidigVurdering = 5;
      //Math.round(gjennomsnitt)
    </script>
    
    <div class="stjerneVurderingContainer">
      {#each alternativer as alternativ}
        <input
          value={alternativ}
          bind:group={midlertidigVurdering}
          type="radio"
          name="star"
          id={alternativ.toString()}
        /><label for={alternativ.toString()} />
      {/each}
    </div>
    <head>
        <link
        rel="stylesheet"
        href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css"
      />
      <link
        href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.missing_component.css"
        rel="stylesheet"
      />
    </head>
    
        <style>
    .stjerneVurderingContainer {
        display: flex;
        position: relative;
        flex-direction: row-reverse; /* Change from 'row' to 'row-reverse' */
        align-items: center;
        width: 60%;
        top: -3%;
        margin: 0;
        padding: 0;
    }
    .stjerneVurderingContainer input {
        display: none;
    }
    .stjerneVurderingContainer label {
        display: block;
        cursor: pointer;
        width: 2vh;
    }
    .stjerneVurderingContainer label:before {
        content: "\f005";
        font-family: fontAwesome;
        position: relative;
        display: block;
        font-size: 2vh;
    }
    .stjerneVurderingContainer label:after {
        content: "\f005";
        font-family: fontAwesome;
        position: absolute;
        display: block;
        font-size: 2vh;
        color: orange;
        top: 0;
        opacity: 0;
        transition: 0.5s;
        text-shadow: 0 2px 5px rgba(0, 0, 0, 0.5);
    }
    .stjerneVurderingContainer label:hover:after,
    .stjerneVurderingContainer input:hover ~ label:after,
    .stjerneVurderingContainer input:checked ~ label:after {
        opacity: 1;
    }
</style>

 
    