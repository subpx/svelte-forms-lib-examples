<script>
  import createForm from "svelte-forms-lib";
  import yup from "yup";
  import CustomInput from "../../CustomFormInput.svelte";

  const { form, errors, state, handleChange, handleSubmit } = createForm({
    initialValues: {
      name: "",
      email: "",
      sex: ""
    },
    validationSchema: yup.object().shape({
      name: yup.string().required(),
      email: yup
        .string()
        .email()
        .required(),
      sex: yup.string().required()
    }),
    onSubmit: ({ values }) => {
      console.log("make form request:", values);
    }
  });

  function customInputEvent(name, value) {
    return {
      target: {
        name, 
        value
      }
    }
  }
</script>

<style>
  .error {
    display: block;
    color: red;
    font-size: 12px;
  }
</style>

<form on:submit={handleSubmit}>
  <label for="name">name</label>
  <input
    id="name"
    name="name"
    on:change={handleChange}
    on:blur={handleChange}
    bind:value={$form.name} />
  {#if $errors.name}
    <hint class="error">{$errors.name}</hint>
  {/if}

  <label for="email">email</label>
  <input
    id="email"
    name="email"
    on:change={handleChange}
    on:blur={handleChange}
    bind:value={$form.email} />
  {#if $errors.email}
    <hint class="error">{$errors.email}</hint>
  {/if}

  <label for="sex">sex</label>
  <CustomInput 
    on:change={(event) => handleChange(customInputEvent('sex', event.detail))}
    bind:selected={$form.sex}
  />
  {#if $errors.sex}
    <hint class="error">{$errors.sex}</hint>
  {/if}

  <button type="submit">submit</button>
</form>

<!-- print out state for debugging -->
<pre>{JSON.stringify($state, null, 2)}</pre>
