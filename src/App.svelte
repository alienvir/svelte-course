<script>
  import ContactCard from "./ContactCard.svelte";

  let name = "";
  let jobTitle = "";
  let description = "";
  let userImage;
  let age = 30;

  $: uppercaseName = name.toUpperCase();

  $: console.log(name);

  $: if (name === "Maximilian") {
    console.log("It runs!");
    age = 31;
  }

  function incrementAge() {
    age += 1;
  }

  function changeName() {
    name = "Maximilian";
  }

  function nameInput(event) {
    const enteredValue = event.target.value;
    name = enteredValue;
  }
</script>

<style>
  h1 {
    color: purple;
  }
</style>

<h1>Hello {uppercaseName}, my age is {age}!</h1>
<button on:click={incrementAge}>Change Age</button>
<input type="text" bind:value={name} />
<input type="text" bind:value={jobTitle} />
<input type="text" bind:value={description} />
<input type="text" bind:value={userImage} />

<ContactCard {name} {jobTitle} {description} {userImage} />
