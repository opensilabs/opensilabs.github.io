---
lng_pair: id_20261010_photonic-ai-computing
title: "光でできたコンピュータ"
author: OpenSI-Labs
category: chips
tags: [フォトニックコンピューティング, 光ニューラルネットワーク, 省エネルギー, コチ大学, ハードウェア]
date: 2026-10-10 06:00:00 -0700
img: /assets/img/posts/2026-10-10-photonic-ai-computing.png
meta_description: "トルコ・コチ大学の2つの新研究が、AI計算を光そのものの中で実現した。色を捨てないフォトニックニューラルネットワークと、レーザー共振器自体を非線形プロセッサにするシステム。"
---

あなたが使ったAIは例外なく電子で「考えて」きた。数十億のトランジスタが開閉し、そのたびにエネルギーを燃やして熱として捨てる。業界の答えは「大きく作る」こと——クラスタも電力契約も巨大化し、小さな町ひとつ分の電気があなたの質問ひとつのために使われる。

コチ大学Uğur Teğin研究室（イスタンブール）の2つの新研究は問いを変えた。光子で考えたらどうなるか、と。光は複数の情報流を同時に運べ、「計算」はほぼタダだ。ひとつは『Communications Engineering』の色を捨てないフォトニックニューラルネットワーク、もうひとつは『Communications Physics』のファイバーレーザーをプロセッサにする研究。[今週のまとめ報道](https://techxplore.com/news/2026-10-approach-sustainable-ai-offloading-burden.html)が両者を並べ、まったく異なるAIハードウェア哲学を描き出した。

## 色を捨てるな

一見些細で、勘定すると恐ろしい事実から始めよう。ほとんどの画像分類器は情報を捨てることから始める——赤・緑・青を1つのグレーに潰すのだ。だが色は信号だ。皮膚病変の診断は微妙な赤みに懸かり、衛星画像の意味は緑の中にあるかもしれない。

KılınçとTeğinのシステムはこの近道を拒否する。画像は光の伝搬を制御するデバイスに符号化され、位相マスクの積層（多平面光変換）が3チャンネルを連れ立って進ませながら混合・変換。通過の過程で、画像を区別する特徴——色、形、質感——が物理的に強調される。カメラが光パターンを記録し、分類器がカテゴリを読み取る。

数字は鮮烈だ。皮膚疾患の分類精度は生ピクセルの68%から光学前処理後の**98%**へ。医用画像、自然画像、回帰タスクで光学前処理は基準より25〜45ポイント上回り、「RGBを潰さない」だけで6〜11ポイントの上乗せがあった（[論文](https://www.nature.com/articles/s44172-026-00762-w)）。

<svg viewBox="0 0 720 470" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="マルチチャンネル光コンピューティングの流れ：RGBの3チャンネルを位相マスクに符号化し、光の伝搬で変換、カメラで読み取る">
  <defs>
    <marker id="arrP" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">マルチチャンネル光コンピューティング：色は最後まで残る</text>
  <rect x="30" y="50" width="150" height="70" rx="10" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="105" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#a61e4d">RGB画像の入力</text>
  <text x="105" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">3チャンネルを保持</text>
  <rect x="30" y="140" width="150" height="26" rx="6" fill="#f8f9fa" stroke="#adb5bd"/>
  <text x="105" y="157" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">グレースケール化しない</text>
  <line x1="180" y1="85" x2="225" y2="85" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrP)"/>
  <rect x="225" y="50" width="170" height="70" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="310" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#1864ab">位相マスク群</text>
  <text x="310" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">多平面光変換</text>
  <line x1="395" y1="85" x2="440" y2="85" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrP)"/>
  <rect x="440" y="50" width="150" height="70" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="515" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#e67700">光の伝搬変換</text>
  <text x="515" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">特徴を光学的に強調</text>
  <line x1="590" y1="85" x2="620" y2="85" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrP)"/>
  <rect x="620" y="50" width="80" height="70" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="660" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" font-weight="700" fill="#5f3dc4">カメラ</text>
  <text x="660" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">+分類器</text>
  <rect x="120" y="200" width="480" height="120" rx="10" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="360" y="228" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#2b8a3e">自己最適化ループ</text>
  <text x="360" y="252" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">実験測定から直接学ぶ——完璧なシミュレータは不要</text>
  <text x="360" y="274" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">ベイズ最適化（チャンネル混合）＋ハードウェア・イン・ザ・ループ</text>
  <text x="360" y="296" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">自己組織化臨界（位相設定）——組立誤差に自動適応</text>
  <line x1="310" y1="120" x2="310" y2="195" stroke="#2b8a3e" stroke-width="2" stroke-dasharray="6,4" marker-end="url(#arrP)"/>
  <rect x="225" y="350" width="270" height="70" rx="10" fill="#ffffff" stroke="#212529" stroke-width="2"/>
  <text x="360" y="378" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#212529">皮膚疾患分類：68% → 98%</text>
  <text x="360" y="400" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">自己最適化でさらに7〜12ポイント上乗せ</text>
  <text x="360" y="448" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#868e96">図注：RGBの3チャンネルが連れ立ってプログラマブルな位相マスクを通過。実機に合わせて自己調整する。</text>
</svg>

## 学ぶのはデバイスそのもの、シミュレーションではない

重要なのは精度の数字ではない。光ニューラルネットワークには「墓場問題」がある。シミュレーションでは美しいのに、実験室では死ぬ。ズレ、誤差、ドリフト——物理デバイスは理想モデルと決して一致せず、そのギャップが性能を食い尽くす。

Teğinのチームは問題をひっくり返した。完璧なシミュレータの代わりに、実験測定から直接学ぶ。2つの相補戦略は微分可能な順方向モデルを使わない。ベイズ最適化が入力のチャンネル混合を整え、自己組織化臨界のハードウェア・イン・ザ・ループが高次元の位相設定を探索する。機械は自分のハードウェアの癖を学び適応する——不完全さは学習対象の一部だ。この自己最適化がさらに7〜12ポイントを積み増した。

電子工学は60年かけて公差を締め上げてきた——ナノからオングストロームへ。これは逆方向の賭けだ。不完全な物理でコンピュータを作り、物理にアルゴリズムを教えさせる。まったく異なるハードウェア哲学であり、ベンチマーク表の外でも注目される理由だ。

## 考えるレーザー

2つ目の研究はさらに奇妙で、ある意味もっとラディカルだ。Eşlik、Kesgin、Kılınç、Teğinは連続波マルチモードファイバーレーザーの共振器自体をプロセッサにした。入力画像は空間光変調器に位相パターンとして書き込まれ、光は共振器内を循環する。マルチモード干渉と利得飽和が高次元非線形変換へとかき混ぜ、安定した強度パターンを出す。クラスはすでに分離され、単純な線形分類器が仕上げるだけだ。

非線形マッピングをGPUは実行していない。物理がやったのだ。リサイクルごみ、気象・衛星画像、網膜スキャン、皮膚病変で**85〜99%**を達成し、学習可能パラメータは従来の深層ネットより桁違いに少ない（[論文](https://www.nature.com/articles/s42005-026-02823-0)）。

<svg viewBox="0 0 720 400" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="ファイバーレーザー共振器を非線形光プロセッサに：位相符号化された画像がレーザーのダイナミクスで分離可能なパターンに変換される">
  <defs>
    <marker id="arrQ" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">レーザー共振器自体がプロセッサ</text>
  <rect x="20" y="60" width="130" height="70" rx="10" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="85" y="88" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#a61e4d">画像の入力</text>
  <text x="85" y="108" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">ごみ、衛星、網膜…</text>
  <line x1="150" y1="95" x2="190" y2="95" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrQ)"/>
  <rect x="190" y="60" width="140" height="70" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="260" y="88" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#1864ab">空間光変調器</text>
  <text x="260" y="108" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">位相パターン符号化</text>
  <line x1="330" y1="95" x2="370" y2="95" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrQ)"/>
  <rect x="370" y="50" width="200" height="90" rx="40" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="470" y="80" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#e67700">ファイバーレーザー共振器</text>
  <text x="470" y="100" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">マルチモード干渉</text>
  <text x="470" y="118" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">＋利得飽和</text>
  <line x1="570" y1="95" x2="610" y2="95" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrQ)"/>
  <rect x="610" y="60" width="90" height="70" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="655" y="88" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" font-weight="700" fill="#5f3dc4">線形</text>
  <text x="655" y="106" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" font-weight="700" fill="#5f3dc4">分類器</text>
  <rect x="190" y="180" width="380" height="80" rx="10" fill="#ffffff" stroke="#212529" stroke-width="2"/>
  <text x="380" y="210" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#212529">精度 85〜99%</text>
  <text x="380" y="232" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">学習可能パラメータは深層ネットより桁違いに少ない</text>
  <text x="380" y="252" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">——レーザーのダイナミクスが隠れ層を置き換えた</text>
  <text x="360" y="310" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#212529">要点：非線形マッピングはタダだ</text>
  <text x="360" y="334" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">デジタルネットでは、非線形性は行列積とメモリ転送のコスト。</text>
  <text x="360" y="354" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">共振器の中では、それは光が通過するときに本来することだ。</text>
  <text x="360" y="386" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#868e96">図注：入力画像は位相パターンに。レーザー自身のダイナミクスが非線形計算を行う。</text>
</svg>

## 正直な損益計算

2つ釘を刺す。このジャーナルは誇大広告をしない。第一に、どちらも純粋な光ではない。書き込みに空間光変調器、読み取りにカメラ、最適化に制御ユニット——両端はまだ電子だ。正直な問いは、総作業量の何割を光が引き受けられるか。今は最も重い中間部を担い、両端は電子のまま。高速光変調器とチップ集積フォトニクスがどこまで押し上げられるかは、未解決の賭けだ。

第二に、これは概念実証のスケールで、データセンターの置き換えではない。来年ファイバーレーザーの中で最先端モデルを学習する者はいない。

だが方向は正しく、タイミングも重要だ。AI推論は物理的限界にぶつかっている——電力、発熱、メモリとプロセッサ間のデータ転送コスト。そのどれもが電子の属性だ。フォトニクスはそれらを回避するだけでなく、いちばん硬い限界を反転させる。電子が完璧さを製造コストで払うところ、フォトニクスは手元のデバイスを学べる。物理に逆らうのではなく、物理とともに計算するのだ。

1980年代も光コンピュータを夢見て、プログラマビリティと適応性で敗れた。足りなかったピースはより良い光学ではなかったらしい。光学に自分自身を学ばせることだったのだ。

**議論：** 未来のAIハードウェアが完璧な製造の代わりに自分自身の物理基板の不完全さを学ぶようになったら、チップ製造の経済はどう書き換えられるか——「そこそこ良い物理」が「完璧なシリコン」に勝つとき、勝者は誰か。
