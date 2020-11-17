<main>
   <h1>Tic Tac Toe</h1>
   <label for="level">Select a level:</label>
   <select name="level" id="level">
      <option value="">Beginner</option>
      <option value="saab">Medium</option>
      <option value="mercedes">Hard</option>
   </select>

   <div class="game-frame">
      {#each Array(9) as field, index}
    <Field onClick={()=>{console.log('er4t34regrfs')}} />
{/each}
   </div>
   <h3>New game</h3>
</main>

<script>
import Field from './Field.svelte'

let winning = [
   [1, 2, 3],
   [4, 5, 6],
   [7, 8, 9],
   [1, 4, 7],
   [2, 5, 8],
   [3, 6, 9],
   [1, 5, 9],
   [3, 5, 7]
]

const winner = () => {
   console.log('Checking for winner');
}
</script>
<style>
main {
   text-align: center;
   padding: 1em;
   max-width: 240px;
   margin: 0 auto;
}

.game-frame {
   width: 400px;
   height: 400px;
   margin: 0 auto;
   display: grid;
   grid-template-columns: repeat(3, 1fr);
   gap: 10px;
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
