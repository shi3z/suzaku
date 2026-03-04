# Suzaku（朱雀）

ワンショットでローカルLLM環境を自動構築するブートストラッパー。

誰でも迷わずローカルLLMを動かせることを目指しています。

## 特徴

- **完全自動セットアップ** — OSやハードウェアの差異を吸収し、最小限の操作で環境構築
- **インテリジェントなハードウェア検出** — GPU種別（NVIDIA / AMD / Apple Silicon）、RAM容量を自動判定
- **コンテキスト長の最適化** — 搭載メモリに応じて最適なコンテキスト長を自動設定
  - 64GB以上: 128K / 32GB以上: 64K / 16GB以上: 32K / 16GB未満: 16K
- **オプション機能の安全なインストール** — vLLM、MLX、Docker等はコア機能を壊さず導入

## 対応プラットフォーム

| OS | アーキテクチャ | サポート |
|---|---|---|
| macOS | Apple Silicon | 優先サポート |
| macOS | Intel | ベストエフォート |
| Linux | x86_64 | 優先サポート |
| Linux | aarch64 | ベストエフォート |

## クイックスタート

```bash
git clone https://github.com/shi3z/suzaku.git
cd suzaku
./setup.sh
```

セットアップ完了後:

```bash
ollama run gpt-oss:20b-long
```

API経由での利用:

```bash
curl http://localhost:11434/api/chat -d '{
  "model": "gpt-oss:20b-long",
  "messages": [{"role": "user", "content": "こんにちは"}]
}'
```

## セットアップの5フェーズ

1. **環境検出** — OS、CPUアーキテクチャ、RAM、GPU種別を検出
2. **Ollamaインストール** — Ollamaの導入とサーバーのヘルスチェック
3. **ベースモデルのダウンロード** — gpt-oss:20b を取得
4. **派生モデルの作成** — メモリに応じた拡張コンテキスト長でモデルを作成
5. **追加環境の構築（任意）** — vLLM、MLX、uv、Docker等

## 必要要件

- bash
- インターネット接続
- モデル保存用の十分なストレージ

## ライセンス

MIT
