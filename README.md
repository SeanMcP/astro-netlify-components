# astro-netlify-components

[![npm](https://img.shields.io/npm/v/astro-netlify-components.svg)](https://npmjs.com/package/astro-netlify-components) [![npm](https://img.shields.io/npm/dt/astro-netlify-components.svg)](https://npmjs.com/package/astro-netlify-components)

🌌 Astro components for Netlify

## Usage

Install with your preferred package manager:

```bash
npm i astro-netlify-components
```

Then import the components into your Astro project:

```astro
---
import CMS from "astro-netlify-components/CMS.astro";
import Form from "astro-netlify-components/Form.astro";
import Identity from "astro-netlify-components/Identity.astro";
---
```

## Components

### `CMS`

A full-page component to render the [Netlify CMS](https://www.netlifycms.org/) admin interface. The component:

- Adds the Netlify Identity script to the document `head`
- Adds the Netlify CMS script to the document `body`
- Implements a redirect script based on Netlify Identity and `Astro.url.pathname`
- Exposes "head"/"food" slots for customization
- Fixes jumping cursor issue in WebKit browsers ([netlify/netlify-cms#5092](https://github.com/netlify/netlify-cms/issues/5092))

```astro
---
// src/pages/admin.astro
import CMS from "astro-netlify-components/CMS.astro";
---

<CMS />
```

**Note**: Make sure to [configure your CMS with a `config.yml` file](https://www.netlifycms.org/docs/configuration-options/) in the correct public directory!

#### Slots

The `CMS` component supports the following slots:

- "head": Content rendered in the `<head>` element
- "foot": Content rendered in the `<body>` element, _after_ the CMS script

```astro
<CMS>
  <Fragment slot="head">
    <link rel="icon" href="/favicon.ico" />
    <style>
      /** ... */
    </style>
  </Fragment>
  <script slot="foot">
    // Create custom widget
  </script>
</CMS>
```

### `Form`

A helpful type-safe wrapper to create forms with [Netlify Forms](https://docs.netlify.com/forms/setup/). The component:

- Requires a `name` prop to identify the form
- Adds the `data-netlify=true` attribute to the `form` element
- Adds a honeypot field
- Warns if your `action` property does not begin with `/`

```astro
---
import Form from "astro-netlify-components/Form.astro";
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
  name: string;
}
```

`name` is the only required prop, and is used by Netlify to identify the form.

If you pass an `action` prop that does not start with a `/`, then the component will throw an error. [Read Netlify's docs about success redirects](https://docs.netlify.com/forms/setup/#success-messages).

### `Identity`

A script tag to add to your `document.head` to enable [Netlify Identity](https://docs.netlify.com/visitor-access/identity/). This is used internally by `CMS` ([read more](https://www.netlifycms.org/docs/add-to-your-site/#add-the-netlify-identity-widget)).

```astro
---
import Identity from "astro-netlify-components/Identity.astro";
---

<!DOCTYPE html>
<html>
  <head>
    <Identity />
  </head>
  <body>
    <!-- ... -->
  </body>
</html>

```

## License

[MIT](/LICENSE)
