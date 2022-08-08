# Vite - Vue plugin: custom element props get removed when remounted in production build

Reproduction for custom element props that get removed when a component gets remounted in a production build.

I have a custom element `test-component` with a `value` prop defined which I want to use in a Vue template like this: `<test-component value="input A"></test-component>`. Vue sees that it has a `value` prop, so it sets this instead of an attribute. In the dev tools, you can see it didn't set an attribute, but the property directly. This works as expected. However, if it gets unmounted by rendering something else and then gets remounted, the prop will not be set. This only happens in the production build (`npm run build` + `npm run preview`), and not with the dev server (`npm run dev`). 

This is not an issue if the property of the custom element gets reflected back to an attribute. But this is not always the case, for example with props that could change a lot, like `value`.

It's also not an issue when using a ref as a value for the prop.

I have found a workaround by using a unique `key` for each custom element like this: `<test-component value="input A" :key="input-a"></test-component>`, but this is far from optimal DX in my opinion.
