<script>
  import Basic from "./examples/basic/Basic.svelte";
  import YupValidation from "./examples/yup-validation/YupValidation.svelte";
  import CustomValidation from "./examples/custom-validation/CustomValidation.svelte";

  let tab = "basic";

  function setTab(t) {
    tab = t;
  }
</script>

<style>
  .container {
    max-width: 700px;
    margin: auto;
  }

  .header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 100px;
  }

  nav {
    min-height: 50px;
  }

  a {
    color: #000;
    margin-right: 20px;
  }

  a:hover {
    text-decoration: none;
  }

  .active {
    color: #ff3e00;
  }

  .logo {
    font-size: 24px;
    color: #ff3e00;
  }

  .note {
    background: #f7f7f7;
    border-radius: 2px;
    border-left: 3px solid #ff3e00;
    padding: 15px;
    line-height: 1.8;
    font-size: 14px;
  }
</style>

<div class="container">
  <header class="header">
    <h1 class="logo">Svelte forms lib examples</h1>
  </header>

  <nav>
    <a
      href="#basic"
      class:active={tab === 'basic'}
      on:click={() => setTab('basic')}>
      Basic
    </a>
    <a href="#yup" class:active={tab === 'yup'} on:click={() => setTab('yup')}>
      Yup validation
    </a>
    <a
      href="#custom"
      class:active={tab === 'custom'}
      on:click={() => setTab('custom')}>
      Custom validation
    </a>
  </nav>

  <main>
    {#if tab === 'basic'}
      <p class="note">Basic example contains no validation</p>
      <Basic />
    {/if}

    {#if tab === 'yup'}
      <p class="note">
        Example using Yup as validation. Validation happens when input changes
        and upon form submission.
      </p>
      <YupValidation />
    {/if}

    {#if tab === 'custom'}
      <p class="note">
        Example using Yup as validation. The validate function allows for custom
        validation. Validation is only fired upon submission. Field validation
        coming soon.
      </p>
      <CustomValidation />
    {/if}
  </main>
</div>
