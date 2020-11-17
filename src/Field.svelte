<div class="field" onClick={onClick} />

<script>
export let onClick;
</script>

<style>

.field {
   background-color: rgb(203, 255, 196);
   border: 1px solid rgb(65, 161, 0);
   cursor: pointer;
   border-radius: 20px;
}

.field:hover {
   background-color: rgb(182, 255, 173);
   border: 1px solid rgb(38, 95, 0)
}
</style>
