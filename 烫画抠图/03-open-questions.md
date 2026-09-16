# 待验证清单

## 必须验证
1. ag-psd 的 LICENSE 原文是否允许商用
2. vtracer 是否支持按色层分层输出
3. vtracer 输出格式（SVG / 其他）
4. ag-psd 的 `type: 'vector'` + `linkedFiles` 实际能否在 Photoshop 中双击编辑

## 已拍板
1. 矢量化主方案：vtracer
2. PSD 生成方案：ag-psd（待 license 确认）
3. 白墨 MVP：自研简单版
4. 输入优先级：透明 PNG > 高清 JPG
5. 后端语言：Python（或 Node，取决于团队）