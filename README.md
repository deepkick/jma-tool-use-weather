# jma-tool-use-weather

**気象庁の公式データに、日本語で質問できる窓口** — LLM の Tool Use を Google Colab で体験するデモ

気象データアナリスト・コミュニティ(WDAC)AI研究ラボ ワーキングチーム 第2回(2026-10-04)の話題提供用に、
Claude と共に作成したノートブックです。エンジニアでない方が、自分の Colab で動かして
「LLM が公式データを自分で取りに行って答える」仕組みを体験することを目的にしています。

## 何ができるか

- 「今週の京都でサイクリングに向く日は?」「宮城県の今週の天気を 200 字の記事に」といった日本語の質問に、
  LLM が気象庁の公開データ(週間予報・3 日間予報・概況文・警報注意報・アメダス実況)を取りに行って答えます
- 回答は Markdown(見出し・表)で表示され、`.md` / `.html` として保存・ダウンロードできます
- Python 関数を 1 つ書いて登録するだけで、LLM が使える「道具(Tool)」が増えます

## 動作条件

- Google アカウントと Google Colab(無料枠の T4 GPU で動作)
- API キー・Hugging Face トークン・課金は不要
- LLM は Qwen3 をローカル推論(4bit 量子化)。ノートブック冒頭で GPU に合わせてモデルを選べます

| モデル | VRAM 目安 | T4 (16 GB) | A100 |
|---|---|---|---|
| Qwen3-4B-Instruct-2507 | 約 3 GB | ◎ 速い | ◎ |
| Qwen3-8B(デフォルト) | 約 6 GB | ○ 標準 | ◎ |
| Qwen3-14B | 約 10 GB | △ 遅い | ◎ |
| Qwen3-30B-A3B-Instruct-2507 | 約 18 GB | × | ◎ |

## 使い方

1. 下のバッジから Colab で開く(または `notebooks/` の `.ipynb` を Colab にアップロード)
2. メニュー「ランタイム」→「ランタイムのタイプを変更」→ T4 GPU を選択
3. 上から順にセルを実行(モデルの読み込みに 5〜6 分かかります)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/deepkick/jma-tool-use-weather/blob/main/notebooks/jma_tool_use_weather.ipynb)

## リポジトリ構成

```
├── README.md
├── LICENSE
├── spec.md                              # 仕様書
└── notebooks/
    └── jma_tool_use_weather.ipynb       # 本体
```

## データの出典と利用条件

- 気象データはすべて気象庁のウェブサイト(https://www.jma.go.jp/)が公開している JSON を利用しています。
  出典: 気象庁ホームページ。利用にあたっては気象庁の「利用規約」に従ってください
  (https://www.jma.go.jp/jma/kishou/info/coment.html)
- 本ノートブックが取得するのは気象庁の**公式発表(予報官の判断を経た予報・実況・警報)**です
- 本ノートブックは学習・デモ目的です。防災上の判断は必ず気象庁および自治体の公式発表に基づいてください
- LLM(Qwen3)は Alibaba Cloud が Apache 2.0 ライセンスで公開しているモデルです

## 参考

- Qwen Team (2025). Qwen3 Technical Report. arXiv:2505.09388
- Hugging Face Transformers — Tool use / function calling with chat templates

## ライセンス

MIT License(コード)。気象データの権利は気象庁に帰属します。
