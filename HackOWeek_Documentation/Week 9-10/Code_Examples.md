# PhishGuard Hack-O-Week — Week 9-10 Code Examples

Code is kept outside the Word report. Each section identifies whether it is copied from the application or is an educational example.

## Controlled field and submit

**Source:** `frontend/src/components/URLScanner.jsx`

```
const [url, setUrl] = useState('')
const handleSubmit = (event) => {
  event.preventDefault()
  handleAnalyze(url)
}

<form onSubmit={handleSubmit} noValidate>
  <label htmlFor="url-input">URL to inspect</label>
  <input id="url-input" value={url}
    onChange={(event) => setUrl(event.target.value)} />
  <button type="submit" disabled={loading}>Analyze URL</button>
</form>
```

Actual implementation. React state is the input value; form submission uses the event handler and the button reflects loading state.

## Validation and result state

**Source:** `frontend/src/components/URLScanner.jsx`

```
const trimmed = (targetUrl ?? '').trim()
if (!trimmed) {
  setError('Enter a URL to analyze.')
  inputRef.current?.focus()
  return
}
const parsedUrl = new URL(trimmed)
const data = await analyzeUrl(trimmed)
setResult(data)
onNewResult?.(addToHistory(data))
```

Actual implementation. Invalid/empty values stop before the request. A valid response updates local result state and notifies the parent of history changes.

## Parent state and component composition

**Source:** `frontend/src/App.jsx`

```
const [history, setHistory] = useState(() => getHistory())
const syncHistory = useCallback(
  (nextHistory) => setHistory(nextHistory), []
)

<URLScanner onNewResult={syncHistory} scanRequest={scanRequest} />
<ScanHistory history={history}
  onClear={() => setHistory(clearHistory())}
  onRescan={handleRescan} />
```

Actual implementation. App owns history shared by the scanner and history display; callbacks let children request parent-owned updates.
