<script>
  export let onClick, number;
</script>

<style>
  .field {
    background-color: #2d2d2d;
    cursor: pointer;
    border-radius: 20px;
    display: grid;
    place-items: center;
  }

  .field:hover {
    background-color: #383838;
  }

  .field p {
    font-size: 82px;
    font-weight: bold;
    color: white;
  }
</style>

<div class="field" on:click={onClick} {number}>
  <p />
</div>
