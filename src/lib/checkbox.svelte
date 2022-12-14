<div class="checkbox">
    <input id={name} bind:checked={checked} type="checkbox">
    <label for={name}>{label}</label>
</div>

<script lang="ts">
    export let name: string;
    export let label: string;
    export let checked: boolean = true;
</script>

<style lang="scss">
  @use '$lib/_variables.scss' as *;

  .checkbox {
    display: flex;
    column-gap: 10px;
    cursor: pointer;
  }

  input[type="checkbox"] {
    position: relative;

    width: 20px;
    height: 20px;

    background: linear-gradient($white, $white) padding-box, $gradient_metal_light border-box;
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba($black, 0.1);
    border: 2px solid transparent;

    &:checked::after {
      background-image: url("./assets/check.svg");
      background-repeat: no-repeat;
      background-position: center;
      position: absolute;
      content: "";
      width: 100%;
      height: 100%;
    }
  }
</style>
