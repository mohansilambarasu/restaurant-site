# Restro NYC — Restaurant Site

A fictional Italian-American restaurant website. Built as a host site to 
demonstrate the menu-admin SDK integration.

## Live Demo

https://mohansilambarasu.github.io/restaurant-site/

## SDK Integration

The menu admin SDK is embedded via npm CDN — no build tool, no install:

```html
<script src="https://unpkg.com/@mohansilambu/menu-admin@0.0.2/dist/menu-admin.umd.js"></script>

<div id="external-menu"></div>

<script>
  const instance = MenuAdmin.createMenuAdmin(
    document.getElementById("external-menu"),
    { theme: "light" }
  );
</script>
```

## Style Isolation

The requirement was that the SDK's styles must not leak into the host site, 
and the host site's styles must not break the SDK.

The SDK uses Shadow DOM — the browser's built-in isolation boundary. All SDK 
styles are injected inside the shadow root, not the host document. This means:

- This site's global styles (`h1`, `label`, `input`, `body` resets) have zero 
  effect on the SDK's form and card components
- The SDK's `.menu-form`, `.menu-card` styles are invisible to this site

You can verify this in DevTools — find `#external-menu` in the Elements panel 
and expand it. You'll see `#shadow-root (open)` containing its own `<style>` 
tag completely separate from the host document's styles.

## Related

- SDK repo: https://github.com/mohansilambarasu/menu-admin-sdk
- npm package: https://www.npmjs.com/package/@mohansilambu/menu-admin
