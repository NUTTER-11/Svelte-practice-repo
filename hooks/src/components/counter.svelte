<script context="module">
    let totalcount = 0;
    export function getTotalcount() {
        return totalcount;
    }
</script>

<script>
    let count = 0;
    function clickhandler() {
        count += 1;
        totalcount += 1;
    }
</script>

<h2>count ={count}</h2>
<button on:click={clickhandler}>increment</button>
