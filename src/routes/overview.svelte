<script context="module">
    export async function preload({ params }, { token }) {
        if (!token) {
            this.redirect(302, `/login`);
        }
    }
</script>
<script>
    import {post} from "utils.js";

    async function getMyData()
    {
        return await post('auth/getMyData');
    }
</script>
{#if process.browser}
    {#await getMyData()}
        loading...
    {:then my}
        <p>{my.name}</p>
        <!--<pre>{JSON.stringify(my, null, 4)}</pre>-->
    {/await}
{/if}