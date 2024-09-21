<script lang="ts">
  import Card, {
    Content,
    PrimaryAction,
    Actions,
    ActionButtons,
    ActionIcons,
  } from "@smui/card";
  import Button, { Label } from "@smui/button";

  import { navigate } from "svelte-routing";

  export let setActive;
  let clicked = 0;

  import Textfield from "@smui/textfield";
  import Icon from "@smui/textfield/icon";

  let User = [];
  let email = "";
  let password = "";

  async function logedin(event) {
    event.preventDefault();
    // Create an object to hold the login values
    const loginvalues = { email, password };

    const response = await fetch(
      "http://localhost:3001/login-as-existing-user/login",
      {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(loginvalues), // Convert login values to a JSON string
      },
    );

    if (response.ok) {
      const data = await response.json();

      const token = data.token; // Extract the token from the response
      if (token) {
        localStorage.setItem("token", token); // Store the token in local storage
      }

      email = "";
      password = "";

      navigate("/dashboard"); // Redirect to the dashboard
    } else {
      console.error("Failed to login", response.status, response.statusText);
    }
  }
</script>

<form on:submit={logedin}>
  <div class="card-display">
    <div class="card-container" style="border: 1px solid black;">
      <Card>
        <Content>
          <div class="columns margins">
            <div>
              <!-- svelte-ignore a11y-label-has-associated-control -->
              <mean><label>E-mail</label></mean>
              <Textfield
                class="shaped-outlined"
                variant="outlined"
                bind:value={email}
                label="E-mail"
                type="email"
              >
                <Icon class="material-icons" slot="leadingIcon">email</Icon
                ></Textfield
              >

              <pre class="status"></pre>
            </div>
            <div>
              <!-- svelte-ignore a11y-label-has-associated-control -->
              <label>Password</label>
              <Textfield
                class="shaped-outlined"
                variant="outlined"
                bind:value={password}
                label="Password"
                type="password"
              >
                <Icon class="material-icons" slot="leadingIcon">password</Icon>
              </Textfield>

              <pre class="status"></pre>
            </div>
          </div>
        </Content>
        <Actions>
          <Button type="submit" on:click={() => clicked++}>
            <Label>Login</Label>
          </Button>
          {#each ["Sign-Up"] as tab}
            <Button on:click={() => setActive(tab)}><Label>{tab}</Label></Button
            >
          {/each}
        </Actions>
      </Card>
    </div>
  </div>
</form>
<pre class="status">Clicked: {clicked}</pre>

<style>
  *
    :global(
      .shaped-outlined .mdc-notched-outline .mdc-notched-outline__leading
    ) {
    border-radius: 28px 0 0 28px;
    width: 28px;
    padding-right: 16px;
  }
  *
    :global(
      .shaped-outlined .mdc-notched-outline .mdc-notched-outline__trailing
    ) {
    border-radius: 0 28px 28px 0;
  }
  * :global(.shaped-outlined .mdc-notched-outline .mdc-notched-outline__notch) {
    max-width: calc(100% - 28px * 2);
  }
  *
    :global(
      .shaped-outlined.mdc-text-field--with-leading-icon:not(
          .mdc-text-field--label-floating
        )
        .mdc-floating-label
    ) {
    left: 26px;
  }
  * :global(.shaped-outlined) {
    padding-left: 42px;
  }
  label {
    display: inline-block;
    margin-right: 40px;
  }
  mean {
    margin-right: 28px;
  }
</style>
