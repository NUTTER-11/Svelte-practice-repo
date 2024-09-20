<script>
    import { onMount } from "svelte";
    let posts = [];
    let title = "";
    let body = "";
    let userId = "";
    let id =""
 

    onMount(async () => {
        await fetchPosts();
    });

    async function fetchPosts() {
        const response = await fetch(
            "https://jsonplaceholder.typicode.com/posts",
        );
        posts = await response.json();
    }

    async function submitPost(event) {
        event.preventDefault();

        const newPost = { userId, title, body ,id };

        const response = await fetch(
            "https://jsonplaceholder.typicode.com/posts",
            {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify(newPost),
            },
        );

        if (response.ok) {
            const addedPost = await response.json();
            posts = [...posts, addedPost];
            title = "";
            body = "";
            userId="";
            id="";
        } else {/*  */
            console.error("Failed to add post");
        }
    }
</script>

<form on:submit={submitPost}>
    <input type="number" bind:value={userId} placeholder="User ID" />
    <input type="number" bind:value={id} placeholder="id" />
    <input type="text" bind:value={title} placeholder="Title" required />
    <textarea bind:value={body} placeholder="Body" required></textarea>
    <button type="submit">Post</button>
</form>

<!-- Display the posts -->
{#each posts as post (post.id)}
    <h3>{post.userId} {post.title}</h3>
    <p>{post.body}</p>
    <hr />
{:else}
    <p>Loading...</p>
{/each}
