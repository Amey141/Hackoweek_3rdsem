# PhishGuard Hack-O-Week — Week 15-16 Code Examples

Code is kept outside the Word report. Each section identifies whether it is copied from the application or is an educational example.

## Actual FastAPI request/response route

**Source:** `backend/app/main.py`

```
@app.post("/api/analyze", response_model=AnalysisResponse)
def analyze_url(request: URLRequest):
    try:
        result = URLAnalyzer.analyze(request.url)
        return result
    except ValueError as exc:
        raise HTTPException(
            status_code=422, detail=str(exc)
        ) from exc
    except Exception as exc:
        raise HTTPException(
            status_code=500, detail="Internal analysis error."
        ) from exc
```

Actual application code in Python. FastAPI validates the request model, calls the analyzer, then serializes the response or maps the exception to an HTTP status.

## Node built-ins, raw HTTP, and CommonJS

**Source:** `Educational example (not in PhishGuard)`

```
const fs = require('node:fs')
const path = require('node:path')
const http = require('node:http')
const port = Number(process.env.PORT) || 8000
const configPath = path.join(process.cwd(), 'config.json')
const hasConfig = fs.existsSync(configPath)
const server = http.createServer((req, res) => {
  if (req.method === 'POST' && req.url === '/api/analyze') {
    res.writeHead(200, { 'content-type': 'application/json' })
    res.end(JSON.stringify({ classification: 'Suspicious', risk_score: 45 }))
    return
  }
  res.writeHead(404); res.end('Not found')
})
server.listen(port)
module.exports = server
```

Educational Node.js example. require and module.exports show CommonJS. fs checks for a file; path builds a platform-specific path; process reads PORT; and http creates and starts a request/response server. These modules are not used by the PhishGuard backend.

## Express route, middleware, and error handler

**Source:** `Educational example (not in PhishGuard)`

```
const express = require('express')
const app = express()
app.use(express.json())
app.post('/api/analyze', (req, res, next) => {
  try {
    const result = analyzeUrl(req.body.url)
    res.json(result)
  } catch (error) { next(error) }
})
app.use((error, req, res, next) => {
  res.status(400).json({ detail: error.message })
})
```

Educational Express example. JSON middleware parses request data, the route handles the endpoint, and error middleware converts thrown errors into a response.

## Actual frontend package list

**Source:** `frontend/package.json`

```
"scripts": {
  "dev": "vite",
  "build": "vite build",
  "lint": "oxlint",
  "preview": "vite preview"
},
"dependencies": {
  "react": "^19.3.1",
  "react-dom": "^19.3.1"
}
```

Actual frontend NPM configuration. npm run dev/build/lint/preview are declared scripts. The Python backend packages in requirements.txt are installed through pip.
