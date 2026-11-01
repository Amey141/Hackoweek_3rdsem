# PhishGuard Hack-O-Week — Week 11-12 Code Examples

Code is kept outside the Word report. Each section identifies whether it is copied from the application or is an educational example.

## useRef and useCallback

**Source:** `frontend/src/components/URLScanner.jsx`

```
const inputRef = useRef(null)
const loadingRef = useRef(false)

const handleAnalyze = useCallback(async (targetUrl) => {
  if (loadingRef.current) return
  // Validate, request, and update result state.
}, [onNewResult])

inputRef.current?.focus()
```

Actual implementation. A DOM ref focuses an invalid input. A mutable ref guards duplicate requests without triggering a render.

## useMemo derived list

**Source:** `frontend/src/components/ScanHistory.jsx`

```
const filteredHistory = useMemo(() => {
  const normalized = query.trim().toLowerCase()
  if (!normalized) return history || []
  return (history || []).filter((entry) =>
    `${entry.url} ${entry.domain}`.toLowerCase().includes(normalized)
  )
}, [history, query])
```

Actual implementation. The filtered list is recomputed when history or query changes; memoization is useful if deriving this list becomes costly.

## Custom hook and Context API

**Source:** `Educational example (not in PhishGuard)`

```
function useScanHistory() {
  const [scans, setScans] = useState([])
  const addScan = useCallback((scan) => {
    setScans((current) => [scan, ...current])
  }, [])
  return { scans, addScan }
}
const ScanContext = createContext(null)
function ScanCount() {
  const { scans } = useContext(ScanContext)
  return <span>{scans.length}</span>
}
```

Educational example. A custom hook groups reusable state logic. useContext reads shared state provided by a context; both patterns are absent from the application.

## Nested routes, parameters, and navigation

**Source:** `Educational example (not in PhishGuard)`

```
<Routes>
  <Route path="/" element={<Layout />}>
    <Route index element={<Dashboard />} />
    <Route path="history" element={<ScanHistoryPage />} />
    <Route path="scan/:scanId" element={<ScanResultPage />} />
  </Route>
</Routes>
const { scanId } = useParams()
const navigate = useNavigate()
```

Educational example requiring React Router, which is not in package.json. The nested routes share Layout; :scanId is a route parameter and navigate changes location.
