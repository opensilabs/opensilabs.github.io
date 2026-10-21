---
lng_pair: id_20261020_dream1-robot-brain
title: "1時間3ドル、ロボットに脳をレンタルする"
author: OpenSI-Labs
category: robotics
tags: [ロボティクス, 基盤モデル, ワールドモデル, ロボットAPI, Dream Labs]
date: 2026-10-20 03:30:00 -0700
img: /assets/img/posts/2026-10-20-dream-1-robot-brain.png
meta_description: "Dream LabsのDream-1は人間の動画をレンタル可能なロボットの脳に変える。1時間3ドル、未知のロボットにもゼロショット対応——規模ではなく普及に賭ける一手。"
---
ペットボトル1本分の3ドルで、2026年10月19日からロボットの「脳」が1時間レンタルできる。

元NVIDIA・GR00TのJoel Jangらが興したDream Labsが9,000万ドルのシードでステルスから出た。目玉はロボット基盤モデル初の公開API「Dream API」——カメラ映像と指示を送ればモーター指令が返る。

肝は「ワールド・アクション・モデル」だ。人間の映像から「次に何が起こるか」を予測して行動を導く。出力の目標姿勢を逆運動学ソルバが関節指令に翻訳する。前作DreamZeroは30分の「遊び」で新ロボットに適応済み。

<svg viewBox="0 0 720 372" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Dream-1の仕組み：人間の一人称視点映像で訓練したワールド・アクション・モデルが次のフレームを予測しロボットの動作を出力する">
  <defs>
    <marker id="jaf1a" markerWidth="10" markerHeight="10" refX="8" refY="3" orient="auto"><path d="M0,0 L8,3 L0,6 Z" fill="#6b5f45"/></marker>
  </defs>
  <rect x="16" y="30" width="190" height="252" rx="12" fill="#faf6ec" stroke="#8a7d5c" stroke-width="2"/>
  <text x="111" y="60" text-anchor="middle" font-size="17" font-weight="bold" fill="#3a3226">人間の一人称視点映像</text>
  <rect x="36" y="74" width="150" height="54" rx="6" fill="#ffffff" stroke="#8a7d5c" stroke-width="1.5"/>
  <rect x="86" y="86" width="50" height="30" rx="3" fill="#dfe9f5" stroke="#5b7ba6" stroke-width="1.5"/>
  <line x1="111" y1="86" x2="111" y2="116" stroke="#5b7ba6" stroke-width="1.5" stroke-dasharray="4,3"/>
  <rect x="36" y="138" width="150" height="54" rx="6" fill="#ffffff" stroke="#8a7d5c" stroke-width="1.5"/>
  <rect x="86" y="150" width="50" height="30" rx="3" fill="#dfe9f5" stroke="#5b7ba6" stroke-width="1.5"/>
  <rect x="86" y="150" width="25" height="30" rx="3" fill="#b9cfe8" stroke="#5b7ba6" stroke-width="1.5"/>
  <rect x="36" y="202" width="150" height="54" rx="6" fill="#ffffff" stroke="#8a7d5c" stroke-width="1.5"/>
  <rect x="96" y="212" width="30" height="34" rx="3" fill="#b9cfe8" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="111" y="274" text-anchor="middle" font-size="14" fill="#5c5340">洗濯物をたたむ · 荷造り · 片付け</text>
  <line x1="210" y1="156" x2="244" y2="156" stroke="#6b5f45" stroke-width="2.5" marker-end="url(#jaf1a)"/>
  <rect x="250" y="30" width="220" height="252" rx="12" fill="#f2f6fb" stroke="#5b7ba6" stroke-width="2"/>
  <text x="360" y="60" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c3e55">ワールド・アクション・モデル</text>
    <line x1="300" y1="100" x2="360" y2="85" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="100" x2="360" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="100" x2="360" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="100" x2="360" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="100" x2="360" y2="205" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="130" x2="360" y2="85" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="130" x2="360" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="130" x2="360" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="130" x2="360" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="130" x2="360" y2="205" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="160" x2="360" y2="85" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="160" x2="360" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="160" x2="360" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="160" x2="360" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="160" x2="360" y2="205" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="190" x2="360" y2="85" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="190" x2="360" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="190" x2="360" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="190" x2="360" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="190" x2="360" y2="205" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="85" x2="420" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="85" x2="420" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="85" x2="420" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="115" x2="420" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="115" x2="420" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="115" x2="420" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="145" x2="420" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="145" x2="420" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="145" x2="420" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="175" x2="420" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="175" x2="420" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="175" x2="420" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="205" x2="420" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="205" x2="420" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="205" x2="420" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <circle cx="300" cy="100" r="7" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="300" cy="130" r="7" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="300" cy="160" r="7" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="300" cy="190" r="7" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="360" cy="85" r="7" fill="#dfe9f5" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="360" cy="115" r="7" fill="#dfe9f5" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="360" cy="145" r="7" fill="#dfe9f5" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="360" cy="175" r="7" fill="#dfe9f5" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="360" cy="205" r="7" fill="#dfe9f5" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="420" cy="115" r="7" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="420" cy="145" r="7" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="420" cy="175" r="7" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="360" y="274" text-anchor="middle" font-size="14" fill="#3d4f68">予測：次に何が起こるか？</text>
  <line x1="474" y1="156" x2="508" y2="156" stroke="#6b5f45" stroke-width="2.5" marker-end="url(#jaf1a)"/>
  <rect x="514" y="30" width="190" height="252" rx="12" fill="#f3faf3" stroke="#4e7d4e" stroke-width="2"/>
  <text x="609" y="60" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c442c">ロボットの動作</text>
  <rect x="584" y="198" width="50" height="14" rx="4" fill="#9db89d"/>
  <line x1="609" y1="198" x2="609" y2="152" stroke="#4e7d4e" stroke-width="6" stroke-linecap="round"/>
  <circle cx="609" cy="152" r="7" fill="#4e7d4e"/>
  <line x1="609" y1="152" x2="648" y2="122" stroke="#4e7d4e" stroke-width="6" stroke-linecap="round"/>
  <line x1="648" y1="122" x2="658" y2="106" stroke="#4e7d4e" stroke-width="4" stroke-linecap="round"/>
  <line x1="648" y1="122" x2="664" y2="114" stroke="#4e7d4e" stroke-width="4" stroke-linecap="round"/>
  <rect x="648" y="192" width="30" height="20" rx="3" fill="#e8d9b8" stroke="#8a7d5c" stroke-width="1.5"/>
  <text x="609" y="250" text-anchor="middle" font-size="14" fill="#33502f">目標グリッパー姿勢</text>
  <text x="609" y="272" text-anchor="middle" font-size="14" fill="#33502f">→ 逆運動学 → 関節指令</text>
  <text x="360" y="322" text-anchor="middle" font-size="14" fill="#6b5f45">訓練データは人間の動画、特定ロボットの遠隔操作データではない</text>
  <text x="360" y="346" text-anchor="middle" font-size="14" font-weight="bold" fill="#3a3226">——ハードを越えて転移する鍵</text>
</svg>
図1：人間の観察がロボットの行動になる。

訓練外の27台をゼロショットで操縦し、18年前のPR2も動かした。Robocurveでは59対48で勝ち、コストは16分の1（同社発表）。

<svg viewBox="0 0 720 400" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="対比：旧来型は1台ごとに特注の脳、Dream-1は1つの脳が多くの身体を動かす">
  <rect x="16" y="30" width="320" height="332" rx="12" fill="#faf6ec" stroke="#8a7d5c" stroke-width="2"/>
  <text x="176" y="62" text-anchor="middle" font-size="18" font-weight="bold" fill="#3a3226">旧来型：1台に1つの脳</text>
    
  <rect x="63" y="286" width="26" height="9" rx="3" fill="#c9bfa8"/>
  <line x1="76" y1="286" x2="76" y2="252" stroke="#8a7d5c" stroke-width="5" stroke-linecap="round"/>
  <line x1="76" y1="252" x2="67" y2="240" stroke="#8a7d5c" stroke-width="3.5" stroke-linecap="round"/>
  <line x1="76" y1="252" x2="85" y2="240" stroke="#8a7d5c" stroke-width="3.5" stroke-linecap="round"/>
  <circle cx="76" cy="224" r="14" fill="#f3e2c7" stroke="#b07a3f" stroke-width="2"/>
  <path d="M 69,224 q 3,-6 7,0 t 7,0" stroke="#b07a3f" stroke-width="1.8" fill="none"/>
    
  <rect x="163" y="286" width="26" height="9" rx="3" fill="#c9bfa8"/>
  <line x1="176" y1="286" x2="176" y2="252" stroke="#8a7d5c" stroke-width="5" stroke-linecap="round"/>
  <line x1="176" y1="252" x2="167" y2="240" stroke="#8a7d5c" stroke-width="3.5" stroke-linecap="round"/>
  <line x1="176" y1="252" x2="185" y2="240" stroke="#8a7d5c" stroke-width="3.5" stroke-linecap="round"/>
  <circle cx="176" cy="224" r="14" fill="#f3e2c7" stroke="#b07a3f" stroke-width="2"/>
  <path d="M 169,224 q 3,-6 7,0 t 7,0" stroke="#b07a3f" stroke-width="1.8" fill="none"/>
    
  <rect x="263" y="286" width="26" height="9" rx="3" fill="#c9bfa8"/>
  <line x1="276" y1="286" x2="276" y2="252" stroke="#8a7d5c" stroke-width="5" stroke-linecap="round"/>
  <line x1="276" y1="252" x2="267" y2="240" stroke="#8a7d5c" stroke-width="3.5" stroke-linecap="round"/>
  <line x1="276" y1="252" x2="285" y2="240" stroke="#8a7d5c" stroke-width="3.5" stroke-linecap="round"/>
  <circle cx="276" cy="224" r="14" fill="#f3e2c7" stroke="#b07a3f" stroke-width="2"/>
  <path d="M 269,224 q 3,-6 7,0 t 7,0" stroke="#b07a3f" stroke-width="1.8" fill="none"/>
  <text x="176" y="326" text-anchor="middle" font-size="14" fill="#5c5340">1台ずつ個別に訓練</text>
  <text x="176" y="348" text-anchor="middle" font-size="14" fill="#5c5340">専門家が数か月調整、新ハードではゼロから</text>
  <rect x="384" y="30" width="320" height="332" rx="12" fill="#f2f6fb" stroke="#5b7ba6" stroke-width="2"/>
  <text x="544" y="62" text-anchor="middle" font-size="18" font-weight="bold" fill="#2c3e55">Dream-1：1つの脳、多くの身体</text>
  <circle cx="544" cy="128" r="46" fill="#ffe9a8" opacity="0.45"/>
  <circle cx="544" cy="128" r="32" fill="#fff3d6" stroke="#c9962e" stroke-width="2.5"/>
  <path d="M 522,128 q 5,-9 11,0 t 11,0 t 11,0" stroke="#c9962e" stroke-width="2" fill="none"/>
  <path d="M 526,140 q 5,-8 10,0 t 10,0" stroke="#c9962e" stroke-width="2" fill="none"/>
  <line x1="544" y1="162" x2="430" y2="222" stroke="#c9962e" stroke-width="1.5" stroke-dasharray="5,4"/>
  <line x1="544" y1="162" x2="498" y2="222" stroke="#c9962e" stroke-width="1.5" stroke-dasharray="5,4"/>
  <line x1="544" y1="162" x2="590" y2="222" stroke="#c9962e" stroke-width="1.5" stroke-dasharray="5,4"/>
  <line x1="544" y1="162" x2="658" y2="222" stroke="#c9962e" stroke-width="1.5" stroke-dasharray="5,4"/>
    
  <rect x="419" y="266" width="22" height="8" rx="3" fill="#5b7ba6" opacity="0.55"/>
  <line x1="430" y1="266" x2="430" y2="238" stroke="#5b7ba6" stroke-width="5" stroke-linecap="round"/>
  <line x1="430" y1="238" x2="422" y2="228" stroke="#5b7ba6" stroke-width="3.5" stroke-linecap="round"/>
  <line x1="430" y1="238" x2="438" y2="228" stroke="#5b7ba6" stroke-width="3.5" stroke-linecap="round"/>
    
  <rect x="487" y="266" width="22" height="8" rx="3" fill="#4e7d4e" opacity="0.55"/>
  <line x1="498" y1="266" x2="498" y2="238" stroke="#4e7d4e" stroke-width="5" stroke-linecap="round"/>
  <line x1="498" y1="238" x2="490" y2="228" stroke="#4e7d4e" stroke-width="3.5" stroke-linecap="round"/>
  <line x1="498" y1="238" x2="506" y2="228" stroke="#4e7d4e" stroke-width="3.5" stroke-linecap="round"/>
    
  <rect x="579" y="266" width="22" height="8" rx="3" fill="#b07a3f" opacity="0.55"/>
  <line x1="590" y1="266" x2="590" y2="238" stroke="#b07a3f" stroke-width="5" stroke-linecap="round"/>
  <line x1="590" y1="238" x2="582" y2="228" stroke="#b07a3f" stroke-width="3.5" stroke-linecap="round"/>
  <line x1="590" y1="238" x2="598" y2="228" stroke="#b07a3f" stroke-width="3.5" stroke-linecap="round"/>
    
  <rect x="647" y="266" width="22" height="8" rx="3" fill="#8a5f9e" opacity="0.55"/>
  <line x1="658" y1="266" x2="658" y2="238" stroke="#8a5f9e" stroke-width="5" stroke-linecap="round"/>
  <line x1="658" y1="238" x2="650" y2="228" stroke="#8a5f9e" stroke-width="3.5" stroke-linecap="round"/>
  <line x1="658" y1="238" x2="666" y2="228" stroke="#8a5f9e" stroke-width="3.5" stroke-linecap="round"/>
  <text x="544" y="312" text-anchor="middle" font-size="14" fill="#3d4f68">未知のロボット27台（シミュレーションでゼロショット）</text>
  <text x="544" y="336" text-anchor="middle" font-size="14" fill="#3d4f68">18年前のPR2も含む · 1時間3ドルの従量課金</text>
</svg>
図2：1つの脳が多くの身体を動かす時代へ。

1時間3ドル、1回1.6秒分の動作で1時間約2,250回、1動作0.0013ドル。ハードも2,000ドル台から。

業界の隘路はデータだ。1作業に専門家が数か月かかる。その不足を人間の動画で埋めるのがDreamの賭けだ。

賭けは「規模ではなく普及」だ。競合は大型化に巨額を投じる。Dream Labsは9,000万ドルにとどめ、知能をAPIで従量課金する。

ただし研究ベータ版だ。「ミスはする」。双腕＋グリッパーの机上作業に限り、移動や器用なハンドはロードマップ上。資金の大半は計算資源に。

脳を時間貸しする時代、ロボットの価値は「手」か「心」か——ミスしたら誰が負うのか。
