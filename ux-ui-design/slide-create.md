# Skill: Tạo slide mới từ slide template có sẵn

## Nguyên tắc cốt lõi

**Không dùng `create_design` để tạo lại slide từ đầu.** AI tự vẽ sẽ không bao giờ match được font, spacing, alignment, và hierarchy của slide gốc.

Cách đúng: **clone template → chỉnh text** — giữ nguyên 100% structure, chỉ thay nội dung.

---

## Quy trình

### 1. Đọc thumbnail và layer tree của slide mẫu

Trước khi làm bất cứ thứ gì, inspect layer tree của tất cả slide mẫu:

    function describeTree(node, depth = 0) {
      const indent = '  '.repeat(depth);
      let info = `${indent}[${node.type}] "${node.name}"`;
      if (node.type === 'TEXT') info += ` → "${node.characters.slice(0, 60)}"`;
      if ('x' in node) info += ` (x:${Math.round(node.x)}, y:${Math.round(node.y)})`;
      const lines = [info];
      if ('children' in node && depth < 4) node.children.forEach(c => lines.push(...describeTree(c, depth + 1)));
      return lines;
    }

Xác định rõ: loại slide đang có, tên chính xác layer chứa text, phần tử nào là template-specific (hình minh họa, icon...).

### 2. Tính grid position

Đọc x, y của các slide hiện có để tìm quy luật lưới:

    // gap ngang = 1920 (width) + 240 (gap) = 2160px
    // gap dọc = 1680px
    // x = 0, 2160, 4320, 6480, ...
    // y = hàng mới cho mỗi section

Lập bảng { key, x, y } cho tất cả slide mới trước khi bắt tay làm.

### 3. Duplicate template — không dùng create_design

    async function dupAt(sourceId, x, y) {
      const source = await figma.getNodeByIdAsync(sourceId);
      const clone = source.clone();
      figma.currentPage.appendChild(clone);
      clone.x = x;
      clone.y = y;
      return clone.id;
    }

Chạy tất cả dupAt() trong một script, return toàn bộ IDs để dùng ở bước tiếp.

### 4. Edit text — chỉ text, không đụng gì khác

    function findFirst(node, pred) {
      if (pred(node)) return node;
      if ('children' in node) { for (const c of node.children) { const f = findFirst(c, pred); if (f) return f; } }
      return null;
    }
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

Path đến text node theo từng loại slide:

- Header slide: "Title Group" → 2 TEXT sort by y → [0] label, [1] main title
- 3-note slide: "Title" frame → TEXT; "Note" sort by x → "Container" → TEXT sort by y → [0] heading, [1] desc
- 2-column slide: "Title" → TEXT; "Note" sort by x → left col → "Wrapper" sort by y → 2 TEXTs

### 5. Dọn dẹp sau khi clone

Xóa hình minh họa bị copy theo — hình trong template là của slide đó, không dùng cho slide mới:

    frame.children
      .filter(c => c.type === 'RECTANGLE' && c.name.toLowerCase().startsWith('image'))
      .forEach(n => n.remove());

Với slide placeholder — để trống, không fill content:

    frame.children.filter(c => c.name === 'Note').forEach(n => { n.visible = false; });

---

## Checklist

- Xem thumbnail tất cả slide mẫu trước khi bắt đầu
- Inspect layer tree để biết chính xác tên layer và cấu trúc
- Tính position grid cho tất cả slide mới
- Clone template (không dùng create_design)
- Load font trước khi edit text
- Xóa hình minh họa bị copy theo
- Để trống slide placeholder (ẩn Note frames, không fill content)
- Không sửa layout, color, spacing — chỉ text

---

## Sai lầm cần tránh

Đừng dùng create_design để tạo slide "trông giống" → Clone đúng template gốc
Đừng edit layout hay style → Chỉ edit text content
Đừng giữ hình minh họa từ template → Xóa sau khi clone
Đừng fill content vào slide placeholder → Để trống, ẩn Note frames
Đừng dùng design agent để "match style" → Duplicate → text edit
