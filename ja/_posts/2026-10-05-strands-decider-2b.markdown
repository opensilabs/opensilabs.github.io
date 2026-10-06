---
lng_pair: id_20261005_strands-decider-2b
title: "書けないモデル：AWSがエージェントに与えた「決定者」"
author: OpenSI-Labs
category: models
tags: [決定モデル, AIエージェント, AWS, オープンソース, LLM]
date: 2026-10-05 06:00:00 -0700
img: /assets/img/posts/2026-10-05-strands-decider-2b.png
meta_description: "AWSのStrands Decider 2Bは言語モデリングヘッドを切り離しポインタヘッドに置換——生成せず選ぶだけの決定モデルを単一フォワードパスで実現。"
---

先週、AWSは20億パラメータの言語モデルを公開した。ただし一文字も書けない。要約もコードも雑談も不可。思考をテキストに変える部品が、外科手術のように取り除かれているからだ。

これは欠陥ではない。設計そのものだ。

Strands Decider 2B——AmazonのStrands Labsが開発し、10月1日にオープンソース公開した。一年前にはほぼ存在しなかった新種「決定モデル（decision model）」の一員だ。言語モデルが「生成」するのに対し、決定モデルは「選ぶ」。質問と選択肢を渡すと各選択肢の確率分布を返す。フォワードパスは一度きり。デコードもサンプリングもない。（[TechStrong](https://techstrong.ai/articles/aws-explores-decision-models-with-strands-decider-2b/)）

手術は精密だ。アリババのオープンウェイトQwen3.5-2B-Baseを「胴体」とし、次トークン予測の出力層——言語モデリングヘッドを切り離し、100万強パラメータのポインタヘッドを移植した。`<answer>`位置の内部表現と各候補の最終トークンの隠れ状態を内積比較し、マスク付きsoftmaxを一度かける。問題を一度読み、答えは一回の行列積から落ちてくる。（[TechTimes](https://www.techtimes.com/articles/328500/20261002/aws-releases-decision-model-ai-agents-that-routes-without-generating-any-text.htm)）

適応に再学習は不要だった。Microsoft ResearchのLoRAをランク16で適用するだけで足り、較正を守るためポインタヘッドは32ビット全精度に保たれた。設計名は「Hobson」、公開版はバージョン19。初期のスロットヘッド設計は著しく劣っていたという。（[VentureBeat](https://venturebeat.com/technology/amazon-unveils-a-free-fast-open-source-jev-killer-strands-decider-2b-makes-decisions-in-fractions-of-a-second)、[SQ Magazine](https://sqmagazine.co.uk/amazon-strands-decider-2b-open-source-decision-model/)）

なぜ「できないことの多い」モデルを作るのか。エージェント内部の判断の大半に言葉は要らないからだ。どのツールが処理するか。ポリシー適合か。次はどのモデルか。今日これらは汎用LLMに投げられ、本質は四択なのに生成サイクルをまるごと燃やす。Deciderはその雑務用で、高価な推論は本当に必要な仕事に残す。（[TechStrong](https://techstrong.ai/articles/aws-explores-decision-models-with-strands-decider-2b/)、[AIAffairs](https://www.aiaffairs.com/technology/aws-releases-strands-decider-2b-local-ai-agent-decisions/)）

数字が物語る。RTX 3090級で100ミリ秒未満、M3 MacBookで中央値約153ミリ秒。新興ベンチマークJevBenchでイージー層100%、約20億級公開モデル中2位、学習レシピ完全公開のモデルでは1位。AWSはBrierスコアで評価する——「口にした確信度」と実際の正解率の一致を見る指標だ。（[CryptoBriefing](https://cryptobriefing.com/amazon-strands-decider-2b-open-source-jev/)、[SQ Magazine](https://sqmagazine.co.uk/amazon-strands-decider-2b-open-source-decision-model/)）

この一点が核心だ。信頼こそ商品でない限り、較正を自慢する者はいない。「選択肢B、92%」と言って本当に92%当たるモデルは業務ロジックに直結できる。許可、拒否、迷えばエスカレーション。チャットボットの自信は演技、決定者の自信はAPIだ。

しかもAWSは孤独ではない。OpenAIはDevDayでDecisions APIを、Databricksはai_decideをベータ公開。TypeSafeのJevが先鞭をつけ、CEOはXで「Jevクローン戦争」と冗談を飛ばす。決定モデルはスタックの一層になりつつある。（[Another Daily AI Newsletter](https://www.anothercodingblog.com/p/another-daily-ai-newsletter-october)）

ここが考えどころだ。3年続いた「一つのモデルがすべてをこなす」ドクトリンからの撤退である。業界はプロンプトで汎用モデルに下請けをさせた——効果はあった、請求書も立派だった。Deciderは古い美徳への回帰、サイズの合った部品だ。LLMの胴体は驚異の「読み手」として残し、「書き手」からは降ろす。認知科学の言葉ではSystem 1モジュール——速く、専門的で較正済み——を最先端モデルのSystem 2に外付けする。「大が考え、小が些事を決める」ハイブリッドエージェントをAWSはすでに観察している。（[The AI Economy](https://theaieconomy.substack.com/p/strands-decider-2b)）

レイテンシより重要な二次効果もある。判断のたびフルLLMを燃やすなら、ガードレールは配給制——要所に置いて祈るだけだ。判断がローカルで100ミリ秒なら、ツール呼び出しごとに検問を置ける。AWSのデモがまさにそれだ。天気APIの前に、使う都市がユーザー由来か幻覚かを決定者が検証し、後者なら問い直しに送り返す。安いブレーキは至る所で使われる。性能の皮を被った安全の話だ。（[AIAffairs](https://www.aiaffairs.com/technology/aws-releases-strands-decider-2b-local-ai-agent-decisions/)）

冷静さも要る。四択ベンチマークはこの種を甘やかす。選択肢も質問も閾値も誰かが定義する——デモでは手作業だった。モデルはスコアを渡すだけ、「何を問うか」は開発者の仕事だ。統合ライブラリは開発中とAWSも認める。（[VentureBeat](https://venturebeat.com/technology/amazon-unveils-a-free-fast-open-source-jev-killer-strands-decider-2b-makes-decisions-in-fractions-of-a-second)）

ゆえに今回の核心は重みですらないかもしれない。学習データ、スクリプト、19版の反復ノート——レシピの全公開だ。誰でも決定者を作り、自前の選択肢に微調整し、判断のたびAPIを借りず自前ハードで回せる。モデルはデモ、レシピこそプラットフォームだ。

3年、業界は「一つのモデルがどこまでできるか」を問うた。より良い問いはこうだ。そのモデルは最小限何ができればいいのか——その一事を速く、正直に、オープンにやるなら。

*あなたの業務では今、どの判断がLLMのフル生成を燃やしているか。チェックが0.1秒なら何を置くか。*
