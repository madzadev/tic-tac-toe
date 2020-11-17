<script>
  export let onClick, number;
</script>

<style>
  .field {
    background-color: rgb(233, 196, 255);
    border: 1px solid rgb(156, 0, 161);
    cursor: pointer;
    border-radius: 20px;
    display: grid;
    place-items: center;
  }

  .field p {
    font-size: 30px;
  }

  .field:hover {
    background-color: rgb(214, 146, 253);
    border: 1px solid rgb(55, 0, 71);
  }
</style>

<div class="field" on:click={onClick} {number}>
  <p />
</div>
