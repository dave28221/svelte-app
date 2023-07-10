<script>
    import { createForm } from "svelte-forms-lib";
    import * as yup from "yup";

    const { form, handleChange, handleSubmit, errors, state } = createForm({
        initialValues: {
            name: "",
            email: "",
        },
    validationSchema: yup.object().shape({
        name: yup.string().required(),
        email: yup.string().email().required()
    }),
    onSubmit: (values) => {
            alert(JSON.stringify(values));
    }
});
</script>

<div class="signUpPage">
<h1 class="makeBorder">Sign Up</h1>
<div class="centreForm">
    <form on:submit={handleSubmit}>
        <label for="name">Name</label>
        <input
            id="name"
            name="name"
            on:change={handleChange}
            bind:value={$form.name}
        />
        {#if $errors.name}
        <small>{$errors.name}</small>
        {/if}

        <label for="email">Email</label>
        <input
            id="email"
            name="email"
            on:change={handleChange}
            bind:value={$form.email}
        />
        {#if $errors.email}
        <small>{$errors.email}</small>
        {/if}


        <button class="submitSign" type="submit">Submit</button>
    </form>
</div>
</div>

<style>
    
    .signUpPage{
        padding-bottom:100px;
    }

    .submitSign{
       margin-top:40px !important;
       margin: 0 auto;
       background-color: rgb(166, 22, 22);
    }
    .centreForm {
        margin-top:40px !important;
        display: flex;
        justify-content: center;
        align-items: center;
        border-top:none !important;
        width:35%;
        margin: 0 auto;
        padding:50px;
        box-shadow: 16px 15px 34px 4px rgba(0, 0, 0, 0.38);
     
    }

    form {
        width: 100%;
        max-width: 400px;
    }
    :root {
        --primary-light: #a6f9d6;
        --primary: #5f91b0;
        --primary-dark: #8098b1;
        --secondary: #1e2145;
        --white: #fff;
        --grey: #e6e6ff;
        --grey-dark: #6d7098;
        --red: #ff6b6b;
    }

    input,
    select,
    textarea {
        font-family: inherit;
        font-size: inherit;
        max-width: 400px;
        width: 100%;
        padding: 12px;
        box-sizing: border-box;
        border: 1px solid var(--grey);
        border-radius: 4px;
        transition: all 150ms ease;
        background: var(--white);
    }

    select {
        height: 45px;
    }

    input:focus,
    select:focus,
    textarea:focus {
        outline: none;
        box-shadow: 0 0 0 4px rgb(227, 227, 245);
        border-color: var(--grey);
    }

    input:disabled,
    select:disabled,
    textarea:disabled {
        color: #ccc;
    }

    button {
        color: #fff;
        background-color: var(--primary);
        border: none;
        text-transform: uppercase;
        letter-spacing: 1.8px;
        outline: none;
        border-radius: 4px;
        display: block;
        margin-top: 12px;
        line-height: 1.8;
        font-size: 12px;
        padding: 10px 18px;
        min-width: 120px;
        transition: all 150ms ease;
        cursor: pointer;
    }

    button:disabled {
        background-color: var(--grey);
    }

    button:focus:not(:disabled) {
        box-shadow: 0 0 0 4px var(--primary-light);
    }

    button:hover:not(:disabled) {
        background-color: var(--primary-dark);
    }

    label {
        display: block;
        color: var(--grey-dark);
        font-weight: bold;
        margin-top: 20px;
        margin-bottom: 4px;
        text-transform: uppercase !important;
        font-size: 12px;
        letter-spacing: 1.9px;
        line-height: 2;
    }

    /* used for errors */
    small {
        display: block;
        font-size: 12px;
        color: var(--red);
        margin-top: 10px;
    }
</style>
