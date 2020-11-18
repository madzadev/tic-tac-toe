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

      winCombos.forEach((array) => {
        if (array.every((element) => arr2.includes(element))) {
          if (perc == 0) {
            message = "You Win!";
            const game = document.querySelector(".game-frame");
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
        // easy - number picked at random
        do {
          num = Math.floor(Math.random() * 9);
        } while (arr.includes(num));

        let arr2 = arr.filter((val, i) => i % 2 == 0);
        let arr3 = arr.filter((val, i) => i % 2 == 1);

        winCombos.forEach((array) => {
          if (
            array.some((element) => arr2.includes(element)) &&
            !array.some((element) => arr3.includes(element))
          ) {
            console.log(`Possible winning combinations: ${array}`);

            const findCommon = (a, b) => {
              return a.filter((n) => {
                return b.indexOf(n) !== -1;
              });
            };

            const findMissing = (a, b) => {
              return a.filter((item) => b.indexOf(item) == -1);
            };

            const common = findCommon(array, arr2);

            if (common.length == 2) {
              if (!arr.includes(findMissing(array, common))) {
                num = findMissing(array, common);
              }
            } else if (common.length == 1) {
              // console.log("not dangerous");
              // num = findMissing(array, common)[1];
            }
          }
        });

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
  <div class="game-frame">
    {#each Array(9) as field, index}
      <Field onClick={userMove} number={index} />
    {/each}
  </div>
  <h1 class="reset" on:click={reset}>{!message ? 'Reset' : 'New Game'}</h1>
</main>
