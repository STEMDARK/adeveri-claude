# Adeveri for Claude

Adeveri gives Claude the text of Romanian legislation as Monitorul Oficial al României published it, Partea I and Partea I bis, from 1989 to today: laws, ordinances, government decisions, orders, and decisions of the Constitutional Court and the High Court. It knows which text is in force on a given day, and every rule in an answer links to its passage on the printed page.

## What it does

- Searches the law in force today, or everything ever published, repealed texts included.
- Reads an act as it stands today or as it stood on a given day, and the history of an article.
- Shows the cited passages on their printed pages, inside the conversation.
- Where available, looks up the case files of Romanian courts.

The `romanian-law` skill tells the assistant how to search, state the law in force and cite it.

## Connecting

The plugin connects to the Adeveri MCP server at `https://adeveri.com/mcp`. The first time, sign in with an Adeveri account or choose **Continue without an account**, which asks for no name and no email address. [How to connect](https://adeveri.com/en/connect)

## What it sends

The plugin runs nothing on your device. The assistant sends the Adeveri server the searches it makes and the acts, articles and dates it reads for you, and any feedback it sends through `send_feedback`, which carries no identifier of yours. The [Privacy Policy](https://adeveri.com/en/privacy) says what the server records and for how long.

## Before relying on an answer

The texts are rebuilt from each issue of Monitorul Oficial and can lag behind the latest one. Check a text on its printed page before relying on it.

## Links

[Website](https://adeveri.com/en) · [Privacy Policy](https://adeveri.com/en/privacy) · [Terms](https://adeveri.com/en/terms) · [Support](https://adeveri.com/en/contact)

## About this package

Version 0.1.1, built from commit `bc8f9db01933e0395dde48d920e5613a65b85e5f` of Adeveri's source; `BUILD.json` records the hash of every file. This repository is generated: make changes in the source, not here. The MIT license covers only the files of this package, not the Adeveri service or the content it returns.
