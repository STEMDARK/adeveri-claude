# Adeveri for Claude

Version **0.1.0**, generated from [`f7e1aa1d5393ba60a164be6bc4bfc36901636c6a`](https://github.com/STEMDARK/legislation-archive/commit/f7e1aa1d5393ba60a164be6bc4bfc36901636c6a).

Searches Romanian legislation and court case files through the hosted Adeveri MCP server, with citations back to the printed official sources. Connect to `https://adeveri.com/mcp` and choose **Continue as guest**; no account, password or verification code is required. Read the returned provisions and verify the cited printed sources before relying on an answer.

This repository is generated. Edit the skills, tool definitions and packaging code in [legislation-archive](https://github.com/STEMDARK/legislation-archive), then run `cargo xtask plugin push claude --version 0.1.0`. The source repository is private; its commit identifier remains recorded here. Do not edit generated files in this repository.

`BUILD.json` records the full source commit, source tree and SHA-256 of every packaged file except itself. Immutable `v0.1.0` tags identify package releases; `submitted/v…` and `published/v…` annotated tags record operator-confirmed directory events and the MCP server commit observed at that time. Pushing a package does not submit or publish it.

The live MCP server at `https://adeveri.com/mcp` is deployed independently. This package's source commit identifies its skills and metadata, not necessarily the server currently answering requests. Run `cargo xtask deploy status` in the source repository to inspect the deployed build.

[Privacy](https://adeveri.com/privacy) · [Terms](https://adeveri.com/terms) · [Support](mailto:contact@adeveri.com)

The MIT license covers only the files distributed in this plugin package; it does not license the private server implementation or third-party content returned by the service.
