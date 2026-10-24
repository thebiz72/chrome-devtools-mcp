This repository contains an MCP server and CLI for Chrome DevTools.

# Instructions

- Use only scripts from `package.json` to run commands.
- Use `npm run build` to run tsc and test build.
- Use `npm run test` to build and run tests, run all tests to verify correctness.
- Use `npm run test path-to-test.ts` to build and run a single test file, for example, `npm run test tests/McpContext.test.ts`.
- Use `npm run format` to fix formatting and get linting errors.
- Never modify `third_party/devtools-frontend` except for experimentation: it is a git submodule, a mirror of the actual codebase.

## Base44 sandbox setup

- This is a CLI/MCP server, not a web app — there is no web UI to preview on port 3000.
- The `devtools-frontend` git submodule must be initialized before building: `git submodule update --init --depth 1`.
- `npm ci` runs `scripts/prepare.ts` (via the `prepare` script) which verifies the submodule and patches `@paulirish/trace_engine`.
- Build: `npm run build` (runs `tsc && node scripts/post-build.ts`). Output is in `build/`.
- Run the CLI: `node build/src/bin/chrome-devtools-mcp.js --help`.
- The sandbox compose (`docker-compose.base44.yml`) installs deps, builds, and keeps the container alive so the CLI can be exec'd into.
- Chrome is NOT installed in the sandbox container — only build/CLI-help verification is possible. Browser automation requires a real Chrome installation.

## Rules for TypeScript

- Do not use `any` type.
- Do not use `as` keyword for type casting.
- Do not use `!` operator for type assertion.
- Do not use `// @ts-ignore` comments.
- Do not use `// @ts-nocheck` comments.
- Do not use `// @ts-expect-error` comments.
- Prefer `for..of` instead of `forEach`.
