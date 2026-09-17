# Icon Reference: Linear/Notion-style Line Icons

Stroke-based, `currentColor`, 20x20 viewBox, `stroke-width="1.5"`,
`stroke-linecap="round"`, `stroke-linejoin="round"`, `fill="none"`. Paste the
`<svg>...</svg>` directly into the Vue template where an icon is needed
(inline, not as separate .svg files, so `currentColor` picks up the
surrounding text/accent color automatically).

## dashboard / home
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M8.5 3H4a1 1 0 0 0-1 1v4.5a1 1 0 0 0 1 1h4.5a1 1 0 0 0 1-1V4a1 1 0 0 0-1-1Z"/>
  <path d="M16 3h-4.5a1 1 0 0 0-1 1v4.5a1 1 0 0 0 1 1H16a1 1 0 0 0 1-1V4a1 1 0 0 0-1-1Z"/>
  <path d="M8.5 12.5H4a1 1 0 0 0-1 1V16a1 1 0 0 0 1 1h4.5a1 1 0 0 0 1-1v-2.5a1 1 0 0 0-1-1Z"/>
  <path d="M16 12.5h-4.5a1 1 0 0 0-1 1V16a1 1 0 0 0 1 1H16a1 1 0 0 0 1-1v-2.5a1 1 0 0 0-1-1Z"/>
</svg>
```

## inventory / box
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M10 2.5 3 6v8l7 3.5 7-3.5V6l-7-3.5Z"/>
  <path d="M3 6l7 3.5 7-3.5"/>
  <path d="M10 9.5V17"/>
</svg>
```

## orders / cart
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M3 4h1.5l1.2 8.4a1.5 1.5 0 0 0 1.5 1.3h6.4a1.5 1.5 0 0 0 1.5-1.2l1-5.5H5"/>
  <circle cx="8" cy="17" r="1"/>
  <circle cx="14" cy="17" r="1"/>
</svg>
```

## analytics / reports / chart
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M3 17V3"/>
  <path d="M3 17h14"/>
  <path d="M6.5 14v-4"/>
  <path d="M10.5 14V7"/>
  <path d="M14.5 14v-6.5"/>
</svg>
```

## finance / dollar
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M10 2.5v15"/>
  <path d="M13.5 5.75c0-1.24-1.57-2.25-3.5-2.25S6.5 4.5 6.5 5.75s1.57 2 3.5 2.5 3.5 1.26 3.5 2.5-1.57 2.25-3.5 2.25-3.5-1.01-3.5-2.25"/>
</svg>
```

## users / team
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <circle cx="7" cy="6.5" r="2.5"/>
  <path d="M2.5 16.5c0-2.5 2-4.5 4.5-4.5s4.5 2 4.5 4.5"/>
  <circle cx="14.5" cy="7" r="2"/>
  <path d="M12.8 12.2c1.9.4 3.2 2 3.2 4.3"/>
</svg>
```

## settings / gear
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <circle cx="10" cy="10" r="2.5"/>
  <path d="M10 3v1.6M10 15.4V17M17 10h-1.6M4.6 10H3M14.9 5.1l-1.1 1.1M6.2 13.7l-1.1 1.1M14.9 14.9l-1.1-1.1M6.2 6.2 5.1 5.1"/>
</svg>
```

## calendar
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <rect x="3" y="4.5" width="14" height="12" rx="1.5"/>
  <path d="M3 8h14"/>
  <path d="M7 2.5v3M13 2.5v3"/>
</svg>
```

## search
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <circle cx="8.5" cy="8.5" r="5"/>
  <path d="M16 16l-3.8-3.8"/>
</svg>
```

## notifications / bell
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M5 8a5 5 0 0 1 10 0c0 3.5 1 4.5 1 4.5H4s1-1 1-4.5Z"/>
  <path d="M8.3 15a1.7 1.7 0 0 0 3.4 0"/>
</svg>
```

## mail
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <rect x="2.5" y="4.5" width="15" height="11" rx="1.5"/>
  <path d="M3 5.5l7 5.5 7-5.5"/>
</svg>
```

## documents / file
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M6 2.5h5.5L15 6v11a1 1 0 0 1-1 1H6a1 1 0 0 1-1-1V3.5a1 1 0 0 1 1-1Z"/>
  <path d="M11.5 2.5V6H15"/>
</svg>
```

## tags / labels
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M10.5 3H4a1 1 0 0 0-1 1v6.5a1 1 0 0 0 .3.7l6.5 6.5a1 1 0 0 0 1.4 0l6-6a1 1 0 0 0 0-1.4L10.5 3Z"/>
  <circle cx="7" cy="7" r="1.25"/>
</svg>
```

## shipping / truck
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <rect x="2" y="6" width="9" height="7" rx="1"/>
  <path d="M11 8.5h3.5L17 11v2a1 1 0 0 1-1 1h-1"/>
  <circle cx="6" cy="15" r="1.5"/>
  <circle cx="13.5" cy="15" r="1.5"/>
</svg>
```

## layers
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M10 2.5 3 6.5l7 4 7-4-7-4Z"/>
  <path d="M3 10.5l7 4 7-4"/>
  <path d="M3 14.5l7 4 7-4"/>
</svg>
```

## folder
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M2.5 5.5a1 1 0 0 1 1-1H8l1.5 2H16a1 1 0 0 1 1 1v7a1 1 0 0 1-1 1H3.5a1 1 0 0 1-1-1v-9Z"/>
</svg>
```

## list / table
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M3 5.5h14M3 10h14M3 14.5h14"/>
</svg>
```

## grid
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <rect x="3" y="3" width="6" height="6" rx="1"/>
  <rect x="11" y="3" width="6" height="6" rx="1"/>
  <rect x="3" y="11" width="6" height="6" rx="1"/>
  <rect x="11" y="11" width="6" height="6" rx="1"/>
</svg>
```

## add / plus
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M10 4v12M4 10h12"/>
</svg>
```

## logout
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M8 3H4.5a1 1 0 0 0-1 1v12a1 1 0 0 0 1 1H8"/>
  <path d="M13 13.5 17 10l-4-3.5"/>
  <path d="M17 10H8"/>
</svg>
```

## user / profile
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <circle cx="10" cy="7" r="3"/>
  <path d="M3.5 17c0-3.6 2.9-6 6.5-6s6.5 2.4 6.5 6"/>
</svg>
```

## globe / language
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <circle cx="10" cy="10" r="7"/>
  <path d="M3 10h14"/>
  <path d="M10 3c2 2.2 3 4.4 3 7s-1 4.8-3 7c-2-2.2-3-4.4-3-7s1-4.8 3-7Z"/>
</svg>
```

## fallback / generic (dot-bookmark)
```html
<svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M5.5 3.5h9a1 1 0 0 1 1 1V17l-5.5-3-5.5 3V4.5a1 1 0 0 1 1-1Z"/>
</svg>
```
