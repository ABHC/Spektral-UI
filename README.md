# Spektral UI

A Svelte 5 design system. 
Customisable, composable and accessible. WCAG-focused and theme driven. 

[Documentation](#) · [npm](#)

## Install

```bash
npm install @spektral/ui
```

## Quick start

```svelte
<script>
  import { Button, Card, Badge } from '@spektral/ui';
</script>

<Card>
  <Badge>New</Badge>
  <Button palette="accent">Get started</Button>
</Card>
```

Import the tokens once, in your app entry:

```ts
import '@spektral/ui/tokens.css';
```

## What's inside

- 35+ components: Accordion, Alert, Avatar, Badge, Button, Callout, Card, Checkbox, CodeBlock, ColorPicker, Command, DataTable, Drawer, Explorer, Footer, Header, Headline, Hero, Input, ListItem, Marquee, Modal, Nav, Popover, Progress, RadioGroup, SearchField, Select, Selector, Slider, Switch, Textarea, TileGrid, Timeline, Tooltip.
- A token system (`tokens.css`) with palettes, tones, typography, radii, shadows.
- Light/dark support out of the box.
- Use the theme export system to emit a custom token file to replace the default token.ccs in your project.

## Requirements

- Svelte `^5.0.0`
- Modern browsers (CSS custom properties, `:has`, `color-mix`).

## Documentation

Full docs, component API, live examples, theming guide: **[link to docs site]**.

## License

GPL-3.0 — see [LICENSE](./LICENSE).
