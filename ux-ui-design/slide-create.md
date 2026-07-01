# Skill: Tạo slide mới từ slide template
---
name: long-chau-slide-creator
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

Dùng 1 trong 3 bìa sau tuỳ theo đang demo cho concept nào (nếu chung chung thì dùng Slide 1, nếu cho landing page thì slide 2, nếu web/app thì slide 3)

Slide 1 — Node 3:4567 — Cover chính: subtitle + main title + date + mascot + logo góc
Slide 2 — Node 3:4568 — Cover + iMac mockup (blank screen bên phải)
Slide 3 — Node 3:4569 — Cover + iPhone mockup (blank screen bên phải)

### Nhóm 2 — Agenda & Section dividers

Slide 4  — Node 1:15993 — Agenda meeting: 2×3 grid, tối đa 6 items có số thứ tự màu
Slide 5  — Node 3:4570  — Section divider (dark bg, text bottom-left). Dùng slide này làm base cho MỌI section divider, chỉ đổi text "Mục X: Tên section"
Slide 8  — Node 3:4573  — Section divider variant 2
Slide 26 — Node 3:4591  — Section divider variant 3
Slide 37 — Node 3:4602  — Section divider variant 4
Slide 44 — Node 3:4609  — Section divider variant 5

### Nhóm 3 — Special layouts

Slide 6  — Node 3:4571 — Sơ đồ team (org chart có avatar)
Slide 7  — Node 3:4572 — Logo grid đối tác (4 hàng × 8 cột)
Slide 9  — Node 3:4574 — Note cards 3×4 — badge đồng màu yellow (12 items)
Slide 10 — Node 3:4575 — Note cards 3×4 — badge đa màu accent (12 items)
Slide 11 — Node 3:4576 — 3-column text với bullet list
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

### 1. Xác định nội dung cần tạo
Đọc kỹ yêu cầu: số lượng slide, loại nội dung, section nào.

### 2. Chọn layout từ bảng trên

Bullet points / danh sách     → Slide 9, 10, 11
Dữ liệu bảng                  → Slide 12
Text + hình ảnh               → Slide 13–20
Demo app mobile               → Slide 21–23
Demo web/desktop              → Slide 24–25
Biểu đồ                       → Slide 27–36
Process / timeline            → Slide 38–42
Bản đồ                        → Slide 43, 46
Q&A / Kết thúc                → Slide 45, 47

### 3. Clone template — KHÔNG dùng create_design

Dùng duplicate_nodes (MCP):
  sourceFileKey: 86lEVKARTBxBI5wibL1iJW
  sourcePageId:  0:1
  nodeIds:       [danh sách node ID cần clone]
  fileKey:       [file hiện tại đang làm việc]

Hoặc Plugin API (nếu đã copy vào file rồi):

async function dupAt(sourceId, x, y) {
  const source = await figma.getNodeByIdAsync(sourceId);
  const clone = source.clone();
  figma.currentPage.appendChild(clone);
  clone.x = x; clone.y = y;
  return clone.id;
}

### 4. Tính grid position trước khi clone

gap ngang: 1920 + 240 = 2160px
gap dọc:   1080 + 200 = 1280px
Lập bảng { slideKey, x, y } trước, clone tất cả trong 1 script.

### 5. Edit text — chỉ text, không đụng gì khác

function findAll(node, pred, r = []) {
  if (pred(node)) r.push(node);
  if ('children' in node) node.children.forEach(c => findAll(c, pred, r));
  return r;
}

async function setTxt(n, v) {
  if (!n || n.type !== 'TEXT') return;
  if (n.fontName !== figma.mixed) await figma.loadFontAsync(n.fontName);
  else for (const s of n.getStyledTextSegments(['fontName'])) await figma.loadFontAsync(s.fontName);
  n.characters = v;
}

Path đến text node:
- Cover slide:  "Title Group" → 2 TEXT sort by y → [0] label, [1] main title
- Note cards:   "Note" sort by x → "Container" → TEXT sort by y → [0] heading, [1] desc
- Section div:  "Title Group" → TEXT sort by y → label + main title

### 6. Image placeholder

Component Slide/Note/Image Placeholder (dashed border): KHÔNG xóa, để user tự thay ảnh.
Nếu slide có ảnh mockup thực (phone/iMac): giữ nguyên hoặc replace cùng kích thước.

### 7. Chart placeholder

Component Slide/Note/Chart Selector: KHÔNG xóa, để user mở plugin UChart.
Size UChart: 1600×800 (full width slot), 500×750 (multi-slot).

---

## Quy tắc brand bắt buộc

- KHÔNG xóa logo Nhà Thuốc Long Châu / FPT Retail
- KHÔNG thay đổi màu background — dùng đúng gradient token
- KHÔNG thay font — load font từ node, setTxt, không đổi fontName
- KHÔNG thay layout, spacing, sizing — chỉ thay text và image content
- Accent màu note items: yellow → pink → green → purple → teal → sky
- Section divider: luôn dùng slide 5 làm base, chỉ đổi text "Mục X: Tên section"

---

## Checklist

- Inspect layer tree slide mẫu trước khi làm
- Chọn đúng layout từ bảng 47 slides
- Tính grid position cho tất cả slide mới
- Clone bằng duplicate_nodes — không dùng create_design
- Load font trước khi edit text
- Dùng component có sẵn (6 components) thay vì tự vẽ
- Bind đúng color token, không hardcode màu
- Để nguyên image placeholder và chart placeholder
- Không sửa layout, spacing, sizing

## Sai lầm cần tránh

create_design để tạo slide trông giống    → Clone đúng template node ID
Tự tạo note card từ rectangle + text      → Dùng component Slide/Note/Number Item
Hardcode màu hex vào fills                → Bind variable token color/accent/*
Xóa logo hoặc đổi vị trí                 → Giữ nguyên logo
Fill ảnh vào chart placeholder            → Để component Slide/Note/Chart Selector nguyên
Clone slide rồi edit layout               → Chỉ edit text characters
