<script>
  import { onMount } from "svelte";
  let firstName = "";
  let user = '';

  async function searchUser() {
    user = '';
    try {
      const response = await fetch(
        `http://localhost:3001/search/get-all-users?first_name=${encodeURIComponent(firstName)}`,
        {
          method: "GET",
          headers: {
            Authorization: `Bearer ${localStorage.getItem("token")}`, // Adjust token retrieval as needed
          },
        },
      );
      const Userfounded = await response.json();
      user = Userfounded.user;
    } catch (err) {
      console.error("Error:", err);
      errorMessage = "Server error";
    }
  }
</script>

<main>
  <h1>Search Users</h1>
  <input type="text" bind:value={firstName} placeholder="Enter first name" />
  <button on:click={searchUser}>Search</button>



  {#if user}
    <div class="result">
      <h2>User Found:</h2>
      <p>First Name: {user.first_name}</p>
      <p>Email: {user.email}</p>
    </div>
  {/if}
</main>

<style>

  .result {
    margin-top: 20px;
  }
</style>
