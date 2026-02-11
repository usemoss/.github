# Moss

**The real-time search runtime for AI agents.**

If you've built a voice agent, copilot, or any AI that needs to retrieve context on the fly, then you've felt the lag. Every query hops through networks and cloud databases, adding hundreds of milliseconds. The illusion of conversation breaks.

Moss fixes that. We collapse the retrieval stack into a single runtime, built in Rust and WebAssembly, that runs wherever your agent runs. Browser, edge, on-device, or cloud. Sub-10ms lookups, zero network hops.

---

### Quickstart

#### TypeScript

```bash
npm install @inferedge/moss
```

```typescript
import { MossClient, DocumentInfo } from '@inferedge/moss'

const client = new MossClient(process.env.MOSS_PROJECT_ID!, process.env.MOSS_PROJECT_KEY!)

const documents: DocumentInfo[] = [
  { id: 'doc1', text: 'How do I track my order? Log into your account.', metadata: { category: 'shipping' } },
  { id: 'doc2', text: 'What is your return policy? 30-day returns on most items.', metadata: { category: 'returns' } },
]

await client.createIndex('faqs', documents, 'moss-minilm')
await client.loadIndex('faqs')

const results = await client.query('faqs', 'How do I return a damaged product?', 3)
console.log(results.docs[0]) // <10ms, zero network hops
```

#### Python

```bash
pip install inferedge-moss
```

```python
import os, asyncio
from inferedge_moss import MossClient, DocumentInfo

client = MossClient(os.getenv("MOSS_PROJECT_ID"), os.getenv("MOSS_PROJECT_KEY"))

documents = [
    DocumentInfo(id="doc1", text="How do I track my order? Log into your account.", metadata={"category": "shipping"}),
    DocumentInfo(id="doc2", text="What is your return policy? 30-day returns on most items.", metadata={"category": "returns"}),
]

async def main():
    await client.create_index("faqs", documents, "moss-minilm")
    await client.load_index("faqs")

    results = await client.query("faqs", "How do I return a damaged product?", top_k=3)
    print(results.docs[0])  # <10ms, zero network hops

asyncio.run(main())
```

---

### Why Moss

AI interfaces are changing. Voice agents, copilots, multimodal apps - they all share the same hard requirement: retrieval must happen at the speed of thought.

But today's search stacks weren't built for this. They're cloud-first, latency-heavy, and painful to scale for real-time use. Every round-trip to a vector database adds delay your users can feel.

Moss puts semantic search in the same runtime as your agent. No separate service to deploy. No network hop. The index lives right next to your application, and lookups happen in under 10ms.

---

### What teams build with Moss

Voice AI agents that can't afford latency. Copilots with long-term memory and personalization. Multimodal systems blending text, voice, and context. Privacy-first applications where data needs to stay on-device.

If retrieval is on your critical path, Moss is built for you.

---

### Get started

- [Documentation](https://docs.moss.dev) - quickstart, API reference, guides
- [Examples](https://github.com/usemoss/moss-samples) - sample integrations and demos
- [Website](https://moss.dev) - product overview and pricing

Moss is backed by [Y Combinator (F25)](https://www.ycombinator.com/companies/moss). We're based in San Francisco.

If you're building fast, interactive AI systems - welcome!
