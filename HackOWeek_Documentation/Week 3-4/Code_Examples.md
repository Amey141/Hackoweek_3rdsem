# PhishGuard Hack-O-Week — Week 3-4 Code Examples

Code is kept outside the Word report. Each section identifies whether it is copied from the application or is an educational example.

## URLScanner form

**Source:** `frontend/src/components/URLScanner.jsx`

```
<section id="scanner" aria-labelledby="scanner-title">
  <h1 id="scanner-title">URL Security Analysis</h1>
  <form className="scanner-form" onSubmit={handleSubmit} noValidate>
    <label htmlFor="url-input">URL to inspect</label>
    <input id="url-input" value={url}
      onChange={(event) => setUrl(event.target.value)}
      aria-describedby={error ? 'scan-error' : 'scanner-help'}
      aria-invalid={Boolean(error)} />
    <button type="submit" disabled={loading}>Analyze URL</button>
  </form>
</section>
```

Actual implementation. The label is connected to the input, the submit event is handled by the form, and error/help text is referenced for assistive technology.

## URL entry and result layout

**Source:** `frontend/src/index.css`

```
.url-entry {
  display: flex;
  align-items: center;
  gap: 10px;
}
.result-grid {
  display: grid;
  grid-template-columns: minmax(0, 1.45fr) minmax(240px, .8fr);
  gap: 14px;
}
@media (max-width: 900px) {
  .result-grid { grid-template-columns: minmax(0, 1fr); }
}
```

Actual CSS. Flexbox aligns the input controls, while Grid gives the diagnostic and detail panels separate columns on wide screens and one column on compact screens.

## CSS tokens and focus treatment

**Source:** `frontend/src/index.css`

```
:root {
  --surface-0: #0d1117;
  --text: #e5eaf0;
  --cyan: #55c9d8;
  --red: #e17878;
  --mono: 'IBM Plex Mono', Consolas, monospace;
}
button:focus-visible, a:focus-visible,
input:focus-visible {
  outline: 2px solid var(--cyan);
  outline-offset: 3px;
}
```

Actual CSS. Variables centralize repeated theme values, and :focus-visible makes keyboard focus visible. The stylesheet also includes screen-reader-only text, table scopes, and reduced-motion handling.
