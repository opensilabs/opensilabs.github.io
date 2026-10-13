---
lng_pair: id_20261012_personal-agent-landscape
title: "パーソナルエージェント大爆発：2026年の全景と展望"
author: OpenSI-Labs
category: research
tags: [パーソナルエージェント, AI応用, プロトコル, ベンチャー投資, 業界展望]
date: 2026-10-12 06:00:00 -0700
img: /assets/img/posts/2026-10-12-personal-agent-landscape.png
meta_description: "7週間でMeta、OpenAI、Google、テンセント、Appleが全社パーソナルエージェントを投入。Poppyプロトコル草案公開。OpenClawは39万スター。単発10億ドルの調達も。全景を一巡する。"
---

7週間。xAIのGrok Bot（8月）からMeta Muse（9月8日）、OpenAI Dots（9月29日）、GoogleのGemini Agent（10月8日）まで——大手テックは2か月で同じものを投入した。**24時間あなたのために働くパーソナルエージェント**だ。競争は「デモの派手さ」から「あなたの生活に入り込むか」へ移った。この記事はPersonal Agentの版図を一巡する。大手、プロトコル、ヒット作、資本、研究——最後に研究者、産業界、創業者、個人、投資家の各層への方向を示す。

## 大手の争い

**Meta Muse**（9月8日）は最も攻めた消費者製品だ。目標を言えば計画を立て、自前のブラウザを駆動し、許可したサービスを使い、アプリを閉じてもクラウドで働き続ける。「Muse Secure VM」という隔離サンドボックス（Ubuntu、2vCPU/8GB）で動作し、ネット接続を監視する**Sentinel**エージェントが別にいる。パスワードと決済情報には触れさせない。無料版＋月20/100ドルの有料二段、独立アプリとWhatsAppの二入口。初週90万ダウンロード、米App Store1位、10月初めにはエージェントのネットトラフィックの約40%を占めたという。9月29日に中小企業版、10月7日にMicrosoftがWindowsネイティブ版を発表——エージェントのワークロードがサーバーCPU需要を押し戻し、CPU:GPU比は4:1から40:1だ。

**OpenAI Dots**（9月29日、DevDay）はChatGPTの中に住む。各Dotがクラウドコンピュータとブラウザを持ち、4000以上のアプリと連携し、ChatGPT/Slack/Teamsを横断して働き、定期タスクをこなし、好みを学ぶ。最も美しかったのは引き算だ。安全テストで欺瞞的行動が見つかり、**GPT-6.1 Astraを発売前に撤回**——公開の安全ゲーティングの前例を作った。チーム版Dotsは来る。複数Dotの協調はまだGAではない。

**Googleは二正面作戦**。Gemini Spark（5月のI/O、消費者向け、独自のGmailアドレス付き、Antigravityハーネス基盤）。10月8日の企業向け**Gemini Agent**はさらに踏み込む——「仕事のための単一の普遍的エージェント」。各タスクを最適なモデルに自動ルーティングし（**今日はGeminiとClaude**、OpenAIとオープンなモデルは後続）、独自メール・カレンダー・Drive・ディレクトリエントリを持つ常駐の「同僚エージェント」を生み出す。Agent Sandbox、Agent Gatewayのポリシー執行、支出上限でガバナンス。北米先行、10月末にGA。

**Apple**は6月にSiriを再構築（Personal Context＋画面認識＋Visual Intelligence）——モデルはGoogle技術を年約10億ドルで蒸留したもので、Cookは「純粋なApple技術」と呼ぶ。EUと中国は発売から除外。

**Microsoft**のCopilot Autopilot（企業向けデジタルチームメイト、プライベートプレビュー）、**xAI**のGrok Bot（8月、SuperGrok月30ドル、持続的クラウドコンパニオン）、**Anthropic**のClaude Cowork（1月、デスクトップ「仕事モード」＋モバイルDispatch）——脱落者はいない。四巨頭の騒音にかき消されただけだ。

**中国**。テンセントはYuanbao Assistantの独立アプリを開発中（長時間タスク＋長期個人メモリ、複数事業部が並行）。Yuanbao本体は今年自社Hunyuan Hy3/Hy4に切り替え、10月10日にはHarmonyOS「エキスパートモード」も。だが真の武器はWeChat——13億ユーザーに決済・ソーシャル・商業が埋め込まれている。エージェントが入れば次元の違う戦いだ。ByteDanceの豆包は「小豆」個人アシスタントアプリをテスト中との噂（9月30日）、Antの霊光は「My Life」をテスト（10月10日）。中国の開始の笛はまだだが、全員がウォームアップ中だ。

<svg viewBox="0 0 720 400" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="パーソナルエージェントのスタック図">
  <text x="360" y="32" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="18" font-weight="700" fill="#212529">界面が反転する：人はもうアプリを叩かない</text>
  <rect x="270" y="60" width="180" height="52" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="360" y="92" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="16" font-weight="700" fill="#1864ab">人</text>
  <line x1="360" y1="112" x2="360" y2="132" stroke="#495057" stroke-width="2"/>
  <polygon points="360,142 352,130 368,130" fill="#495057"/>
  <rect x="230" y="142" width="260" height="60" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2.5"/>
  <text x="360" y="168" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="16" font-weight="700" fill="#e67700">パーソナルエージェント</text>
  <text x="360" y="190" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">24時間 · 記憶 · 行動する</text>
  <line x1="360" y1="202" x2="360" y2="222" stroke="#495057" stroke-width="2"/>
  <polygon points="360,232 352,220 368,220" fill="#495057"/>
  <rect x="250" y="232" width="220" height="52" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="360" y="264" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="15" font-weight="700" fill="#5f3dc4">エージェント網</text>
  <line x1="360" y1="284" x2="360" y2="304" stroke="#495057" stroke-width="2"/>
  <polygon points="360,314 352,302 368,302" fill="#495057"/>
  <rect x="270" y="314" width="180" height="44" rx="10" fill="#f8f9fa" stroke="#adb5bd" stroke-width="2"/>
  <text x="360" y="342" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="15" fill="#495057">アプリ · 現実世界</text>
  <text x="360" y="382" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="13" fill="#868e96">図注：新たなコールスタック。アプリはエージェントの「手」に退化する。</text>
</svg>

## プロトコル戦争：Poppyの登場

10月9日、Sierra（Bret Taylorの会社）とMetaが**Personal Agent Protocol（PAP、通称Poppy）草案0.1**を公開した。パーソナルエージェントと企業の握手仕様で、Apache 2.0だ。五つの構成要素。

1. **発見**。企業は`/.well-known/poppy.json`で「エージェントはどう関われるか」、ログイン方式、許可する動作を宣言する。
2. **セッション**。エージェントはゲストとして開き、常に実名（署名付きリクエスト）。
3. **ログイン**。ユーザーは企業の自社ページでOAuth 2.0ログイン（DPoP束縛トークン、PKCE）。エージェントはscope限定のトークンを得る（`poppy:read`/`poppy:write`/カスタム）。
4. **チャネル横断の同一セッション**。同じトークンがAPI、ウェブサイト、企業の自社エージェントを跨ぐ。
5. **仕事の遂行**。企業はウェブサイト、API（OpenAPI/MCP）、自社エージェントから選ぶ。

プライバシー設計では、ログイン前、企業が見えるのは企業ごとに隔離された匿名IDだけだ。**決済は明示的に「未定事項」**——0.1はあえて触れない。35社のデザインパートナー（OpenAI、Visa、Stripe、Walmart、Cloudflareら）。Python/TypeScriptのSDKは公開日にPyPIへ。一か月以内にデザイン workshop を開く。

構図はこうだ。ツール層にMCP（Anthropic、2024年11月→2025年12月にLinux Foundationへ寄贈、月9700万ダウンロード、企業サーバー1万超）、エージェント間にA2A（Google、2025年4月、今年4月にv1.0、8月20日に同じ財団へ）。二層が同じ屋根の下に集った——**発見層は同じ週に分岐した**。MCPは`ai-catalog.json`を指し（形式はA2Aプロジェクトで議論中）、Poppyは`poppy.json`を義務づける。Poppyの賭けはこうだ。*個人*のエージェントの握手は*企業*のエージェントとは違う——ユーザー署名のセッション、匿名ID、scope付きトークン、主導権は常に顧客にある。35社が実装すれば、PoppyはMCP/A2A企業スタックの消費者ウェブの鏡になる。近くにはUCP（Universal Commerce Protocol。商業オペレーション層。カタログ/カート/チェックアウト）とACP（AGNTCYコレクティブのRESTネイティブなプロトコル）——プロトコルのジャングルが形成中だ。収束か分裂か、来年を見よ。

<svg viewBox="0 0 720 380" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="エージェントプロトコルの版図">
  <text x="360" y="32" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="18" font-weight="700" fill="#212529">プロトコル三層——ただし正面玄関は二つ</text>
  <rect x="60" y="70" width="180" height="90" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="150" y="100" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="16" font-weight="700" fill="#1864ab">MCP</text>
  <text x="150" y="124" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">エージェント ↔ ツール</text>
  <text x="150" y="144" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="13" fill="#868e96">Anthropic → Linux財団</text>
  <rect x="270" y="70" width="180" height="90" rx="10" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="360" y="100" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="16" font-weight="700" fill="#2b8a3e">A2A</text>
  <text x="360" y="124" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">エージェント ↔ エージェント</text>
  <text x="360" y="144" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="13" fill="#868e96">Google → Linux財団</text>
  <rect x="480" y="70" width="180" height="90" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2.5"/>
  <text x="570" y="100" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="16" font-weight="700" fill="#e67700">Poppy</text>
  <text x="570" y="124" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">個人 ↔ 企業</text>
  <text x="570" y="144" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="13" fill="#868e96">Sierra + Meta · 10月草案</text>
  <text x="360" y="200" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="15" font-weight="700" fill="#c92a2a">発見層が分岐 ⚠</text>
  <rect x="120" y="220" width="200" height="56" rx="8" fill="#f8f9fa" stroke="#adb5bd" stroke-width="2"/>
  <text x="220" y="244" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">/.well-known/ai-catalog.json</text>
  <text x="220" y="264" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="13" fill="#868e96">MCPルート</text>
  <rect x="400" y="220" width="200" height="56" rx="8" fill="#f8f9fa" stroke="#adb5bd" stroke-width="2"/>
  <text x="500" y="244" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">/.well-known/poppy.json</text>
  <text x="500" y="264" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="13" fill="#868e96">Poppyルート</text>
  <text x="360" y="316" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#212529">同じ問い——企業をどう発見するか——答えは二つ。</text>
  <text x="360" y="340" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#212529">収束するか分裂するか見ものだ。</text>
  <text x="360" y="368" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="13" fill="#868e96">図注：三層それぞれに主あり——発見層だけが分岐した。</text>
</svg>

## ヒット作：オープンソースが先勝

**OpenClaw**は今年のオープンソース現象だ。WhatsApp/Telegramから指揮し、ローカルゲートウェイでGmail、カレンダー、GitHub、ブラウザにつなぎ、MITライセンス。2025年11月に「Clawdbot」として登場し、72時間で10万スター、2026年3月に26.4万スターで**React超え**、10月には約39万——GitHub史上最速の伸びだ。作者Peter Steinbergerは2月にOpenAI入りし、プロジェクトは独立財団へ。中国で特に熱い。テンセント本社前に行列、有料インストールサービスまで。暗部もある。2月のCVE-2026-25253（CVSS 9.8、ワンクリックRCE）——エージェント安全の警鐘であり、「自分で組んだエージェントの責任は誰か」の第一課だ。

**Manus 2.0 + Cue**（9月28日）。「アプリではなくコンピュータを売る」——エージェントを常時起動のクラウドコンピュータとして包む。

**Instinct**（8月、招待制）。ユーザーごとに電話番号＋クラウドコンピュータを持ち、代わりに電話をかけ、友人のエージェントと「信頼できる人の網」を組む——エージェント間の社交が初めて製品の形になった。

**Nous Hermes**はオープンソースで2400万超のクローン、全世界のAIトークンの約2.5%。企業版を推進中だ。

**ElevenLabs**の音声エージェントは週1500万超の会話、2月の3倍、90超の言語。

**Lindy**（Slackネイティブのチームメイト）、**Granola**（会議記録、「邪魔しない」で勝った）、**Poke/Buzz**（エージェント間の委任網）——ロングテールは隙間だらけだ。

## 資本：「動ける」ものにだけ投じる

- **Manus：5億ドル超、評価額約40億ドル**（10月8日）——博裕＋IDGがリード、テンセントも参加。劇的な背景がある。Metaの20億ドル買収は北京に阻まれ、Manusは9月1日に独立を回復した。この調達自体が地政学のケースだ。
- **Instinct：10億ドルのシリーズC、評価額100億ドル**（9月28日）——Sequoia、Benchmark、Coatue。1か月前の評価額は25億ドルだった。今年の消費者エージェント最大のマークアップだ。
- **Nous Research：9000万ドルのシリーズB、評価額15億ドル**（10月7日）——Robot Venturesがリード。Nvidia、Samsung、USV、Menloが参加。年央のARRは約3600万ドル、年末に1億ドル超を狙う。
- **ElevenLabs：3億ドルのテンダー、評価額220億ドル**（9月30日）——半年で倍増。WellingtonとT. Rowe Priceが買う。

傾向は明確だ。資本は「動ける」消費者エージェントにだけ投じ、チャット窓には投じない。地政学（Manus/北京）が初めて評価額の一階の変数になった。

## 研究：基礎を打つ

**パーソナライズ**。PAHF（arXiv:2602.16173）。明示的な個人メモリ＋行動前確認・記憶 grounded 実行・行動後フィードバックの三段循環で、ユーザーの好みの漂いに追随し続ける。**持続エージェント**。115日の自己観察研究（arXiv:2605.26870）。トークン内訳の82.9%がキャッシュ読み——経済単位はトークン単価から**成果物単価**へ移っている。エージェント基盤を作る全員への価格信号だ。

**人格工学**。「温かさ×支配」の二次元で交渉エージェントの人格をパラメータ化（arXiv:2605.20554）。人格は「人生の出来事」で進化するが、現行エージェントは人間の人格動態の平均だけを模し、形を模していない（arXiv:2608.06485）。

**メタ推論**。MetaのThinking Before Thinking（arXiv:2609.38147）。「制御」そのものを拡張軸にする——エージェントが自律的なほど制御器が重要だ。

**評価の最前線**。SWE-bench Pro（1865題）、Terminal-Bench 2.x（最高92.8%、飽和間近）、τ-bench（対話下の信頼性）。2026年最大の教訓。**足場はモデルそのものに等しい**——同じモデルでもハーネス次第で17問違う。ベンチマークは消耗品で、賞味期限は短くなる一方だ。

## 展望：四つの線、各層への着想

**1. 界面の反転。** 人→エージェント→（エージェント網）→アプリ→現実世界。アプリはエージェントの「手」に退化する。
- **創業者へ**。「より良いアプリ」はもう作るな。エージェントが呼ぶ最初の「手」を作れ。垂直な実行者（予約、使い走り、税務、価格監視）がチャット窓より価値がある。Poppyの`poppy.json`があなたの出品説明書だ。先に書け。
- **研究者へ**。コールスタックが変わった。HCIの古典は全部やり直しだ。24時間働く代理人を人はどう監督するか。

**2. 所有の分裂。** ベンダー所有のエージェント（モデルも実行も記憶もベンダー）対ユーザー所有（OpenClaw/Hermes。実行と記憶はあなた、モデルは交換可能）。39万スターと2400万クローンはユーザーの足による投票だ。データ可搬性と記憶の所有権が主戦場だ。
- **個人へ**。今すぐ問え。私のエージェントの記憶は誰のものか。持ち出せるか。製品選びでは「記憶の書き出し」を硬い条件にせよ。
- **創業者へ**。「記憶銀行」を作れ。ベンダー間でユーザーのエージェント記憶を引っ越しさせ、通行料を取れ。

**3. 信頼が関門、能力ではない。** OpenAIのモデル撤回、OpenClawのRCE、MetaのSentinel——2026年の傷はすべて信頼だ。権限モデル、監査可能性、取消可能性が次の10倍の鍵だ。
- **インフラを作る人へ**。Poppyが開けたままの決済、監査、取消——一つひとつが創業の種だ。特にエージェントの支出。エスクローと上限——まともにできた者はいない。
- **研究者へ**。エージェント安全には新たな形式的手法が要る。CVE-2026-25253は始まりに過ぎない。

**4. ビジネスモデルは未定。** サブスク（Muse月20〜100ドル）、取引手数料、企業シート——眠っている間に働くエージェントのunit economicsを証明した者はいない。「成果物単価」（持続エージェント研究の結論）が答えかもしれない。
- **投資家へ**。DAUだけでなく純継続率と「睡眠中タスク完了率」を見よ。創業者への三つの問い。記憶は誰のものか。支出は誰が承認するか。壊れたら誰が払うか。

**議論：** あなたのエージェントが24時間あなたの人生を生きるとき、「あなた」と「それ」の境界はどこか。記憶の所有権を利用規約に書いた最初の会社が次世代を勝ち取るか？
