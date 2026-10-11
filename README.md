# Repolex Knowledge Graph of psf/policies

RDF knowledge graph data for [psf/policies](https://github.com/psf/policies), parsed by [repolex](https://repolex.ai).

> **Note**: This data is experimental and subject to change without notice.

## How to use this data

The easiest way to get started is to install the [rlex](https://github.com/repolex-ai/rlex) query tool:

```bash
cargo install --git https://github.com/repolex-ai/rlex
```

Verify the install:

```bash
rlex --help
```

**rlex is designed to be used primarily by LLMs in a terminal.** Start up your favorite AI assistant and ask it to use rlex. It handles the SPARQL — you just ask questions in plain English.

To load this repo's data:

```bash
rlex download psf/policies
```

Consult `rlex --help` for other options, including SPARQL queries, HTTP server, and interactive visualization.

## Data structure

All data is stored as gzip-compressed [N-Quads](https://www.w3.org/TR/n-quads/) (`.nq.gz`), a standard RDF format that can be loaded into any triplestore or graph database.

```
.
├── aggregate
│   ├── ast
│   │   └── e767816f9675d0b63089de873ddd89744a47c6b2
│   │       └── chunk-001.nq.gz
│   └── repolex
│       └── e767816f9675d0b63089de873ddd89744a47c6b2
│           └── chunk-001.nq.gz
├── blob
│   ├── 10c18959b6968c4223227728ccb0aed0b3e43d2e.nq.gz
│   ├── 110e4ab42787876819cbb850c0c323e271feb118.nq.gz
│   ├── 1abcd45ac077843d79734d8c7e3747095751e7e2.nq.gz
│   ├── 1d86bb4bdebca19cc18c977010bc223cc818c029.nq.gz
│   ├── 2b876754ffe968224f63c5b8198107f26aeb65a1.nq.gz
│   ├── 2b9589dd7c5221fd65d88a24309c3cf33f3b3196.nq.gz
│   ├── 319962585cfd4f6056f9e01a42ad8b10f307aba4.nq.gz
│   ├── 329e4e08c4aa996a655fd3627c29678507432bf7.nq.gz
│   ├── 33a75a39a42a8b9d00c596091ca4e514470e486c.nq.gz
│   ├── 3a7faabdbc266e4a88094bd0a6d0aea5ff764e80.nq.gz
│   ├── 3cd35ebe2b8c6fb4a70f669c91ca70e45033798d.nq.gz
│   ├── 448b8d9676f3e30dfcc3704e01e32eeca1295909.nq.gz
│   ├── 5e4495cd6790e164caf49db43c9712308c4be99e.nq.gz
│   ├── 5efdc93e5091c252f6789c74f1f960223c223a63.nq.gz
│   ├── 66e5ef9f6da8baf3a7fc91e406d58e95a4de0a40.nq.gz
│   ├── 705c203e3f9a4e5ebbcd96953fb899d532a38f36.nq.gz
│   ├── 79b6c13e35dd1a55f87a77950b8e9310e028c0e2.nq.gz
│   ├── 7a0f9aa14bac518d48d5b145b06532be769ae686.nq.gz
│   ├── 80d71e385db234192e37c8f794f1e734722987af.nq.gz
│   ├── 818e7b8afef708e2c00111d9c7750af190311a75.nq.gz
│   ├── 8365645c9712db6e0fa7cea3ba541517059f321f.nq.gz
│   ├── 8b137891791fe96927ad78e64b0aad7bded08bdc.nq.gz
│   ├── 90bffc0637d262765b7e6cff70cef4821cd9d355.nq.gz
│   ├── 92f2fbacb230285e69cbea882bee4e214a5ef46f.nq.gz
│   ├── 94307d8d40bbeded577dafda759ecf0b348e3105.nq.gz
│   ├── 95b00ab7761551f09e76ada520b253cc9bcf2aa6.nq.gz
│   ├── 97277d0b591c8e96bdb42dc9dbffefa4fb010451.nq.gz
│   ├── a17bd4c6e402254891be63205618a9ef7220c533.nq.gz
│   ├── aa48240e9b63bb9f32339d10ae3022b4150088c8.nq.gz
│   ├── aaf6b855380e4a92272c7d60e393635ec5db3ec0.nq.gz
│   ├── ab6c12d1e0cca32d9e741b046b4acd277b1c3725.nq.gz
│   ├── bc5c9373165b1362f5ab92990bdedc349ee45042.nq.gz
│   ├── c095fdaba6b4c4ae647d0b04aa70d9967811830c.nq.gz
│   ├── d543f1d758ee6a30ed52695889f377b66ba4e8aa.nq.gz
│   ├── ed9404f27d308376b5a79782aa6e30f06e7f8432.nq.gz
│   └── f48602567dcc5b13f23ad7d70d8540744119f10d.nq.gz
├── branch
│   └── branch.nq.gz
├── commit
│   └── commit.nq.gz
├── filetree
│   └── e767816f9675d0b63089de873ddd89744a47c6b2.nq.gz
├── issue
│   └── issue.nq.gz
├── pr
│   └── pr.nq.gz
└── tag
    └── tag.nq.gz

13 directories, 44 files
```

| Directory | What it contains |
|-----------|-----------------|
| `blob/` | Per-file AST graphs, content-addressed by git blob SHA. Each file in the source repo gets its own graph. |
| `aggregate/ast/` | Combined AST graph per parsed commit. Merges all blob graphs for a snapshot of the entire codebase at that point. |
| `aggregate/lsp/` | Language Server Protocol enrichment: resolved symbols, definitions, references, and type information. |
| `aggregate/dataflow/` | Interprocedural data flow edges between functions and modules. |
| `aggregate/repolex/` | Combined graph (AST + LSP + dataflow) per commit. |
| `commit/` | Git commit metadata (author, date, message, parent links). |
| `branch/` | Branch metadata. |
| `tag/` | Tag metadata. |
| `filetree/` | File tree snapshots per commit (which files existed and their blob SHAs). |
| `audit/` | Code architecture and graph audit reports per commit. |

## Source repository

[psf/policies](https://github.com/psf/policies)

---
*Parsed on 2026-10-11 by [repolex](https://repolex.ai)*
