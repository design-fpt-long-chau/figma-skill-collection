# Skill: Tạo slide mới từ slide template
---
name: long-chau-slide
description: Tạo slide mới theo template Nhà Thuốc Long Châu — clone đúng layout từ file template, dùng đúng component/token/style có sẵn, chỉ edit text và image content
created-by: TrongPD3 (trongpd3@fpt.com)
created-in: Figma AI Agent — FPT Long Châu workspace
last-updated: 2026-07-01
---

# Long Châu Slide — Tạo slide theo template chuẩn

## Nguyên tắc cốt lõi

Không dùng create_design để tạo lại slide từ đầu. AI tự vẽ sẽ không bao giờ match được font, spacing, alignment, và hierarchy của slide gốc.

Cách đúng: clone template → dùng đúng component → chỉnh text/image — giữ nguyên 100% structure.

---

## Template file

- File key: 86lEVKARTBxBI5wibL1iJW
- Page: ✏️ Template (id: 0:1)
- Kích thước: 1920×1080px
- Brand: Nhà Thuốc Long Châu / FPT Retail

---

## Bảng 47 layout template

### Nhóm 1 — Cover / Opening (dark background)

Slide 1 — Node 3:4567 — Cover chính: subtitle + main title + date + mascot + logo góc
Slide 2 — Node 3:4568 — Cover + iMac mockup (blank screen bên phải)
Slide 3 — Node 3:4569 — Cover + iPhone mockup (blank screen bên phải)

### Nhóm 2 — Agenda & Section dividers

Slide 4  — Node 1:15993 — Agenda meeting: 2×3 grid, tối đa 6 items có số thứ tự màu
Slide 5  — Node 3:4570  — Section divider (dark bg, text bottom-left). Dùng slide này làm base cho MỌI section divider, chỉ đổi text "Mục X: Tên section"

### Nhóm 3 — Special layouts

Slide 6  — Node 3:4571 — Sơ đồ team (org chart có avatar)
Slide 7  — Node 3:4572 — Logo grid đối tác (4 hàng × 8 cột)
Slide 9  — Node 3:4574 — Note cards 3×4 — badge đồng màu yellow (12 items)
Slide 10 — Node 3:4575 — Note cards 3×4 — badge đa màu accent (12 items)
Slide 11 — Node 3:4576 — 3-column text với bullet list (xem lưu ý kỹ thuật bên dưới)
Slide 12 — Node 3:4577 — Bảng biểu (data table 4 cột + header row)

### Nhóm 4 — Text & Image

Slide 13 — Node 3:4578 — Hình ảnh toàn màn hình (1 placeholder lớn + caption)
Slide 14 — Node 3:4579 — 1 text block trái + image placeholder phải
Slide 15 — Node 3:4580 — 2 text blocks trái + image placeholder phải
Slide 16 — Node 3:4581 — 3 text blocks nhỏ trái + image placeholder phải
Slide 17 — Node 3:4582 — 1 text block lớn trên + image placeholder dưới
Slide 18 — Node 3:4583 — Image placeholder trên + 1 text block lớn dưới
Slide 19 — Node 3:4584 — Image placeholder trên + 2 text blocks dưới
Slide 20 — Node 3:4585 — Image placeholder trên + 3 note cards dưới

### Nhóm 5 — Mockup

Slide 21 — Node 3:4586 — Phone mockup single (centered, có ảnh app thật)
Slide 22 — Node 3:4587 — 4 phone mockups liên tiếp (user flow/sequence)
Slide 23 — Node 3:4588 — 3 text blocks trái + phone mockup phải
Slide 24 — Node 3:4589 — iMac full width (có ảnh web thật)
Slide 25 — Node 3:4590 — 2 text blocks trái + iMac mockup phải

### Nhóm 6 — Chart & Data

Slide 27 — Node 3:4592 — Chart full width (line chart thực)
Slide 28 — Node 3:4593 — Chart placeholder full (UChart 1600×800)
Slide 29 — Node 3:4594 — 2 charts ngang (bar + pie, thực)
Slide 30 — Node 3:4595 — 2 chart placeholders ngang (UChart 500×750 ×2)
Slide 31 — Node 3:4596 — 3 chart types (radar + treemap + funnel, thực)
Slide 32 — Node 3:4597 — 3 chart placeholders ngang (UChart 500×750 ×3)
Slide 33 — Node 3:4598 — 4-chart grid (stacked bar, multi-line, combo, candlestick)
Slide 34 — Node 3:4599 — 3 note cards trái + chart placeholder phải (UChart)
Slide 35 — Node 3:4600 — 3 note cards trái + chart phải (area/line thực)
Slide 36 — Node 3:4601 — 3 note cards trái + chart placeholder phải (variant)

### Nhóm 7 — Infographic

Slide 38 — Node 3:4603 — Mind map/radial (2 circles, 3 nhánh mỗi bên)
Slide 39 — Node 3:4604 — 5-step linear: hexagons + bullet details
Slide 40 — Node 3:4605 — 5-step circles: icon rings đơn giản
Slide 41 — Node 3:4606 — 5-step wave: snake timeline
Slide 42 — Node 3:4607 — PDCA cycle: 4-segment color ring
Slide 43 — Node 3:4608 — World map: colored regions
Slide 46 — Node 3:4611 — World map: with pins/markers

### Nhóm 8 — Closing

Slide 45 — Node 3:4610 — Q&A: light bg, mascot center
Slide 47 — Node 3:4612 — Thank you: dark bg, text center, logo top

---

## Components có sẵn — ưu tiên dùng thay vì tự tạo

Slide/Note/Number Item           — ID: 23:4716 — Note card có số badge + title + description
Slide/Note/Number Item Horizontal — ID: 23:4865 — Note card nằm ngang
Slide/Note/Chart Selector        — ID: 23:4728 — Placeholder cho chart (UChart)
Slide/Title Badge                — ID: 23:4567 — Badge số thứ tự (pill shape)
Slide/Note/Image Placeholder     — ID: 23:4711 — Placeholder ảnh (dashed border)
Slide/Title Group                — ID: 23:4570 — Group tiêu đề slide

Tạo instance từ component ID trên. KHÔNG tự vẽ lại từ đầu.

---

## Design tokens — bắt buộc dùng thay vì hardcode màu

### Color variables (collection: Color)

Background:
color/bg/page-light + color/bg/page-light-end  → gradient slides content (light blue)
color/bg/page-dark  + color/bg/page-dark-end   → gradient slides dark (cover, closing)
color/bg/surface                               → card background trắng
color/bg/surface-subtle                        → card background nhạt

Text:
color/text/primary   → text chính trên nền sáng
color/text/secondary → text phụ
color/text/on-dark   → text trên nền tối
color/text/brand     → text màu brand xanh Long Châu

Accent (theo thứ tự note items):
color/accent/yellow / yellow-light   → item 01
color/accent/pink                    → item 02
color/accent/green / green-light     → item 03
color/accent/purple / purple-light   → item 04
color/accent/teal                    → item 05
color/accent/sky / sky-light         → item 06+

### Font size variables (collection: Font Size)

font-size/display-lg, display-md, display-sm
font-size/heading-xl, heading-lg, heading-md, heading-sm
font-size/body-lg, body-md, body-sm

### Paint styles (gradients)

gradient/bg-light, gradient/bg-dark
gradient/accent-yellow, accent-blue, accent-green, accent-purple, accent-sky

### Text styles

Display: display/2xl (100px), display/xlarge (64), display/large (80), display/medium (56), display/small (48)
Heading: heading/xlarge (40), heading/large (32), heading/medium (24), heading/small (18), heading/xs (20)
Body:    body/large (24), body/medium (18), body/small (16), body/xs (12)
Label:   label/xlarge (32), label/large (32), label/medium (24), label/small (18)
Caption: caption/lg (19), caption/md (12), caption/sm (9)

---

## Quy trình làm việc

### 1. Lên kế hoạch đầy đủ trước khi làm

Trước khi gọi bất kỳ tool nào, lập bảng đầy đủ:
- Tổng số slides cần tạo
- Layout template phù hợp cho từng slide (từ bảng 47 ở trên)
- Vị trí x/y từng slide (tính theo section layout — xem bước 4)
- Nội dung text cho từng text node

### 2. Xác định nội dung cần tạo

Đọc kỹ yêu cầu: số lượng slide, loại nội dung, các section.

Mapping nội dung → template:
- Bullet points / danh sách (≤12 items)  → Slide 10 (note cards multi-color)
- Bullet points / danh sách (nhiều dòng) → Slide 11 (3-column text)
- Dữ liệu bảng                            → Slide 12
- Text + hình ảnh                         → Slide 13–20
- Demo app mobile                         → Slide 21–23
- Demo web/desktop                        → Slide 24–25
- Biểu đồ                                → Slide 27–36
- Process / timeline                      → Slide 38–42
- Bản đồ                                  → Slide 43, 46
- Q&A / Kết thúc                          → Slide 45, 47

### 3. Clone template — KHÔNG dùng create_design

Dùng duplicate_nodes (MCP tool):
  sourceFileKey: 86lEVKARTBxBI5wibL1iJW
  sourcePageId:  0:1
  nodeIds:       [danh sách node ID cần clone — mỗi unique type chỉ 1 lần]
  fileKey:       [file hiện tại đang làm việc]

**QUAN TRỌNG — Gotcha của duplicate_nodes:**
duplicate_nodes KHÔNG trả về IDs theo thứ tự input. Nó trả về IDs được sort theo source nodeId (thứ tự tăng dần của node ID gốc). Ví dụ, input [3:4567, 1:15993] → output đảo lại vì 1:15993 < 3:4567.

Sau khi duplicate, LUÔN verify mapping bằng cách check node.name:

const mapping = {}
for (let i = 0; i < createdNodeIds.length; i++) {
  const node = await figma.getNodeByIdAsync(createdNodeIds[i])
  mapping[node.name] = createdNodeIds[i]  // name = "1", "4", "5", "10", v.v.
}
// Dùng mapping["1"] cho Cover, mapping["4"] cho Agenda, mapping["5"] cho Section div, v.v.

Sau đó dùng Plugin API để clone nhân bản:

function cloneNode(id) {
  const n = figma.currentPage.children.find(c => c.id === id)
  const cl = n.clone()
  figma.currentPage.appendChild(cl)
  return cl
}

### 4. Vị trí — layout theo section (mặc định bắt buộc)

Mỗi ROW = một section/nhóm logic. KHÔNG dùng grid cố định 5 slides/row.

const GH = 2080  // gap ngang: 1920 + 160
const GV = 1400  // gap dọc: 1080 + 320

Ví dụ cho một presentation 7 sections:
Row 0 (y=BASE): [Cover, ToC]
Row 1 (y=BASE+GV): [Section 01, Content slide]
Row 2 (y=BASE+2*GV): [Section 02, Content slide A, Content slide B]
Row 3 (y=BASE+3*GV): [Section 03, Content slide A, Content slide B]
...

Tính BASE_Y để không đè lên frame cũ:

let maxY = 0
for (const c of figma.currentPage.children) {
  if (!mySlideIds.has(c.id) && 'height' in c) {
    const b = c.y + c.height
    if (b > maxY) maxY = b
  }
}
const BASE_Y = Math.ceil((maxY + 3000) / 1000) * 1000

### 5. Edit text — chỉ text, không đụng gì khác

Utility functions:

function findAll(nd, p, r=[]) { if(p(nd))r.push(nd); if('children' in nd)nd.children.forEach(c=>findAll(c,p,r)); return r }
function findFirst(nd, p) { if(p(nd))return nd; if('children' in nd)for(const c of nd.children){const f=findFirst(c,p);if(f)return f}; return null }
async function setTxt(n, v) {
  if (!n || n.type !== 'TEXT') return
  if (n.fontName !== figma.mixed) await figma.loadFontAsync(n.fontName)
  else for (const s of n.getStyledTextSegments(['fontName'])) await figma.loadFontAsync(s.fontName)
  n.characters = String(v)
}

**Đặc biệt — Slide 11 (3-column) có 3 loại child khác nhau:**

Slide 11 có 3 children direct:
- Col 1: INSTANCE "Slide/Note/Number Item" (x≈64)   → có TEXT number + title + bullets
- Col 2: INSTANCE "Slide/Note/Number Item" (x≈678)  → có TEXT number + title + bullets
- Col 3: FRAME   "Note"                   (x≈1292)   → ẨN cái này (col*
