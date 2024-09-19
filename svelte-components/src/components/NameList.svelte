<script>
    const names = [
        {
            firstname: "Bruce",
            lastname: "Wayne",
        },
        {
            firstname: "Clark",
            lastname: "Kent",
        },
        {
            firstname: "Princess",
            lastname: "Diana",
        },
    ];
</script>

{#each names as name (name)}
    <h2>{name.firstname} {name.lastname}</h2>
    <slot name="hero" firstname={name.firstname} lastname={name.lastname}
    ></slot>
{/each}
