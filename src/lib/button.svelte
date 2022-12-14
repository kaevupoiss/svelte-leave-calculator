<button on:click>
    { content }
</button>

<script lang="ts">
    export let content: string;
</script>

<style lang="scss">
  @use '$lib/_variables.scss' as *;

  button {
    display: grid;
    place-items: center;
    padding: 20px 40px;
    width: min-content;

    border-radius: 999px;
    background: $gradient_red;

    font-weight: 700;
    font-size: 18px;
    line-height: 20px;
    color: $white;
    text-shadow: 2px 2px 0 rgba($black, 0.4);

    transition: box-shadow 50ms ease;

    &:hover {
      box-shadow: 0 4px 10px rgba($black, 0.15), inset 0 -4px 0 rgba($black, 0.25);
    }

    &:active {
      box-shadow: 0 0 10px rgba($black, 0.25), inset 0 4px 0 rgba($black, 0.25);
    }
  }
</style>
