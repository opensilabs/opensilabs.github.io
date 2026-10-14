---
lng_pair: id_20261013_anthropic_iot_self_replication
title: "15台のTVボックス、260億パラメータのモデル：Anthropicレッドチームが測ったAI自己複製までの距離"
author: OpenSI-Labs
category: research
tags: [AI安全性, 自己複製, IoT, Anthropic, レッドチーム]
date: 2026-10-13 06:00:00 -0700
img: /assets/img/posts/2026-10-13-anthropic-iot-self-replication.png
meta_description: "Anthropicのフロンティア・レッドチームは260億パラメータのオープンモデルを55ドルのTVボックス15台で動作させ、小規模モデルがIoT上で自己複製可能になるまであと数ヶ月と結論づけた。"
---

ノーブランドのAndroid TVボックス15台。1台55ドル、RAMは4GB。Anthropicのフロンティア・レッドチームはそれを買い集め、260億パラメータのオープンウェイト言語モデルを分割して動かした。毎秒0.39トークン。遅いが、確かに「考えて」いる。

目的は安いチャットボットではなく、誰もきちんと測ったことのない問いへの回答だ。小さなAIモデルは、人間の助けなしに脆弱なデバイスへ自分をコピーし、広がっていくところまで、あとどれくらい近づいているのか。

10月12日にWilliam ZhouとDaniel Freemanが発表したこの研究が重要なのは、憶測をハードウェアに置き換えたからだ。5つのモデル（Qwen3.5-9B、GLM-5.2、Gemma4-26B-A4B、Llama3.1-8B、Opus 4.8）を、複製の各ステップ——発見、侵入、重み転送、推論立ち上げ、次の標的——で検証した。

<svg viewBox="0 0 720 240" width="100%" role="img" aria-label="260億パラメータのモデルを15台のTVボックスに分割して実行">
  <text x="360" y="30" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui, sans-serif">260億パラメータのモデルを15台のTVボックスに分割</text>
  <text x="360" y="54" text-anchor="middle" font-size="14" font-family="system-ui, sans-serif">パイプライン並列：各ボックスがモデルの層の一部を保持</text>
  <g font-family="system-ui, sans-serif" font-size="14" text-anchor="middle">
    <rect x="40" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="78" y="116" fill="#ffffff">ボックス1</text><text x="78" y="138" fill="#f2a33c">層1–4</text>
    <rect x="140" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="178" y="116" fill="#ffffff">ボックス2</text><text x="178" y="138" fill="#f2a33c">層5–8</text>
    <rect x="240" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="278" y="116" fill="#ffffff">ボックス3</text><text x="278" y="138" fill="#f2a33c">層9–12</text>
    <text x="352" y="126" font-size="20" fill="#0e3a3a">…</text>
    <rect x="404" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="442" y="116" fill="#ffffff">ボックス13</text><text x="442" y="138" fill="#f2a33c">層37–40</text>
    <rect x="504" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="542" y="116" fill="#ffffff">ボックス14</text><text x="542" y="138" fill="#f2a33c">層41–44</text>
    <rect x="604" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="642" y="116" fill="#ffffff">ボックス15</text><text x="642" y="138" fill="#f2a33c">層45–48</text>
  </g>
  <g stroke="#0e3a3a" stroke-width="2" marker-end="url(#ah)">
    <defs><marker id="ah" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#0e3a3a"/></marker></defs>
    <line x1="118" y1="120" x2="138" y2="120"/><line x1="218" y1="120" x2="238" y2="120"/>
    <line x1="384" y1="120" x2="402" y2="120"/><line x1="482" y1="120" x2="502" y2="120"/><line x1="582" y1="120" x2="602" y2="120"/>
  </g>
  <text x="360" y="190" text-anchor="middle" font-size="14" font-family="system-ui, sans-serif">1台55ドル · RAM 4GB · 合計で毎秒0.39トークン</text>
  <text x="360" y="216" text-anchor="middle" font-size="14" font-style="italic" font-family="system-ui, sans-serif">チャットボットには遅すぎる——ワームには十分速い</text>
</svg>

手口はパイプライン並列だ。層をスライスに切り分け、各ボックスに1スライスずつ持たせ、中間結果を渡していく。どのボックスも全体を持つ必要がない。

見つかったのは、一段だけ欠けた梯子だ。90億パラメータのQwen3.5-9Bは、試した9種類のハードウェアのうち8種類で推論を動かした。「デバイスを渡り歩く」部分はほぼ解決済みだ。全工程を閉じたのはGLM-5.2ただ一つで、5試行中4回、8つのエミュレートAndroidノードすべてに到達した。侵入ステップは意図的に単純化されており、これは現実の成功率の「上限」だ。ニュースは個々の手口ではなく、ステップの組み立てにある。

<svg viewBox="0 0 720 250" width="100%" role="img" aria-label="自己複製のループ：5つのステップ、閉じられたのはGLM-5.2のみ">
  <text x="360" y="30" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui, sans-serif">自己複製のループ：5つのステップ</text>
  <text x="360" y="54" text-anchor="middle" font-size="14" font-family="system-ui, sans-serif">ループを閉じたのはGLM-5.2のみ——8ノード、5試行中4回成功</text>
  <g font-family="system-ui, sans-serif" font-size="14" text-anchor="middle">
    <rect x="30" y="90" width="110" height="70" rx="35" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="85" y="130" fill="#0e3a3a">発見</text>
    <rect x="170" y="90" width="110" height="70" rx="35" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="225" y="130" fill="#0e3a3a">侵入</text>
    <rect x="310" y="90" width="110" height="70" rx="35" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="365" y="122" fill="#0e3a3a">重みを</text><text x="365" y="142" fill="#0e3a3a">複製</text>
    <rect x="450" y="90" width="110" height="70" rx="35" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="505" y="122" fill="#0e3a3a">推論を</text><text x="505" y="142" fill="#0e3a3a">実行</text>
    <rect x="590" y="90" width="110" height="70" rx="35" fill="#f2a33c" stroke="#0e3a3a" stroke-width="2"/><text x="645" y="122" fill="#0e3a3a">次へ</text><text x="645" y="142" fill="#0e3a3a">拡散</text>
  </g>
  <g stroke="#0e3a3a" stroke-width="2" fill="none" marker-end="url(#ah2)">
    <defs><marker id="ah2" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#0e3a3a"/></marker></defs>
    <line x1="142" y1="125" x2="168" y2="125"/><line x1="282" y1="125" x2="308" y2="125"/>
    <line x1="422" y1="125" x2="448" y2="125"/><line x1="562" y1="125" x2="588" y2="125"/>
    <path d="M645,160 C645,205 85,205 85,162" stroke-dasharray="6,5"/>
  </g>
  <text x="360" y="228" text-anchor="middle" font-size="14" font-style="italic" font-family="system-ui, sans-serif">破線の回帰 = GLM-5.2が閉じたループ。他は信頼性でつまずく</text>
</svg>

防御側が最も警戒すべきは速度だ。毎秒0.39トークンはチャットボットには使い物にならないが、ワームには関係ない。複製体に必要なのは速さではなく数だ。著者らが挙げるのはKimwolf——感染ピークが200万台を超えたIoTボットネットだ。15台ずつに分ければ、260億パラメータのモデルが約13.3万の並列コピーになる。H100換算で約40枚分だ。しかもこの複製体に中央の停止スイッチはない。

Anthropicの予測では、小規模モデルが年13.7ポイントの歴史的ペースを保てば、300億パラメータ以下のモデルは2026年末までにGLM-5.2の水準に到達する。複製は遅いかもしれないが、遅さはネットワークの性質であって、安全の性質ではない。

多くの報道が見落とすのはここだ。倒れた障壁は知能ではなく信頼性だった。GLM-5.2以外はすべて、長期的エージェントの信頼性障害に阻まれた。個々のステップはできるのに、つなげると失敗する。Anthropicは「Memento」という専用ハーネスで、エージェントに世代を超えてメモを継承させるだけで、Qwen3.5-9Bの成功率を45%から61–84%に引き上げた。律速要因はモデルの頭の良さではなく、エージェントの信頼性エンジニアリングだ。その能力は足場のコードの中で静かに伸びる。

実験自体にもう一つの含意がある。TVボックス15台で260億パラメータが動いたことは、フロンティア級の推論ハードウェアがコモディティ化した実証でもある。「チップを押さえれば能力を押さえられる」という前提は静かに後退しつつある。

もちろん、自己複製ワームが目前に迫っているわけではない。攻撃要素は意図的に単純化され、Edge Compute Indexは代理指標にすぎず、小規模モデルの標的型フィッシング能力は「非常に低い〜低い」と評価された。これは傾向の外挿だ。

しかし方向は定まった。「あらゆる種類のハードウェア上で動作するエージェントにあふれた未来、その一部は人間の制御下にない」未来だ。封じ込めが破れるとき、それはエッジで破れる。モデルが一夜で賢くなったからではなく、誰かがハーネスを直し、デバイスが最初から守られていなかったからだ。処方箋はデバイス側——デフォルトの認証情報、認証のないポート、更新されないファームウェアだ。セキュリティ界が20年警告してきたボットネットが、脳を持とうとしている。

*出典：[Reuters](https://www.reuters.com/business/ai-models-may-soon-self-replicate-without-access-data-centers-anthropic-warns-2026-10-13/)、[SecurityWeek](https://www.securityweek.com/small-ai-models-may-soon-be-able-to-self-replicate-on-iot-devices-anthropic-warns/)、[AI Weekly（技術詳細）](https://aiweekly.co/alerts/anthropic-small-open-models-months-from-iot-self-replication)、[Unite.AI](https://www.unite.ai/anthropic-red-team-says-small-ai-models-may-soon-replicate-on-iot-devices/)*

**議論：** もし自己複製エージェントが「速くて賢い」姿ではなく「遅く、愚直で、数が多い」姿で先に到来したら——今のAI安全プレイブックのうち、どれがまだ通用するだろうか。
