# astro-netlify-components

Astro components for Netlify

## Usage

Install with your preferred package manager:

```bash
npm i astro-netlify-components
```

Then import the components into your Astro project:

```astro
---
import { Form } from "astro-netlify-components";
---

<Form name="example">{/* ... */}</Form>
```

## Components

### `CMS`

TODO(@seanmcp)

### `Form`

A helpful type-safe wrapper to create forms with [Netlify Forms](https://docs.netlify.com/forms/setup/). The component:

- Requires a `name` prop to identify the form
- Adds the `data-netlify=true` attribute to the `form` element
- Adds a honeypot field
- Warns if your `action` property does not begin with `/`

```astro
---
import Form from "astro-netlify-components";
---

<Form name="contact">
  <label>
    <b>Name</b>
    <input type="text" name="name" />
  </label>
  <label>
    <b>Email</b>
    <input type="email" name="email" />
  </label>
  <label>
    <b>Message</b>
    <textarea name="message"></textarea>
  </label>
  <button>Send</button>
</Form>
```

#### Props

```ts
export interface Props extends HTMLAttributes<"form"> {
  /** WARNING: If you set to false, then your Netlify form will not function. */
  "data-netlify"?: boolean;
  name: string;
}
```

`name` is the only required prop, and is used by Netlify to identify the form.

If you pass an `action` prop that does not start with a `/`, then the component will throw an error. [Read Netlify's docs about success redirects](https://docs.netlify.com/forms/setup/#success-messages).
