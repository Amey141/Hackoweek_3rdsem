PhishGuard Hack-O-Week Documentation

Project description
PhishGuard is a React/Vite frontend with a Python FastAPI backend. It inspects URL text using configurable rules and explains the risk score; it does not visit the submitted destination. Scan history is stored in browser local storage.

Weekly folders and topics
- Week 3-4: HTML5 semantics, forms, accessibility, Flexbox, Grid, responsive design, CSS variables.
- Week 5-6: JavaScript fundamentals, ES modules, array and object methods, scan history.
- Week 7-8: Error handling, Git/GitHub workflow, NPM fundamentals and configured scripts.
- Week 9-10: React events, forms, controlled components, composition, lifting state.
- Week 11-12: React hooks, custom hooks, React Router, routes and navigation.
- Week 13-14: State management, props versus Context API, styling approaches.
- Week 15-16: Node.js, CommonJS, built-in modules, HTTP server, Express, contrasted with FastAPI.

Each weekly folder contains its DOCX report, Code_Examples.md, and screenshots/ folder. The Markdown companion holds the code examples; code blocks are intentionally omitted from the Word reports. The screenshots folder contains two actual editor screenshots for each report, and those images are embedded at the end of the DOCX.

Technologies found in PhishGuard
- Frontend: JavaScript ES modules, React, Vite, Tailwind CSS integration, regular CSS, lucide-react, browser localStorage.
- Backend: Python, FastAPI, Pydantic, Uvicorn, tldextract.
- The root workspace has no Git repository metadata or history. frontend/package.json defines dev, build, lint, and preview; it does not define a test script.

Opening the files
Open each .docx in Microsoft Word or another DOCX-compatible editor. Open Code_Examples.md in VS Code, Notepad, or another text editor to read the code examples.

Screenshot process
Screenshots were captured from the corresponding project source files open in Visual Studio Code. Captions name the actual source paths. Screenshots appear after the explanatory sections at the end of each report. Code text stays in Code_Examples.md, outside the Word file.

Educational examples
Topics absent from the inspected application are clearly labeled in Code_Examples.md. These include array reduce/find/some/every and rest syntax where absent, custom JavaScript errors, React Router, Context API, custom hooks, CSS Modules, styled-components, Node.js fs/path/process modules, a raw Node HTTP server, and Express. GitHub collaboration is described as a workflow; no commits, branches, merges, or pull requests are claimed.
