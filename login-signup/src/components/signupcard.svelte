<script lang="ts">
    import Card, {
        Content,
        PrimaryAction,
        Actions,
        ActionButtons,
        ActionIcons,
    } from "@smui/card";
    import Textfield from "@smui/textfield";
    import Icon from "@smui/textfield/icon";
    import Button, { Label } from "@smui/button";

    export let setActive;
    let clicked = 0;
    let User = [];
    let first_name= "";
    let email= "";
    let phone= "";
    let password= "";
    let re_enter_password= "";

    async function signedup(event) {
        event.preventDefault();

        const signupvalues = { first_name, email, phone, password, re_enter_password };

        const response = await fetch(
            "http://localhost:3001/create/new-profile",
            {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify(signupvalues),
            },
        );

        if (response.ok) {
            const addedPost = await response.json();
            User = [...User, addedPost];
            first_name = "";
            email = "";
            phone = "";
            password = "";
            re_enter_password:"";

        } else {
            /*  */
            console.error("Failed to add post");
        }
    }
</script>

<form on:submit={signedup}>
    <div class="card-display">
        <div class="card-container" style="border: 1px solid black;">
            <Card>
                <Content>
                    <div class="columns margins">
                        <div>
                            <!-- svelte-ignore a11y-label-has-associated-control -->
                            <label>UserName</label>
                            <Textfield
                                class="shaped-outlined"
                                variant="outlined"
                                bind:value={first_name}
                                label="UserName"
                            ></Textfield>

                            <pre class="status"></pre>
                        </div>
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
                                <Icon class="material-icons" slot="leadingIcon"
                                    >email</Icon
                                ></Textfield
                            >

                            <pre class="status"></pre>
                        </div>
                        <div>
                            <!-- svelte-ignore a11y-label-has-associated-control -->
                            <label>Phone No.</label>
                            <Textfield
                                class="shaped-outlined"
                                variant="outlined"
                                bind:value={phone}
                                label="Phone-Number"
                                type="number"
                            ></Textfield>

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
                                <Icon class="material-icons" slot="leadingIcon"
                                    >password</Icon
                                >
                            </Textfield>

                            <pre class="status"></pre>
                        </div>
                        <div>
                            <!-- svelte-ignore a11y-label-has-associated-control -->
                            <label>Re-Password</label>
                            <Textfield
                                class="shaped-outlined"
                                variant="outlined"
                                bind:value={re_enter_password}
                                label="Re-Enter-Password"
                                type="password"
                            >
                                <Icon class="material-icons" slot="leadingIcon"
                                    >password</Icon
                                >
                            </Textfield>

                            <pre class="status"></pre>
                        </div>
                    </div>
                </Content>
                <Actions>
                    <Button type="submit" on:click={() => clicked++}>
                        <Label>Sign-Up</Label>
                    </Button>
                    {#each ["Login"] as tab}
                        <Button on:click={() => setActive(tab)}
                            ><Label>{tab}</Label></Button
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
    *
        :global(
            .shaped-outlined .mdc-notched-outline .mdc-notched-outline__notch
        ) {
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
        margin-right: 32px;
    }
</style>
