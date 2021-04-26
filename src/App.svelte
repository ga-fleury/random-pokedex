<script>
  var pokeNumber = Math.floor(Math.random() * 899);
  var pokeURL = "https://pokeapi.co/api/v2/pokemon/" + pokeNumber;
  let currentPokemon = {};
  let img;

  fetch(pokeURL)
    .then(function (response) {
      return response.json();
    })
    .then((json) => {
      currentPokemon = json;
      img = currentPokemon.sprites.other["official-artwork"].front_default;
      console.log(currentPokemon);
    });
</script>

<main>
  <h1>{currentPokemon.name} #{currentPokemon.id}</h1>
  <div class="pokewrapper">
    <img src={img} alt="" />
  </div>
</main>

<style>
  .pokewrapper {
    display: flex;
    justify-content: center;
  }
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
