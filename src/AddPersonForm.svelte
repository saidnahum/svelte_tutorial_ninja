<script>
   import { createEventDispatcher } from "svelte";

   let dispatch = createEventDispatcher();

   let name,
      color,
      age,
      react = false,
      sveltekit = false,
      javascript = false;
   let skills = [];

   const handleSubmit = () => {
      const person = {
         name,
         color,
         age,
         skills,
         id: Math.floor(Math.random() * 1000)
      };

      dispatch("addPerson", person);

   };
</script>

<main>
   <h1>Formulario</h1>
   
   <form on:submit|preventDefault={handleSubmit}>
      <input type="text" placeholder="name" bind:value={name} />
      <!-- <input type="text" placeholder="color" bind:value={color}> -->
   
      <select bind:value={color}>
         <option value="black">Black</option>
         <option value="orange">Orange</option>
         <option value="brown">Brown</option>
         <option value="white">White</option>
      </select>
   
      <input type="number" placeholder="age" bind:value={age} /><br />
   
      <label for="">Skills</label><br />
      <!--<input type="checkbox" bind:checked={react}>React <br>
      <input type="checkbox" bind:checked={sveltekit}>Sveltekit <br>
      <input type="checkbox" bind:checked={javascript}>JavaScript <br> -->
   
      <input type="checkbox" bind:group={skills} value="react" />React <br />
      <input type="checkbox" bind:group={skills} value="sveltekit" />Sveltekit
      <br />
      <input type="checkbox" bind:group={skills} value="javascript" />JavaScript
      <br />
   
      <button>Add Person</button>
   </form>
</main>