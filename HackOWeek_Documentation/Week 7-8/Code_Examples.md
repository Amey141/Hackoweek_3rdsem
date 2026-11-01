# PhishGuard Hack-O-Week — Week 7-8 Code Examples

Code is kept outside the Word report. Each section identifies whether it is copied from the application or is an educational example.

## analyzeUrl error handling

**Source:** `frontend/src/services/api.js`

```
if (!response.ok) {
  let detail = 'Analysis failed.'
  try {
    const body = await response.json()
    detail = body.detail || detail
  } catch {
    // Keep the fallback if the response is not JSON.
  }
  throw new Error(detail)
}
return response.json()
```

Actual implementation. HTTP errors become JavaScript Error objects with a server detail or fallback; malformed error bodies do not hide the original failure.

## analyze_url route

**Source:** `backend/app/main.py`

```
try:
    result = URLAnalyzer.analyze(request.url)
    return result
except ValueError as exc:
    raise HTTPException(status_code=422, detail=str(exc)) from exc
except Exception as exc:
    raise HTTPException(
        status_code=500, detail="Internal analysis error."
    ) from exc
```

Actual Python/FastAPI implementation, not JavaScript try/catch. It distinguishes invalid input from unexpected server errors.

## actual scripts and dependencies

**Source:** `frontend/package.json`

```
"scripts": {
  "dev": "vite",
  "build": "vite build",
  "lint": "oxlint",
  "preview": "vite preview"
},
"dependencies": {
  "lucide-react": "^1.60.0",
  "react": "^19.3.1",
  "react-dom": "^19.3.1"
}
```

Actual manifest. npm run dev/build/lint/preview exist; npm test and npm run test do not. npm install installs frontend dependencies from package.json and package-lock.json.

## Custom JavaScript error class

**Source:** `Educational example (not in PhishGuard)`

```
class UrlInputError extends Error {
  constructor(message) {
    super(message)
    this.name = 'UrlInputError'
  }
}

try {
  if (!input.trim()) throw new UrlInputError('Enter a URL.')
} catch (error) {
  showMessage(error.message)
}
```

Educational JavaScript example. The current project uses built-in Error and Python ValueError; it does not define a custom JavaScript error class.
