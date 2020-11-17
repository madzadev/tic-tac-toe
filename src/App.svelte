<script>
  export let name;
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  .game-frame {
    width: 600px;
    height: 600px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
  }

  .field {
    background-color: bisque;
    border: 1px solid grey;
    cursor: pointer;
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

<main>
  <h1>Tic Tac Toe</h1>
  <div class="game-frame">
    <div class="field" />
    <div class="field" />
    <div class="field" />
    <div class="field" />
    <div class="field" />
    <div class="field" />
    <div class="field" />
    <div class="field" />
    <div class="field" />
  </div>
</main>
