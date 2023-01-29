<script>
	import Modal from "$lib/Modal.svelte";

    let show_modal = false;
    let show_modal_2 = false;

</script>

<div class="flex justify-center items-center min-h-screen">
    <button on:click={()=>show_modal = true} 
        class="px-6 py-3 text-2xl rounded-lg shadow-lg bg-green-500 text-green-50 hover:bg-green-600 active:translate-y-1 active:shadow transition"
    >
        Tap Me
    </button>
</div>



{#if show_modal}
    <Modal on:close={(()=>show_modal = false)}>
        <h1 slot="header" class="text-2xl">Hello world, I am the fixed header of the modal</h1>
        
        <p class="pb-2">This is the contents of the default slot, it can be a long text or any content passed into the default slot of a modal.</p>
        <p>The header and the footer will be visible, while the content in the modal will be scrollable.</p>

        <svelte:fragment slot="footer">
            <button on:click={()=>show_modal_2 = true} class="block p-4 center">Show Another Modal</button>
        </svelte:fragment>
    </Modal>
{/if}


{#if show_modal_2}
    <Modal on:close={(()=>show_modal_2 = false)}>
        <h1 slot="header" class="text-2xl">hello world</h1>
        <p class="pb-2">I am the second modal rendered on top of the first one.</p>
        <p>I can:</p>
        <svelte:fragment slot="footer">
            <button on:click={()=>show_modal_2 = false} class="block p-4 center">Hide myself</button>
            <button on:click={()=>show_modal = show_modal_2 = false} class="block p-4 center">Hide both modals</button>
        </svelte:fragment>
    </Modal>
{/if}