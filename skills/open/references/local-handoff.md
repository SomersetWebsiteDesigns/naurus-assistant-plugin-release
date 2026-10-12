# Local source handoff

This section is for Claude Code on the user's computer. Hosted chat uses the private browser upload link in the main skill instead. Do not install or run this helper inside a hosted chat sandbox; these instruction-only hosted ZIPs do not include it.

Run from the installed package root (the directory containing `package.json`), not the customer's project:

```text
npm ci --ignore-scripts
node scripts/open-in-naurus.mjs --source /absolute/path/to/static-export --inspect
node scripts/open-in-naurus.mjs --source /absolute/path/to/static-export --request-id a-stable-import-id --name "My website"
```

The second command is interactive. Show the manifest first; let the user confirm the selected files, workspace and business. Never answer confirmation on their behalf. The helper prints a Naurus sign-in link. Tokens remain in memory and are never pasted into chat, environment variables or project files. It uses a separate reviewed public OAuth client, not Claude's token cache.

No build, dependency installation or script from the selected project runs. Select an already-created static export. The helper does not export a React/Next application. Hidden folders, dependencies, credentials and unrelated file types are excluded; suspected secrets or symbolic links stop the upload. Inspect the selected HTML itself before sharing; automated scanning is not a guarantee it contains no private content.

On timeout, keep the same request ID and use the private status link. Do not repeatedly create imports. Source changes require a new explicit import and never overwrite an existing project. Finish conversion and manual publication in Naurus.
