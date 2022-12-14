<div class="input">
    <label for={name}>{label}</label>
    <div class="input__wrapper">
        <input bind:value={value}
               id={name}
               class="value"
               type="text"
               inputmode={isNumeric ? 'numeric' : null}
               pattern={isNumeric ? '\\d*' : null}
               autocomplete="off"
        />
        <span class="type">{type}</span>
    </div>
</div>

<script lang="ts">
    export let name: string;
    export let type: string;
    export let label: string;
    export let value: string;
    export let isNumeric: boolean = false;

    $: value = isNumeric ? value.replace(/[^0-9]/g, '') : value;

</script>
<style lang="scss">
  @use '$lib/_variables.scss' as *;

  .input {
    color: $metal_dark;
  }

  input {
    width: 100%;
  }

  label {
    display: block;
    margin-bottom: 5px;
  }

  .input__wrapper {
    display: flex;
    padding: 10px;

    background: linear-gradient($white, $white) padding-box, $gradient_metal_light border-box;
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba($black, 0.1);
    border: 2px solid transparent;
  }

</style>
