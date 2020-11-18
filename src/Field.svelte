<script>
  export let onClick, number;
</script>

<style>
  .field {
    background-color: #2d2d2d;
    /* border: 1px solid rgb(156, 0, 161); */
    cursor: pointer;
    border-radius: 20px;
    display: grid;
    place-items: center;
  }

  .field p {
    font-size: 52px;
    font-weight: bold;
    color: white;
  }

  .winning {
    background-color: green;
  }

  .field:hover {
    background-color: #383838;
    /* border: 1px solid rgb(55, 0, 71); */
  }
</style>

<div class="field" on:click={onClick} {number}>
  <p />
</div>
