# How Yet Another Svelte Modal is different from all the others
1. Modals are always rendered in the div near the root of your app. This allows you not to think if some of the parents of your component have a relativish position.
2. Modals can show modals, can show modals.
3. Works just fine on mobile in fullscreen mode

[Live Demo](https://yas-modal.netlify.app/)

# How to use
## 1. Install Tailwind CSS.
Here is [how to](https://tailwindcss.com/docs/guides/sveltekit).
## 2. Install svelte-modal
```
npm i -D yas-modal
```

## 3. Fix `tailwind.config.cjs`

Adds tailwind classes from the modal into your app's CSS.

```cjs
/** @type {import('tailwindcss').Config} */
module.exports = {
    content: [
        './src/**/*.{html,js,svelte,ts}',
        require('path').join(require.resolve('yas-modal'), '../**/*.svelte')
  ]
  ...
};
```

## 4. Set up `ModalTarget`
Wrap the slot in your root `+layout.svelte` into the ModalTarget component. This will create a div in the root of your app and set it as a context for all child components as `modal-target`
``` svelte
<script>
    import { ModalTarget } from 'yas-modal'
</script>
<ModalTarget><slot/></ModalTarget>
```
## 5. Use the modal in your svelte component
```svelte
<script>
    import { Modal } from 'yas-modal'
    let show_modal = false;
</script>

<button on:click={()=> show_modal = true}>Click me</button>

{#if show_modal}
    <Modal on:close={() => show_modal = false}>
        <h1 slot="header">Title</h1>
        Modal Content
        <div slot="footer">Footer</div>
    </Modal>
{/if}

```

# License
MIT