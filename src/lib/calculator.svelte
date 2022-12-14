<main>
    <section>
        <h4>Compensation Calculator</h4>
        <form>
            <Input name="averageIncome" type="€" label="Average Income" isNumeric="true"
                   bind:value={averageIncome}/>
            <Input name="daysOnLeave" type="days" label="Days on sick-leave" isNumeric="true"
                   bind:value={daysOnSickLeave}/>
            <Checkbox name="isTuberculosis" label="I have tuberculosis" bind:checked={isTuberculosis}/>
            <Button content={"Calculate"} on:click={calculate}/>
        </form>
    </section>
    <section class="compensation">
        <div>
            <p class="compensation-category">The employer compensates<br> <strong>{employerDays} days</strong></p>
            <p class="compensation-amount"><strong>{getString(employerAmount)}€</strong></p>
            <p class="compensation-daily">Daily allowance<br>{getString(dailyComp)} €</p>
        </div>
        <div>
            <p class="compensation-category">Health Insurance compensates<br> <strong>{insuranceDays} days</strong></p>
            <p class="compensation-amount"><strong>{getString(insuranceAmount)}€</strong></p>
            <p class="compensation-daily">Daily allowance<br>{getString(dailyComp)} €</p>
        </div>
    </section>
    <section class="compensation-total">
        <p class="compensation-category">Compensation total for { daysOnSickleaveCopy } days (net)</p>
        <p class="compensation-total-amount">{ getString(employerAmount + insuranceAmount) }€</p>
    </section>
</main>

<script lang="ts">
    import Button from '$lib/button.svelte';
    import Input from '$lib/input.svelte';
    import Checkbox from '$lib/checkbox.svelte';

    let averageIncome: number;
    let daysOnSickLeave: number;
    let isTuberculosis = false;

    let employerDays = 0;
    let employerAmount = 0;

    let insuranceDays = 0;
    let insuranceAmount = 0;

    let daysOnSickleaveCopy = 0;
    let dailyComp = 0;

    function getString(s: number): string {
        return s.toLocaleString("et", {maximumFractionDigits: 2});
    }

    function calculate(): void {
        daysOnSickleaveCopy = daysOnSickLeave;

        // Total days excluding unpaid
        let totalDays = Math.min(daysOnSickLeave, isTuberculosis ? 240 : 182);
        totalDays = Math.max(totalDays - 3, 0);
        // Average daily compensation
        // = 70% of average daily income
        dailyComp = (0.7 * averageIncome / 30);

        employerDays = Math.min(totalDays, 5);
        employerAmount = employerDays * dailyComp;
        // Days excluding unpaid and employer's
        insuranceDays = Math.max(totalDays - 5, 0);
        insuranceAmount = insuranceDays * dailyComp;

    }

</script>

<style lang="scss">
  @use '$lib/_variables.scss' as *;

  main {
    color: $metal_dark;
    background-color: $white;
    clip-path: polygon(
                    0 1rem, 1rem 0, calc(100% - 1rem) 0, 100% 1rem, 100% calc(100% - 1rem),
                    calc(100% - 1rem) 100%, 1rem 100%, 0 calc(100% - 1rem), 0 1rem
    );

    padding: 60px 0px;
    height: min-content;
    min-width: 320px;

    h4 {
      margin-bottom: 20px;
    }

    section {
      padding: 20px;
    }

    .compensation {
      display: grid;
      grid-template-columns: 1fr 1fr;

      div {
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
      }

      p strong {
        font-weight: 700;
      }

      &-category {
        font-weight: 400;
        font-size: 14px;
        line-height: 15px;
        margin-bottom: 10px;
      }

      &-amount {
        font-size: 18px;
        line-height: 20px;
      }

      &-daily {
        font-size: 12px;
        line-height: 15px;
        color: $metal_middle;
      }
    }

    .compensation-total {
      display: flex;
      flex-direction: column;
      align-items: center;

      &-amount {
        font-weight: 700;
        font-size: 24px;
        line-height: 30px;
      }
    }
  }

  .compensation-total {
  }

  form {
    display: flex;
    flex-direction: column;
    row-gap: 20px;
  }

  section:not(:last-of-type) {
    border-bottom: 1px solid $metal_light;
  }
</style>
