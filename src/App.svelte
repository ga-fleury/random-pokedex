<script>
    var pokeNumber = Math.floor(Math.random() * 899);
    var pokeURL = "https://pokeapi.co/api/v2/pokemon/" + pokeNumber;
    let currentPokemon = {};
    let pokeImage;
    let pokeTypes = [];

    // POKE API FETCH

    // fetch(pokeURL)
    //   .then(function (response) {
    //     return response.json();
    //   })
    //   .then((json) => {
    //     currentPokemon = json;
    //     pokeImage = currentPokemon.sprites.other["official-artwork"].front_default;
    //     console.log(currentPokemon);
    //   });

    fetch("bulba.json")
        .then(function (response) {
            return response.json();
        })
        .then((json) => {
            currentPokemon = json;
            pokeImage = currentPokemon.sprites.other["official-artwork"].front_default;
            pokeTypes = Object.values(currentPokemon.types);

            console.log(currentPokemon);
        });
</script>

<main>
    <h1>{currentPokemon.name} #{currentPokemon.id}</h1>
    <div class="pokewrapper">
        <img src={pokeImage} alt="" />
        {#each pokeTypes as type}
            <img src="./img/{type.type.name}.png" alt="" class="poketype" />
            <p class="background-color-{type.type.name}">{type.type.name}</p>
        {/each}
    </div>
</main>

<style lang="scss">
    $color-grass: #9bcc50;
    $color-poison: #9bcc50;

  .background-color-grass {
    background-color: $color-grass;
  }
    .poketype {
        width: 100px;
    }
    .pokewrapper {
        display: flex;
        justify-content: center;
        align-items: flex-start;
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
