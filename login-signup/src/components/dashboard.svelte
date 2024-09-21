<script>
  import { onMount } from "svelte";
  let firstName = ""; // Variable to store the user's first name input
  let user = ""; // Variable to hold the fetched user data
  // Async function to search for a user based on first name
  async function searchUser() {
    user = "";// Clear previous user data before fetching new results
    try {
       // Fetch user data from the API with the specified first name
      const response = await fetch(
        `http://localhost:3001/search/get-all-users?first_name=${encodeURIComponent(firstName)}`,
        {
          method: "GET",
          headers: {
            Authorization: `Bearer ${localStorage.getItem("token")}`,// Include authorization token from local storage
          },
        },
      );
      const Userfounded = await response.json();// Parse the JSON response from the server
      user = Userfounded.user;  // Store the found user data in the user variable
    } catch (err) {
      // Log any errors that occur during the fetch process
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
