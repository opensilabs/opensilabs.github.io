---
lng_pair: id_20261016_muse_spark_open
title: "Muse Spark Open：一台桌子装得下的 816B 模型"
author: OpenSI-Labs
category: models
tags: [开放权重, 混合专家模型, Meta, 苹果, MLX]
date: 2026-10-16 06:00:00 -0700
img: /assets/img/posts/2026-10-16-muse-spark-open.png
meta_description: "Meta 发布 816B 参数开放权重模型，能在两台 Mac Studio 上本地运行——真正的故事是系统层面突破内存墙，以及一份有牙齿的许可证。"
---

10 月 15 日，Meta 公布了 Muse Spark Open 的权重：8160 亿参数、每 token 激活 420 亿、100 万 token 上下文——"迄今最强的美国开放权重模型"，Hugging Face 可下。[\[1\]](https://www.macrumors.com/2026/10/15/meta-muse-spark-open-mac-studio/) [\[2\]](https://particle.news/story/meta-releases-muse-spark-open-and-partners-with-apple-to-run-it-on-m5-ultra-macs)

但比权重更值得看的是那张桌子。Meta 与苹果合作针对 MLX 调优，演示了模型在两台 M5 Ultra Mac Studio 上运行——两台桌面电脑"像一台拥有 1TB 统一内存的超级计算机"。前沿模型本地运行，两年前不可想象。什么变了？

## 稀疏，遇上粗水管

8160 亿是营销数字，420 亿是工程数字。这是混合专家模型：每个 token，路由网络只唤醒约 5% 的"专家"子网络。像一座 8160 亿册藏书的图书馆，每个问题只进一条走廊。

<svg viewBox="0 0 640 220" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="混合专家稀疏激活示意图" style="width:100%;height:auto;display:block;margin:1em 0;">
  <text x="320" y="24" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui,-apple-system,'PingFang SC','Microsoft YaHei',sans-serif" fill="#1a1a1a">每个 token 只激活约 5% 的参数</text>
  <g font-family="system-ui,-apple-system,'PingFang SC','Microsoft YaHei',sans-serif">
    <rect x="40" y="60" width="560" height="70" rx="8" fill="#eef1f6" stroke="#c9d2e0"/>
    <text x="60" y="88" font-size="14" fill="#444">816B 总参数（全部专家）</text>
    <text x="60" y="112" font-size="14" fill="#444">未被路由到时保持休眠</text>
    <rect x="40" y="150" width="560" height="40" rx="8" fill="#dbe7ff" stroke="#7aa2f7"/>
    <rect x="40" y="150" width="29" height="40" rx="8" fill="#2f6df6"/>
    <text x="80" y="176" font-size="14" fill="#1a1a1a">每 token 激活 42B</text>
    <text x="470" y="176" font-size="14" fill="#555">路由器只挑一条走廊</text>
  </g>
</svg>
*图 1：稀疏激活——单 token 计算量停留在 42B 量级。*

稀疏性让内存账算得过来。低精度下 8160 亿参数约需 1TB 内存——苹果硬件登场：每台 M5 Ultra Studio 最高 512GB 统一内存，GPU 直接寻址，免去 CPU/GPU 拷贝税，带宽 1.2TB/s。两台凑 1TB。而每 token 只触及一小片参数，这个带宽喂得饱。稀疏模型、粗内存管道、无显存天花板：锁死 800B 模型的三道约束一次全松。

<svg viewBox="0 0 640 240" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="统一内存池化示意图" style="width:100%;height:auto;display:block;margin:1em 0;">
  <text x="320" y="24" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui,-apple-system,'PingFang SC','Microsoft YaHei',sans-serif" fill="#1a1a1a">两台桌面电脑，1TB 内存</text>
  <g font-family="system-ui,-apple-system,'PingFang SC','Microsoft YaHei',sans-serif">
    <rect x="40" y="50" width="220" height="110" rx="10" fill="#eef1f6" stroke="#c9d2e0"/>
    <text x="150" y="80" text-anchor="middle" font-size="14" font-weight="bold" fill="#1a1a1a">Mac Studio 1</text>
    <text x="150" y="106" text-anchor="middle" font-size="14" fill="#444">512GB 统一内存</text>
    <text x="150" y="130" text-anchor="middle" font-size="14" fill="#444">GPU 直接寻址</text>
    <rect x="380" y="50" width="220" height="110" rx="10" fill="#eef1f6" stroke="#c9d2e0"/>
    <text x="490" y="80" text-anchor="middle" font-size="14" font-weight="bold" fill="#1a1a1a">Mac Studio 2</text>
    <text x="490" y="106" text-anchor="middle" font-size="14" fill="#444">512GB 统一内存</text>
    <text x="490" y="130" text-anchor="middle" font-size="14" fill="#444">带宽 1.2TB/s</text>
    <path d="M260 105 L360 105" stroke="#2f6df6" stroke-width="3" marker-end="url(#arr)"/>
    <path d="M380 135 L280 135" stroke="#2f6df6" stroke-width="3" marker-end="url(#arr)"/>
    <defs><marker id="arr" markerWidth="8" markerHeight="8" refX="7" refY="4" orient="auto"><path d="M0,0 L8,4 L0,8 z" fill="#2f6df6"/></marker></defs>
    <rect x="180" y="185" width="280" height="36" rx="8" fill="#dbe7ff" stroke="#7aa2f7"/>
    <text x="320" y="209" text-anchor="middle" font-size="14" fill="#1a1a1a">1TB 内存池——装下整个 816B 模型</text>
  </g>
</svg>
*图 2：池化统一内存——两台 Studio 如一台机器。*

这是系统故事。训练算力抢头条，但用模型的瓶颈一直是内存墙。Muse Spark Open 的意义不在参数量，而在证明这堵墙正被两面夹击：模型更稀疏，内存更统一。

## 凉水

"开放权重"不等于"开源"。许可证要求显著标注"Built with Muse Spark Open"，年收入超 2000 万美元者提供服务前须通知 Meta 并签约。权重免费，Meta 对像样的部署保留知情和议价权——开放是分发策略：播生态、拿标准、留收费站。

还有两处伏笔。"最强*美国*开放权重"——Meta 基准显示代码弱于中国头部开放模型，前线已多极化。以及"桌面运行"等于两台 1 万美元以上的 Studio，512GB 版苹果还没开卖。桌面 AI 是真的，2 万美元门票也是真的。

但工程含金量不打折。百万上下文、42B 激活、智能体/工具调用强劲的 MoE 在池化统一内存上本地运行，是硬成就。苹果与 Meta 的媾和（"爸爸妈妈又和好了"——Alexandr Wang）本身也是信号：两家都想要前沿 AI 不必跑在英伟达栈上的未来。

**讨论：** 权重开放、许可留控制权、硬件 2 万美元——这个"开放"到底给谁？你会因此换种方式用它吗？
