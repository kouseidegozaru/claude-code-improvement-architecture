# claude-code-improvement-architecture

Claude Code のハーネスを、実セッションの証拠にもとづいて改善し続けるための設計プロンプト集。

## 中身

| ファイル | 内容 |
|---|---|
| [`prompts/01-session-analysis-mcp-server.md`](prompts/01-session-analysis-mcp-server.md) | Claude Code のセッションを分析する MCP サーバーを作らせるプロンプト |
| [`prompts/02-harness-self-improvement-loop.md`](prompts/02-harness-self-improvement-loop.md) | その MCP サーバーを計測器として、ハーネス自己改善ループを構築させるプロンプト |
| [`docs/design-rationale.md`](docs/design-rationale.md) | なぜこの構成にしたか。各制約が防いでいる失敗モード |

## 使い方

1. プロンプト1 を Claude Code に渡す。`---` 以降が本文
2. 設計案が返ってくるので、合意してから実装させる
3. MCP サーバーが動くようになったら、プロンプト2 を渡す
4. プロンプト2 も設計案 → 合意 → 実装の順で進める

どちらも「詳細な技術要件は Claude Code 側に決めさせる」方針で書いてある。
指定してあるのは、目的・答えるべき問い・制約・受け入れ基準・非目標であり、
実装の中身ではない。

## 設計の背景

素朴な自己改善ループは、単一候補を単一スコアで磨き続ける構造になりがちで、
最初の前提がアンカーとして残り、局所最適から出られない。
これはモデルの能力の問題ではなく探索構造の問題なので、
**前提を覆せる探索構造をハーネス側に用意する**必要がある。

- [自己改善エージェントはなぜ前提を覆せないのか ― 局所最適とハーネスでの脱出](https://zenn.dev/layerx/articles/b36ceffe6b5e20)
- [GEPA: Reflective Prompt Evolution Can Outperform Reinforcement Learning (arXiv:2507.19457)](https://arxiv.org/abs/2507.19457)
- [Huxley-Gödel Machine (arXiv:2510.21614)](https://arxiv.org/abs/2510.21614)
