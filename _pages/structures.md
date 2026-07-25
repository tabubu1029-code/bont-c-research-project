---
layout: page
title: 結構展示區 🧬
permalink: /structures/
nav: true
nav_order: 2
---

歡迎來到 3D 結構展示區！這裡展示的是肉毒桿菌毒素 C 型 (BoNT/C) 的立體結構。
你可以直接使用滑鼠左鍵拖曳來**旋轉**模型，或是使用滑鼠滾輪來**放大/縮小**。

<!-- 載入 3Dmol.js 核心函式庫 -->
<script src="https://3Dmol.csb.pitt.edu/build/3Dmol-min.js"></script>

<!-- 建立 3D 檢視器容器，使用 BoNT/C 的公開 PDB ID (3R4S) 作為示範 -->
<div style="height: 500px; width: 100%; position: relative;"
     class="viewer_3Dmoljs"
     data-pdb="3R4S"
     data-backgroundcolor="0xf4f4f4"
     data-style="cartoon:color=spectrum">
</div>
