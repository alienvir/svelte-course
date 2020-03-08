<script>
  let newPassword = "";
  let passwords = [];
  let error = false;

  $: if (newPassword.trim().length < 5) {
    error = "short";
  } else if (newPassword.trim().length > 10) {
    error = "long";
  } else {
    error = false;
  }

  const deletePassword = id => {
    passwords = passwords.filter(element => element.id !== id);
  };

  const savePassword = () => {
    if (!error) {
      passwords = [...passwords, { id: Math.random(), text: newPassword }];
    }
    newPassword = "";
  };
</script>

<style>
  button {
    margin: 1rem 0;
  }
  p.error {
    color: red;
  }
  li {
    margin: 0.7rem 0;
    cursor: pointer;
  }
  div.passwordList {
    background-color: white;
    border: 1px solid darkgray;
    padding-left: 1rem;
    width: 50%;
  }
</style>

{#if passwords.length}
  <div class="passwordList">
    <h3>Saved Passwords</h3>
    <p>Click to remove from the list.</p>
    <ul>
      {#each passwords as password, index (password.id)}
        <li on:click={() => deletePassword(password.id)}>{password.text}</li>
      {/each}
    </ul>
  </div>
{/if}

<div>
  <p>Enter a password between 5 and 10 characters.</p>
  <input type="password" bind:value={newPassword} />
  {#if error}
    <p class="error">This password is too {error}!</p>
  {:else}
    <button on:click={savePassword}>Save</button>
  {/if}
</div>
