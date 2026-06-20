---
title: Agent Skills context map
description: mikuku-articles の Agent Skills 関連記事群を読む前に、中心概念と主張の配置を把握するための蒸留 Markdown。
category: distilled
topics:
  - distilled
  - agent-skills
  - context-map
  - overview
  - concepts
  - claims
  - observations
  - source-guidance
status: draft
audience:
  - human
  - agent
  - maintainer
created: 2026-06-19
updated: 2026-06-19
sources:
  - type: local-file
    path: references/raw/mikuku-articles
    role: primary
---

# 対象テーマに関する記事群の意味の地図

## これは何か

この Markdown は、`mikuku-articles` に含まれる Agent Skills 関連記事群を、記事ごとの要約ではなく、横断的な意味の地図として読むためのものです。

中心にあるのは、Agent Skills を「便利プロンプト集」ではなく、AI agent が作業時に読む前提、判断基準、参照先、禁則事項、出力の型を束ねる開発資産として見る視点です。

## 中心概念

**Agent Skills**

記事群では、Agent Skills は単なる保存済みプロンプトではなく、AI agent に作業の文脈を渡す再利用可能な単位として扱われています。`SKILL.md`、`references/`、`templates/`、`examples/`、場合によっては `scripts/` や CLI / MCP との関係を含みます。

**発火**

発火とは、ユーザー依頼と skill の名前・description が照合され、特定の skill が使われると判断される流れです。発火後は `SKILL.md` が読まれ、必要に応じて参照ファイルが読まれます。記事群では、発火はターンごとに再評価され、無条件に永続しないものとして説明されています。

**description**

description は、skill の用途説明であると同時に、発火判断の入口です。どの依頼で使うか、使わないか、明示指定が必要か、候補提示に留めるべきかを短く書くことが、誤発火や過剰な読み込みを抑える要点として扱われています。

**SKILL.md と references/**

`SKILL.md` は入口、`references/` は知識本体という分担が繰り返し出てきます。`SKILL.md` には発火条件、最初に読むもの、禁止事項、成果物の境界を置き、長い背景説明や詳細な判断基準は `references/` に逃がす考え方です。

**コンテンツ型 Agent Skill**

Markdown、テンプレート、例文、判断基準、画像など、静的なコンテンツを中心に構成する skill を指す仮の整理です。正式分類ではなく、運用から見えてきた観測上の分類として扱われています。

**自然言語プログラミング**

Agent Skills の Markdown は、自然言語で書かれた説明であると同時に、AI agent の振る舞いを制御する実行仕様に近いものとして見られています。発火条件、禁止事項、参照先、出力形式の設計は、条件分岐やモジュール設計に似たものとして語られています。

**progressive disclosure**

必要になった段階で必要な情報だけを読む、という考え方です。Agent Skills では、入口を小さく保ち、詳細資料、例、テンプレート、raw データを必要時に開くことで、トークン消費と判断の混乱を抑える方針として出てきます。

**軽い RAG 風の知識参照**

記事群では、Agent Skills の `references/` 以下に置いた Markdown や raw 記事を、AI agent が検索して読む使い方を「RAG 風」と呼んでいます。ただし、ベクトル DB や検索サーバーを使う本格 RAG ではない、と明確に区別されています。

**蒸留 Markdown**

大量の raw 記事や作業ログを毎回読ませる代わりに、繰り返し使う概念、判断軸、重要な前提を短くまとめ直した入口です。元記事を置き換えるものではなく、raw に戻る前の地図として位置づけられています。

**index.json / miku-indexgen**

資料が増えたとき、AI agent が本文を読む前に候補を絞るための入口として `index.json` や `index.md` が重視されています。`miku-indexgen` は、その入口を自動生成する道具として言及されています。

**開発資産の発芽成長**

Agent Skills が整うと、短い会話や小さな観察から、記事、README、設計メモ、examples、新しい skill のアイデアが生まれやすくなる、という観測です。ただし、増えればよいわけではなく、人間による採否、整理、剪定が必要だとされています。

## 主要な主張

Agent Skills は、AI agent に毎回同じ説明を貼る代わりに、作業の文脈、判断、禁止事項、参照資料を再利用可能な形で置く仕組みとして見られています。

Agent Skills の設計では、人間向けの長い操作説明よりも、agent 向けの判断材料が重要になります。人間には「何の skill か、どう呼ぶか、何が出るか」を示し、細かい条件や文体、参照すべき過去例は `SKILL.md` や `references/` に置くという切り分けです。

`SKILL.md` は太らせすぎないほうがよい、という主張が複数の記事にあります。入口が重いと、発火のたびに不要な文脈を持ち込みやすくなります。一方で短すぎると agent が迷うため、入口として必要な情報は残す必要があります。

トークン消費を抑える鍵は、単に文章を短くすることではなく、不要な skill を発火させないこと、必要な参照だけを読むこと、蒸留済みの入口から raw へ戻れるようにすることです。

Agent Skills は、自然言語だけで完結するものではなく、必要に応じて `.mjs`、CLI、MCP、index 生成などと役割分担します。自然言語は意図や判断基準を渡すのに向き、再現性や性能が必要な定型処理は実行コードやツールに寄せる、という整理です。

Agent Skills や参照資料は、作って終わりではなく、使いながら育てる開発資産として扱われています。よい例、悪い例、判断基準、索引、蒸留 Markdown は、後続の agent 作業の入口になります。

## 観測されたこと

`mikuku-articles-rag-skill` の step1 記事では、最小構成の `SKILL.md` と `.gitignore`、`references/raw/mikuku-articles/` に置いた記事データだけで、AI agent が Agent Skills 関連記事候補を探し、記事群の主張を横断的に整理する動きが記録されています。

その探索では、docs や images ではなく、日付ディレクトリ直下と `2026/draft` の Markdown を中心に、Agent Skills 関連語で候補を絞る動きが見られました。

Agent Skills 関連の主要記事として、発火、説明ページ、自然言語プログラミング、コンテンツ型 skill、コンテンツ型の種類、実行コードとの役割分担、開発資産の発芽成長、トークン削減、魔法書の比喩、RAG 風参照が繰り返し現れています。

記事群では、`index.json`、front matter、ファイル名、見出しが、AI agent が最初に読む候補を選ぶための入口として観測されています。

AI agent は最初からすべてを精読せず、`SKILL.md`、README、TODO、front matter、見出し、ファイル名、検索結果から入口を探し、そのあと必要な場所を深く読む、という「速読」の見方が示されています。

コンテンツ型 Agent Skill では、`templates/` が出力構造、`examples/` が温度感や粒度、`references/` が判断基準や背景知識を支えるものとして観測されています。

## まだ断定できないこと

Agent Skills の発火や読み込みの細部は、記事中でも「現在の Codex セッション内で観測できる範囲」として扱われています。外部仕様として固定されているか、他環境でも同じかは断定できません。

コンテンツ型 Agent Skill、知識ベース型、テンプレート型、索引・入口型などの分類は、正式な標準分類ではありません。自分たちの運用を見直して見えてきた補助線として扱うべきです。

軽い RAG 風の知識参照は、本格的な RAG 基盤と同一視できません。embedding、ベクトル検索、検索サーバー、外部サービスを使った評価とは別物です。

`miku-indexgen` による index 生成が、どの程度トークン消費を減らすかは、step2 ドラフトでは観察予定として置かれています。効果を定量的に断定する材料は、この蒸留対象だけでは不足しています。

`.mjs` や CLI を入れると安定する、という観測はありますが、すべての Agent Skill に実行コードを入れるべきだとは主張されていません。Node.js などの runtime 依存が増えるため、適用範囲は見極めが必要です。

開発資産の発芽成長は、体験から出た概念です。自己強化的な循環として観測されていますが、放置すればよい資産だけが増える、という意味ではありません。

## 元記事へ戻るべき場合

Agent Skills の発火条件、継続、上位指示との優先順位を正確に確認したい場合は、`20260509-agent-skills-activation.md` に戻るべきです。

Agent Skills の説明ページ、人間向け説明と agent 向け判断材料の分担を確認したい場合は、`20260509-agent-skills-docs.md` に戻るべきです。

自然言語プログラミング、`description`、`When To Use`、`Do Not`、Markdown 見出しの意味を詳しく見る場合は、`20260514-agent-skills-natural-language-programming.md` に戻るべきです。

`SKILL.md`、`references/`、`templates/`、`examples/`、`index.json` の役割分担を確認する場合は、`20260516-content-agent-skills.md` と `20260523-content-agent-skill-types.md` に戻るべきです。

プロンプトだけで苦しくなる場面、`.mjs`、CLI、MCP との役割分担を確認したい場合は、`20260526-agent-skills-basic-machine-language.md` に戻るべきです。

トークン消費、progressive disclosure、蒸留 Markdown、front matter、index の考え方を確認したい場合は、`20260531-token-consumption-03-agent-skills-reduction.md` に戻るべきです。

Agent Skills を「魔法書」として説明する比喩や、禁則事項、MP 効率、棚としての skill 群を確認したい場合は、`20260603-general-agent-skills-magic-book.md` に戻るべきです。

実際に `mikuku-articles` を raw に置いて、Agent Skills で軽い RAG 風参照を試した流れを確認したい場合は、`20260615-agent-skills-rag-step-01.md` に戻るべきです。

`miku-indexgen` を使った索引強化の連作計画を確認したい場合は、`2026XXXX-agent-skills-rag-step-02-indexgen.md` に戻るべきです。ただし、このファイルは draft です。

## 注意点

この蒸留 Markdown は、元記事の代替ではありません。既存記事の主張や根拠を答える場合は、該当する raw 記事本文へ戻って確認する必要があります。

Agent Skills を万能な自動実行プラグインとして説明しないでください。記事群では、AI agent が読む追加の運用手順書、判断材料、参照入口として扱われています。

「RAG 風」という表現を、本格 RAG と混同しないでください。ここでの主対象は、ローカル Markdown、索引、ファイル検索、front matter を使った軽量な文脈参照です。

蒸留 Markdown や index は、raw を読まなくてよくするための最終回答ではありません。読む候補を絞り、どの raw に戻るべきかを判断しやすくする入口です。

Agent Skills の分類や比喩は、理解を助ける補助線です。標準仕様や一般化済み理論として断定しないでください。

資料が増えることは、そのまま品質向上を意味しません。記事群では、発芽した開発資産を残すか、畳むか、蒸留するかを人間が判断する必要があるとされています。
