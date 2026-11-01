# PhishGuard Hack-O-Week — Week 13-14 Code Examples

Code is kept outside the Word report. Each section identifies whether it is copied from the application or is an educational example.

## Parent-owned history and prop flow

**Source:** `frontend/src/App.jsx`

```
const [history, setHistory] = useState(() => getHistory())
const [scanRequest, setScanRequest] = useState(null)
const syncHistory = useCallback(
  (nextHistory) => setHistory(nextHistory), []
)

<URLScanner onNewResult={syncHistory} scanRequest={scanRequest} />
<ScanHistory history={history}
  onClear={() => setHistory(clearHistory())}
  onRescan={handleRescan} />
```

Actual implementation. App owns shared state and passes it to children through props. This is simple state lifting, not Context API.

## Local scan state

**Source:** `frontend/src/components/URLScanner.jsx`

```
const [url, setUrl] = useState('')
const [loading, setLoading] = useState(false)
const [error, setError] = useState('')
const [result, setResult] = useState(null)
const [showDemos, setShowDemos] = useState(false)
```

Actual implementation. State that serves only the scanner stays inside URLScanner; history is shared at App level.

## Actual styling tokens

**Source:** `frontend/src/index.css`

```
@import "tailwindcss";

:root {
  --surface-0: #0d1117;
  --surface-1: #121821;
  --text: #e5eaf0;
  --cyan: #55c9d8;
}
body { background: var(--surface-0); color: var(--text); }
```

Actual CSS variables and Tailwind import. The application uses regular global CSS as its primary styling. Tailwind is configured, but CSS Modules and styled-components are absent.

## Context and styling alternatives

**Source:** `Educational example (not in PhishGuard)`

```
const ScanContext = createContext(null)
function AppProviders({ children }) {
  return <ScanContext.Provider value={{ history, addScan }}>
    {children}
  </ScanContext.Provider>
}

// CSS Module: import styles from './Panel.module.css'
// Tailwind: <section className="rounded-lg p-4">
// styled-components: const Panel = styled.section`padding: 1rem;`
```

Educational comparison. Context and the three style syntax examples illustrate assignment approaches; they are not implemented in PhishGuard.
