---
description: >-
  Common issues you would find working with TypeScript, Next.js and how to solve
  them.
---

# 🔎 Troubleshooting Issues

## TypeScript shows file not found error in tsconfig.json

Situation: You move or rename a TypeScript file inside VS Code and immediately `tsconfig.json` shows an error 'File xyz.tsx not found.\`

Rootcause: This happens because TypeScript server did not record the move/rename operation.&#x20;

Solution: This is a known issue being discussed in this PR [https://github.com/microsoft/TypeScript/issues/43838](https://github.com/microsoft/TypeScript/issues/43838) and the correct solution is not available (as of Feb 2024). But there is a workaround - restart the TypeScript server.&#x20;

* In VS Code, open command pallette `Ctrl+Shift+p` and choose the command `Typescript: Restart TS Server`).
