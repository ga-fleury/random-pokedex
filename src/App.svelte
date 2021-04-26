<script>
    var pokeNumber = Math.floor(Math.random() * 899);
    var pokeURL = "https://pokeapi.co/api/v2/pokemon/" + pokeNumber;
    var pokeGenerationURL = "https://pokeapi.co/api/v2/pokemon-species/" + pokeNumber;
    let currentPokemon = {};
    let pokeImage;
    let pokeTypes = [];
    let pokeID;
    let pokeGeneration;

    //turns numbers 1 to 899 into 001...079..898
    let threeDigits = function (myNumber) {
        let formattedNumber = myNumber.toLocaleString("en-US", {
            minimumIntegerDigits: 3,
            useGrouping: false,
        });
        console.log(
            "Input:    " + myNumber + "\n" + "Output:   " + formattedNumber
        );
        return (pokeID = formattedNumber);
    };

    /* 
    POKE API FETCH
    */

    //first fetch pokemon characteristics
    fetch(pokeURL)
        .then((response) => {
            return response.json();
        })
        .then((json) => {
            currentPokemon = json;
            pokeImage =
                currentPokemon.sprites.other["official-artwork"].front_default;
            pokeTypes = Object.values(currentPokemon.types);
            pokeID = threeDigits(currentPokemon.id);

            console.log(currentPokemon);

            // fetch pokémon generation
            return fetch(pokeGenerationURL)
        })
        .then((response) => {
            return response.json();
        })
        .then((json) => {
            console.log(json.generation.name);
            return pokeGeneration = json.generation.name.toUpperCase();
        });

    //pokemon generation fetch
 

    // fake poke api fetch (returns only bulbasaur)

    // fetch("bulba.json")
    //     .then(function (response) {
    //         return response.json();
    //     })
    //     .then((json) => {
    //         currentPokemon = json;
    //         pokeImage =
    //             currentPokemon.sprites.other["official-artwork"].front_default;
    //         pokeTypes = Object.values(currentPokemon.types);
    //         pokeID = threeDigits(currentPokemon.id);

    //         console.log(currentPokemon);
    //         return currentPokemon;
    //     });
</script>

<main>
    <h1>
        {currentPokemon.name} <span class="light">#{pokeID}</span>
    </h1>
    <h4>{pokeGeneration}</h4>
    <div class="pokewrapper">
        <div class="pokedex-left">
            <img src={pokeImage} alt="" height="475" width="475" />
        </div>
        <div class="pokedex-right">
            {#each pokeTypes as type}
                <div class="poketype-card">
                    <div class="background-color-{type.type.name}-div">
                        <img
                            src="./img/{type.type.name}.svg"
                            alt=""
                            class="poketype"
                        />
                    </div>
                    <p class="poketype-text">{type.type.name}</p>
                </div>
            {/each}
        </div>
    </div>
</main>

<svelte:head>
    <link rel="preconnect" href="https://fonts.gstatic.com" />
    <link
        href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;900&display=swap"
        rel="stylesheet"
    />
</svelte:head>

<style lang="scss">
    $types: (
        "bug": #92bd2d,
        "dark": #595761,
        "dragon": #0c6ac8,
        "electric": #f2d94e,
        "fairy": #ef90e6,
        "fighting": #d3425f,
        "fire": #fba64c,
        "flying": #a1bbec,
        "ghost": #5f6dbc,
        "grass": #60bd58,
        "ground": #da7c4d,
        "ice": #76d1c1,
        "normal": #a0a29f,
        "poison": #b763cf,
        "psychic": #fa8582,
        "rock": #c9bc8a,
        "steel": #5795a3,
        "water": #539ddf,
    );

    @each $type, $color in $types {
        .background-color-#{$type}-div {
            background-color: $color;
            border-radius: 100%;
            padding: 10px;
            box-shadow: 0px 0px 30px 4px lighten($color, 30);
        }

        .background-color-#{$type} {
            background-color: $color;
        }
    }

    @keyframes fadeInTop {
        0% {
            opacity: 0;
            transform: translateY(-50px);
        }
        100% {
            opacity: 100%;
            transform: translateY(0px);
        }
    }

    .poketype {
        width: 50px;
        &-text {
            font-family: "Orbitron", sans-serif;
            margin: 5px;
            font-weight: 900;
        }
        &-card {
            margin: 5px;
        }
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
        font-family: "Orbitron";
        animation: fadeInTop 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    }

    h1 {
        color: #313131;
        text-transform: uppercase;
        font-size: 4em;
        font-weight: 900;
        font-family: "Orbitron";
        margin: 0;
        margin-top: 100px;
    }

    h4 {
        margin: 0;
    }

    .light {
        font-weight: 400;
    }

    @media (min-width: 640px) {
        main {
            max-width: none;
        }
    }
</style>
