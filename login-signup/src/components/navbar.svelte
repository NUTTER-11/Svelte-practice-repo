<script lang="ts">
  import Tab, { Label } from "@smui/tab";
  import TabBar from "@smui/tab-bar";
  import Paper, { Content } from "@smui/paper";
  import Logincard from "./logincard.svelte";
  import Signupcard from "./signupcard.svelte";

  let active = "Login";
  function setActive(tab) {
    active = tab;
  }
</script>

<div>
  <!--
    Note: tabs must be unique. (They cannot === each other.)
  -->
  <TabBar tabs={["Login", "Sign-Up"]} let:tab bind:active>
    <Tab {tab}>
      <Label>{tab}</Label>
    </Tab>
  </TabBar>

  {#if active === "Login"}
    <Paper variant="unelevated">
      <Content>
        <main>
          <Logincard {setActive}></Logincard>
        </main>
      </Content>
    </Paper>
  {:else if active === "Sign-Up"}
    <Paper variant="unelevated">
      <Content>
        <main>
          <Signupcard {setActive}></Signupcard>
        </main>
      </Content>
    </Paper>
  {/if}

  <!-- <div style="margin-top: 1em;">
    {#each ["Sign-Up"] as tab}
      <Button on:click={() => (active = tab)}><Label>{tab}</Label></Button>
    {/each}
  </div> -->
</div>

<style>
  main {
    text-align: center;
    padding-left: 200px;
    padding-right: 200px;
    margin: 0 auto;
  }
</style>
