<script>
    import ModalTarget from "$lib/ModalTarget.svelte";
    import '../app.css';
</script>

<ModalTarget><slot/></ModalTarget>


<style lang="postcss">
    :global(html){
        background-color: theme(colors.white);
        color: theme(colors.gray.800);
    }

    @media (prefers-color-scheme: dark) {
        :global(html){
            background-color: theme(colors.black);
            color: theme(colors.slate.200);
        }
    }
</style>