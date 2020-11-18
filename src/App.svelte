<script>
  import Field from "./Field.svelte";

  let winCombos = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];

  let arr = [];
  let usersTurn = true;
  let message = "";

  const winner = (perc) => {
    if (arr.length >= 5) {
      let arr2 = arr.filter((val, i) => i % 2 == perc);
      console.log(`$Array so far clicked: ${arr2}`);
      winCombos.forEach((array) => {
        if (array.every((element) => arr2.includes(element))) {
          console.log(` The winning combination: ${array}`);
          if (perc == 0) {
            message = "You Win!";
            const game = document.querySelector(".game-frame");
            console.log(`winning array: ${array}`);
            array.forEach((arr, index) => {
              game.childNodes[arr].style.backgroundColor = "#58D68D";
            });
          } else {
            message = "PC wins!";
            const game = document.querySelector(".game-frame");
            array.forEach((arr, index) => {
              game.childNodes[arr].style.backgroundColor = "#EC7063";
            });
          }
        }
      });
    }
  };

  const userMove = (e) => {
    if (e.target.firstChild.innerHTML == "" && !message && usersTurn) {
      e.target.firstChild.innerHTML = "X";
      arr.push(parseInt(e.target.getAttribute("number")));
      winner(0);
      usersTurn = false;
      if (arr.length != 9) {
        pcMove();
      }
      if (arr.length == 9 && !message) {
        message = "It's a tie!";
      }
    }
  };

  const pcMove = () => {
    // pc generates rand number from 0 to 8
    if (!message) {
      setTimeout(() => {
        let num;
        do {
          num = Math.floor(Math.random() * 9);
        } while (arr.includes(num));

        const game = document.querySelector(".game-frame");
        game.childNodes[num].firstChild.innerHTML = "O";

        arr.push(num);
        usersTurn = true;
        winner(1);
      }, 500);
    }
  };

  const reset = () => {
    console.log("Game has been resetted");
    message = "";
    arr = [];
    usersTurn = true;

    const game = document.querySelector(".game-frame").childNodes;
    //  console.log(game);
    game.forEach((el) => {
      el.style.backgroundColor = "";
      el.firstChild.innerHTML = "";
    });
  };
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  .game-frame {
    width: 500px;
    height: 500px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
    gap: 10px;
  }

  .title {
    color: white;
    margin-top: 20px;
    margin-bottom: 30px;
    font-size: 46px;
  }

  .reset {
    color: white;
    margin-top: 20px;
    font-size: 26px;
    cursor: pointer;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
  <h1 class="title">{!message ? 'Tic Tac Toe' : message}</h1>
  <!-- <label for="level">Select a level:</label>
  <select name="level" id="level">
    <option value="">Beginner</option>
    <option value="saab">Medium</option>
    <option value="mercedes">Hard</option>
  </select> -->

  <div class="game-frame">
    {#each Array(9) as field, index}
      <Field onClick={userMove} number={index} />
    {/each}
  </div>
  <h1 class="reset" on:click={reset}>{!message ? 'Reset' : 'New Game'}</h1>
</main>
