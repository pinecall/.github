<p align="center">
  <a href="https://github.com/pinecall/pinecall">
    <img src="assets/banner.svg" alt="Pinecall: voice and chat agents, written as a class" width="100%">
  </a>
</p>

<p align="center">
  <a href="https://docs.pinecall.io/start/quickstart/"><b>Quickstart</b></a> ·
  <a href="https://docs.pinecall.io">Docs</a> ·
  <a href="https://github.com/pinecall/pinecall">Source</a> ·
  <a href="https://cloud.pinecall.io/sandbox/">Console</a> ·
  <a href="https://pinecall.io">pinecall.io</a>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/pinecall"><img alt="npm" src="https://img.shields.io/npm/v/pinecall?label=cli&color=5eead4&style=for-the-badge&labelColor=0d1117&logo=npm"></a>
  <a href="https://pypi.org/project/pinecall-runtime/"><img alt="pypi" src="https://img.shields.io/pypi/v/pinecall-runtime?label=runtime&color=5eead4&style=for-the-badge&labelColor=0d1117&logo=python&logoColor=white"></a>
  <a href="https://github.com/pinecall/pinecall/tags"><img alt="release" src="https://img.shields.io/github/v/tag/pinecall/pinecall?label=release&color=9184d9&style=for-the-badge&labelColor=0d1117"></a>
</p>

<br>

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/how-it-works-dark.png">
    <img src="assets/how-it-works-light.png" alt="Phone, browser, chat and WhatsApp reach the Pinecall runtime; its worker runs speech to text, the model and text to speech, its gateway asks your agent.tsx to run a tool, and every step is an entry in the call's log" width="100%">
  </picture>
</p>

**You write the agent as a class. Pinecall answers the phone.** The class's fields are the call's
state, its `@tool` methods are what the model may do, and `render()` is the prompt. Pinecall runs
the rest: the phone line, the browser call, WhatsApp, speech in and out, memory, retrieval, judges
at hang-up, the console and the bill. You can write the agent in TypeScript, Python or Ruby.

**Many orgs, one runtime.** Each business is an org with its own people, keys, numbers, quotas and
data, kept apart down to Postgres row-level security. Each org writes its own agents, and their
code runs in the org's own process, never inside the runtime, so one fleet of workers serves them
all. The runtime is open source: run it on your machine with `pinecall-runtime local up`, or use
Pinecall Cloud.

```tsx
export default class FrontDesk extends Agent {
  stage: Stages<"ask" | "done"> = "ask";

  /** Writes down the caller's message, once they have said their name and what it is about. */
  @tool({ stage: "ask", pii: ["name"] })
  async takeMessage(name: string, about: string) {
    this.stage = "done";
    return { name, about };
  }
}
```

```console
$ pinecall-runtime local up          # the runtime on your machine, or skip it and use Cloud
$ npm i -g pinecall && pinecall new acme --agent front-desk
$ pinecall chat                      # talk to it
$ pinecall test                      # its goldens, judged against a real model
$ pinecall deploy up                 # it answers calls
```

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/architecture-dark.svg">
    <img src="assets/architecture-light.svg" alt="How a call moves through Pinecall" width="100%">
  </picture>
</p>

| | |
|---|---|
| [**pinecall/pinecall**](https://github.com/pinecall/pinecall) | the runtime, the CLI and its MCP server, the console, the widget, and the SDKs for TypeScript, Python and Ruby, all released at one version |
| [**docs.pinecall.io**](https://docs.pinecall.io) | the quickstart, the class, testing, the phone, self-hosting, and a page for every CLI verb |
| [**cloud.pinecall.io**](https://cloud.pinecall.io/sandbox/) | Pinecall Cloud: a sandbox to try an agent where nothing reaches a real caller |

<p align="center">
  <sub><code>$ pinecall --help</code></sub>
</p>
