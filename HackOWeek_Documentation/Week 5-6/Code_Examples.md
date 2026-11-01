# PhishGuard Hack-O-Week — Week 5-6 Code Examples

Code is kept outside the Word report. Each section identifies whether it is copied from the application or is an educational example.

## handleSubmit and async analysis

**Source:** `frontend/src/components/URLScanner.jsx`

```
const handleSubmit = (event) => {
  event.preventDefault()
  handleAnalyze(url)
}

const data = await analyzeUrl(trimmed)
setResult(data)
setUrl(trimmed)
onNewResult?.(addToHistory(data))
```

Actual implementation. The handler prevents a page reload, then asynchronous API output updates React state and scan history.

## addToHistory

**Source:** `frontend/src/services/history.js`

```
const entry = {
  id: Date.now(), url: result.url,
  domain: result.domain,
  risk_score: result.risk_score,
  classification: result.classification,
  timestamp: new Date().toISOString(),
}
const updated = [entry, ...history].slice(0, 50)
localStorage.setItem(STORAGE_KEY, JSON.stringify(updated))
```

Actual implementation. Object properties form a record; array spread places the newest record first, and slice caps stored history at 50 entries.

## filteredHistory

**Source:** `frontend/src/components/ScanHistory.jsx`

```
const filteredHistory = useMemo(() => {
  const normalized = query.trim().toLowerCase()
  if (!normalized) return history || []
  return (history || []).filter((entry) =>
    `${entry.url} ${entry.domain}`.toLowerCase().includes(normalized)
  )
}, [history, query])

{filteredHistory.map((entry) => (
  <tr key={`${entry.id}-${entry.timestamp}`}>
```

Actual implementation. The template literal combines searchable fields; filter selects matches, and map turns each record into a table row.

## Array methods, destructuring, and rest

**Source:** `Educational example (not in PhishGuard)`

```
const [latest, ...olderScans] = scans
const highestRisk = scans.reduce(
  (highest, scan) => Math.max(highest, scan.risk_score), 0
)
const firstPhishing = scans.find((scan) => scan.classification === 'Phishing')
const hasHighRisk = scans.some((scan) => scan.risk_score >= 60)
const allHaveUrls = scans.every((scan) => Boolean(scan.url))
```

Educational example. The rest pattern gathers olderScans after destructuring the latest item. reduce, find, some, and every answer different questions about a collection. These operations are not used in current PhishGuard code.
