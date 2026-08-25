# SD Hub manifest 规范（v8.26 中台）

每个项目一个目录 `p/<sdid>/`，内含 `manifest.json` + `img/`（原图 jpg）+ `th/`（480px 缩略图 jpg）。

## manifest.json
```json
{
  "id": "sd003",
  "zh": "纹身之神",
  "vi": "Thần Hình Xăm",
  "groups": [
    {"id": "g1", "zh": "Minh · 面部", "vi": "Minh · Gương mặt", "cat": "face", "divider": "人物 · Nhân vật"},
    {"id": "g2", "zh": "Minh · 校服造型", "vi": "Minh · Đồng phục", "cat": "costume"}
  ],
  "items": [
    {"n": 1, "name": "Minh-2", "file": "img/img-001.jpg", "thumb": "th/img-001.jpg", "w": 1024, "h": 1536, "group": "g1"}
  ],
  "locked": {}
}
```

## 字段规则
- `cat` 仅四种：`face`（面部/长相，Dennis 选）、`costume`（服装/造型/状态版）、`scene`（场景）、`prop`（道具）。
- `divider`：该组渲染前显示的分区标题（如「场景 · Bối cảnh」），只在该分区第一组出现。
- `name`：以 `-数字` 结尾会被自动显示为「方案 N / Phương án N」；不以数字结尾则原样显示。
- 单图组（items 只有 1 个）自动变成「同意/不同意+理由」投票组。
- 多视图：item 可加 `extra/ew/eh`（副图）+ `flab/xlab`（图注）。
- `locked`：`{"g3": {"type":"pick","item":7,"note":"Dennis 已选定"}}` 或 `{"type":"vote","agree":true,"note":"..."}`。锁定组在 Dennis 页只读展示，在 YGVN 页完全不出现。
- 图片处理：原图转 jpg（q90，最长边≤1600，PNG 白底不裁切），缩略图 `sips -Z 480 q72`；文件名统一 `img-NNN.jpg` 顺序编号。
- 越文必须准确，专名保留原文（如 Minh、Thảo）；写完用码点检查 `'ng\u01b0\u1eddii' not in json_str`（这是错误拼写）。
