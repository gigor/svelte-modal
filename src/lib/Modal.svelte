<script context="module">
    let modals = [];
</script>

<script>
    import { createEventDispatcher, getContext, onMount } from 'svelte';
    import { fly } from 'svelte/transition';

    let get_modal_target = getContext('modal_target')
    
    /** @type {HTMLElement}*/
    let modal_target;
    /** @type {HTMLElement}*/
    let modal_content;
    let layer = modals.length;
    let dispatch = createEventDispatcher();

    onMount(() => {
        modal_target = get_modal_target();

        if (!modal_target) {
            console.error('yas-modal: Parrent Component is not wrapped into modal target');
        }

        modal_content.classList.add(`layer-${layer}`);
        modals = [...modals, modal_content];
        modal_target.appendChild(modal_content);
        document.body.classList.add('has_modal');

        console.log(modals.length, layer, modals.length - 1 == layer);
        return () => {
            modals = modals.filter((m) => m !== modal_content);

            if (modal_target && modal_target.querySelector(`.layer-${layer}`)) {
                modal_target.removeChild(modal_target.querySelector(`.layer-${layer}`));
            }

            if (!modals.length) {
                document.body.classList.remove('has-modal');
            }
        }
    });

    function handle_close(e) {
        if (layer >= modals.length - 1 && e.target == e.currentTarget) {
            dispatch('close');
        }
    }


</script>

<div
    class="bg-black/5 w-full h-full absolute dark:bg-black/10"
    bind:this={modal_content}
    on:click={handle_close}
    on:keyup={handle_close}
    aria-modal="true"
>
    <button
        on:click={handle_close}
        class="close text-3xl text-white drop-shadow dark:text-slate-400"
    >&times;</button>

    <div
        transition:fly|local={{ y: 100, duration: 200 }}
        class="
            modal        
            w-full max-w-xl
            absolute bottom-0 left-1/2 -translate-x-1/2

            flex flex-col
            rounded-t-3xl
            bg-white text-gray-900 dark:bg-slate-900 dark:text-slate-200
            
            lg:bottom-auto 
            lg:top-1/2 lg:-translate-y-1/2
            lg:rounded-b-3xl
        "
    >   
        {#if $$slots.header}
            <div class="p-4">
                <slot name="header" />
            </div>
        {/if}
        <div class="p-4 flex-1 overflow-y-auto">
            <slot />
        </div>

        {#if $$slots.footer}
            <div class="p-4">
                <slot name="footer" />
            </div>
        {/if}
    </div>
</div>


<style lang="postcss">
    .modal {
        max-height: calc(100% - 4rem);
        min-height: 30%;
        padding-bottom: env(safe-area-inset-top);
    }

    .close {
        @apply absolute right-3;
        top: max(calc(env(safe-area-inset-top) + 0.5rem), 1rem);
    }
</style>
