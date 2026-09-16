# 烫画软件 — 技术栈选型结论

## 输入输出定义
- 输入：透明 PNG / 高清 JPG
- 输出：分层 PSD，每个色块独立矢量智能对象 + 独立白墨图层
- 当前范围：平面文件快速通道，不做衣服照片去褶皱

## 已确认的技术选型

### 矢量化：vtracer（主方案），Trazor（参考）
- vtracer 1.0：7036 stars，Rust 核心 + 多语言绑定，MIT
- Trazor：51 stars，TypeScript，算法参考
- 两者实现相同的 seam-free cutout 算法
- **待验证**：vtracer 是否支持按色层分层输出，还是只能输出单张合并 SVG

### PSD 生成：ag-psd（待 license 确认）
- 可创建矢量智能对象：`type: 'vector'` + SVG 数据放入 `linkedFiles`
- 无需 Photoshop 运行
- **风险**：license 为 NOASSERTION，需人工确认 LICENSE 原文

### 白墨层：自研简单版（MVP）
- MVP 逻辑：彩色层并集 + 膨胀 3px + 羽化 1px
- OpenRIP 作为算法参考，不引入 CMYK 管线
- **风险**：OpenRIP 白墨输入是 CMYK 而非 RGB alpha

### 色彩聚类：LAB + K-means + CIEDE2000
- 初始聚类数 15-20，最小面积过滤 200px
- 参考 Layerdivider 的实现路线

### 边缘清理：Alpha 阈值截断 + 形态学处理
- Alpha 阈值 0.5，先腐蚀再膨胀
- 半透明像素不参与聚类

## License 状态
| 项目 | License | 商用风险 |
|---|---|---|
| vtracer | MIT | 低 |
| Trazor | MIT | 低 |
| ag-psd | NOASSERTION | **待确认** |
| OpenRIP | MIT | 低 |
| PhotoshopAPI | BSD-3-Clause | 低 |
| reveal | Apache-2.0 | 低 |