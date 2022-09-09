# Welcome to [Astro](https://astro.build)

This example tries to use client javascript served from a NPM dependency.

In `Layout.astro` the client javascript library is included like:

```
	<body>
		<slot />
		<script>
      import 'aos/dist/aos.js'

			(function() {
        AOS.init({
          duration: 650,
          once: true
        })
			})()
		</script>
	</body>
```

But in the browser it fails with:

`Uncaught ReferenceError: AOS is not defined`

Looking at the hoisted code referenced in the generated HTML as:

`<script type="module" src="/Users/marceloverdijk/workspace/astro-npm-js/src/layouts/Layout.astro?astro&type=script&index=0&lang.ts"></script>`

I can see the orginal imported `aos.js` has been "transformed" 
and it exports something like:

```
var aos_dist_aos_js_default = require_aos();
export {
  aos_dist_aos_js_default as default
};
```

but not AOS anymore, hence the `AOS is not defined` error.

