# Undici Sourcey llms.txt delivery report

Undici is the actively maintained HTTP client that powers Node.js `fetch`. Its documentation website contains versioned guides and a broad API reference, so a compact `llms.txt` gives coding agents a dependable map to the current, canonical documentation without crawling the whole site.

- Target project: the official Node.js [`undici-website`](https://github.com/nodejs/undici-website) repository, pinned at upstream commit `272f5ae6b28b308a3bf2c707e55445a36a3d4de7`.
- Maintainer demand: upstream issue [#10](https://github.com/nodejs/undici-website/issues/10) explicitly requested an `llms.txt` generation option.
- Generation: Sourcey `3.6.5` is pinned exactly and run by `npm run build:llms` after fetching and rendering the real Undici release docs.
- Reproduction: from the pinned source, run `npm ci`, `npm run build:fetch-docs`, `npm run build:html`, and `npm run build:llms`; outputs are `out/llms.txt` and `out/llms-full.txt`.
- Generation proof: [`scripts/build-llms.mjs`](https://github.com/centwright/undici-website/blob/f1f7ea3baa92ebffe13970ebcbe3aecc5201c9a6/scripts/build-llms.mjs) executes the installed Sourcey CLI against [`sourcey.config.ts`](https://github.com/centwright/undici-website/blob/f1f7ea3baa92ebffe13970ebcbe3aecc5201c9a6/sourcey.config.ts); the delivered index was generated, not hand-written.
- Route accuracy: the post-processing step deterministically maps Sourcey's lowercase Markdown filenames back to doc-kit's real case-sensitive routes such as `Agent`, `Fetch`, and `WebSocket`.
- Public artifact: the generated [`llms.txt`](https://raw.githubusercontent.com/centwright/undici-website/bounty-evidence/llms.txt) is hosted in the public GitHub fork that contains the upstream contribution branch.
- Adoption attempt: upstream pull request [nodejs/undici-website#18](https://github.com/nodejs/undici-website/pull/18) is open and gives maintainers the pinned dependency, build command, configuration, and rationale.
- Governed validation: `runx --version` returned `runx-cli 0.7.0`; the validation run sealed receipt `runx:receipt:sha256:0d68645e7d663d7d95dd11ec12b3938b315c04ecfa7abb4184c9a7689ffec509`.

## Live-entry audit

- `https://undici-website.vercel.app/` returned HTTP 200.
- `https://undici-website.vercel.app/getting-started.html` returned HTTP 200 and resolved to `/getting-started`.
- `https://undici-website.vercel.app/best-practices/undici-vs-builtin-fetch.html` returned HTTP 200.
- `https://undici-website.vercel.app/api/Agent.html` returned HTTP 200 and resolved to the case-sensitive `/api/Agent` route.
- `https://undici-website.vercel.app/api/Fetch.html` returned HTTP 200 and resolved to the case-sensitive `/api/Fetch` route.
- `https://undici-website.vercel.app/api/WebSocket.html` returned HTTP 200 and resolved to the case-sensitive `/api/WebSocket` route.

All six spot checks were made against the live official Undici documentation site on 2026-07-13. The generated file contains 48 curated entries drawn from the latest fetched Undici release documentation.
