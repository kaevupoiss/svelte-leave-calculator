<div class="container">
    <aside>
        <h1>Quam Tristique Condimentum</h1>
        <p>Duis mollis, est non commodo luctus, nisi erat porttitor ligula, eget lacinia odio sem nec elit.
            Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. <span class="red">Curabitur blandit</span>
            tempus porttitor. Integer posuere erat a ante venenatis dapibus posuere velit aliquet. Vestibulum id ligula
            porta felis euismod semper.</p>

        <section>
            <div>
                <h2>Fringilla Euismod Adipiscing Ipsum</h2>
                <p>Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Maecenas
                    faucibus
                    mollis interdum. Aenean lacinia bibendum nulla sed.</p>
                <ul>
                    <li>Tellus Ullamcorper Inceptos</li>
                    <li>Magna Condimentum
                        <ul>
                            <li>Mattis Tristique</li>
                            <li>Pharetra Pellentesque Dapibus</li>
                        </ul>
                    </li>
                    <li>Aenean Inceptos</li>
                    <li>Parturient Bibendum</li>
                </ul>
            </div>
            <img src={illustrative} alt="A bedside table with books and files">
        </section>


    </aside>
    <Calculator/>
</div>

<script lang="ts">
    import illustrative from '$lib/assets/illustrative.png';
    import Calculator from '$lib/calculator.svelte';

</script>

<style lang="scss">
  @use "$lib/_variables.scss" as *;

  .container {
    display: flex;
    flex-direction: column-reverse;
    row-gap: 100px;
    width: 100%;
    min-height: 100vh;
    height: 100%;
    padding: 20px;

    background: $gradient-metal;

    @media screen and (min-width: 580px) {
      padding: 50px;
    }

    @media screen and (min-width: 768px) {
      padding: 100px;
    }

    @media screen and (min-width: 1280px) {
      display: grid;
      grid-template-columns: 1fr min-content;
      column-gap: 100px;
    }
  }

  h1 {
    margin-bottom: 20px;
  }

  span.red {
    color: $red;
  }

  section {
    margin-top: 40px;
    display: flex;
    flex-direction: column-reverse;
    row-gap: 20px;

    div {
      display: flex;
      flex-direction: column;
      row-gap: 20px;
    }

    img {
      height: min-content;
      border-radius: 10px;
    }

    @media screen and (min-width: 768px) {
      flex-direction: row;
      column-gap: 40px;
    }
  }

  li {
    position: relative;
    font-weight: 400;
    font-size: 18px;
    line-height: 30px;
    margin-left: 30px;
    margin-block: 10px;

    > ul {
      > li::before {
        width: 12px;
        background: $gradient_metal_light;
      }
    }

    &::before {
      position: absolute;
      top: 13px;
      left: -25px;
      content: "";
      height: 4px;
      width: 16px;
      background: $gradient_red;
    }
  }
</style>
