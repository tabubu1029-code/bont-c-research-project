---
layout: page
title: 結構展示區 🧬
permalink: /structures/
nav: true
nav_order: 2
---

歡迎來到 3D 結構展示區！這裡展示的是肉毒桿菌毒素 C 型 (BoNT/C) 的立體結構。
你可以直接使用滑鼠左鍵拖曳來**旋轉**模型，或是使用滑鼠滾輪來**放大/縮小**。

點擊下方的按鈕，即可自動聚焦並用特定顏色標記出關鍵的受體結合區 (RBD) 與鍵結特徵：

<!-- 互動按鈕區 -->
<div style="margin-top: 15px; margin-bottom: 15px; display: flex; flex-wrap: wrap; gap: 8px;">
  <button class="btn btn-sm btn-outline-danger" onclick="focusResidues(['1251-1260'], 'red')">GBL 迴圈</button>
  <button class="btn btn-sm btn-outline-warning" onclick="focusResidues(['1258','1259'], 'purple')">WY-loop</button>
  <button class="btn btn-sm btn-outline-success" onclick="focusResidues(['933','979','981','1015','1075'], 'orange')">疏水口袋</button>
  <button class="btn btn-sm btn-outline-info" onclick="focusResidues(['935','961','968','1043'], 'blue')">親水口袋</button>
  <button class="btn btn-sm btn-outline-primary" onclick="focusResidues(['1127','1255'], 'green')">鹽橋</button>
  <button class="btn btn-sm btn-outline-secondary" onclick="focusResidues(['1145','1185','1186','1202','1251'], 'cyan')">離子鍵結</button>
  <button class="btn btn-sm btn-outline-dark" onclick="focusResidues(['1151','1169','1171','1180','1206-1210','1214'], 'magenta')">Sia 結合區</button>
  <button class="btn btn-sm btn-outline-dark" onclick="focusResidues(['1125-1130','1146','1174','1175','1179','1203','1255'], 'gold')">Slb 結合區</button>
  <button class="btn btn-sm btn-primary" onclick="resetView()">重置全景</button>
</div>

<!-- 3D 檢視器視窗 -->
<div id="gldiv" style="height: 500px; width: 100%; position: relative; border: 1px solid #ddd; border-radius: 8px;"></div>

<!-- 載入 jQuery 與 3Dmol.js -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
<script src="https://3Dmol.csb.pitt.edu/build/3Dmol-min.js"></script>

<script>
  let viewer = null;

  $(document).ready(function() {
    let element = $('#gldiv');
    let config = { backgroundColor: '#f4f4f4' };
    viewer = $3Dmol.createViewer( element, config );

    // 讀取你上傳在 GitHub 專案裡的 PDB 檔案
    let pdbUri = 'https://tabubu1029-code.github.io/bont-c-research-project/bontc_complex.pdb';

    $.ajax(pdbUri, {
      success: function(data) {
        viewer.addModel(data, "pdb");
        viewer.setStyle({}, {cartoon: {color: '#cccccc'}}); // 預設全部顯示淺灰色
        viewer.zoomTo();
        viewer.render();
      },
      error: function() {
        console.error("無法載入 PDB 檔案，請確認檔案是否已成功上傳！");
      }
    });
  });

  // 點擊按鈕後觸發的聚焦函式
  function focusResidues(resiArray, highlightColor) {
    if(!viewer) return;
    
    // 1. 先將所有結構恢復成淺灰色背景
    viewer.setStyle({}, {cartoon: {color: '#cccccc'}});
    
    // 2. 針對目標殘基，設定鮮豔顏色並疊加立體的球棒模型 (stick)
    viewer.setStyle({resi: resiArray}, {
        cartoon: {color: highlightColor},
        stick: {radius: 0.3, color: highlightColor}
    });
    
    // 3. 將鏡頭平滑拉近到目標區域 (動畫時間 1000 毫秒)
    viewer.zoomTo({resi: resiArray}, 1000);
    viewer.render();
  }

  // 重置全景的函式
  function resetView() {
    if(!viewer) return;
    viewer.setStyle({}, {cartoon: {color: '#cccccc'}});
    viewer.zoomTo(1000);
    viewer.render();
  }
</script>
