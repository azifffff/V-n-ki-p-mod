# Vẽ ảnh cho mod

Trang này giúp ảnh trong mod hợp nét với ảnh gốc của game. Gắn ảnh vào game xem [README § Ảnh](tai-lieu-api.md#ảnh) (`tuTien.assets.set` hoặc thư mục `img/` của gói).

Ảnh gốc của game gen bằng AI (Codex, Gemini) theo các khung prompt dưới đây. Khung chỉ là mẫu: tự sửa phần chủ thể, giữ phần phong cách.

Prompt mẫu dùng được cho mod của Vạn Kiếp Tu Tiên. Không dùng cho sản phẩm thương mại hay game khác (xem LICENSE).

## Hai phong cách

| Loại ảnh | Phong cách | Kiểu `assets.set` |
|---|---|---|
| Icon vật (đan, linh dược, pháp khí, phù, yêu tài…) | **Công bút đạm thái**: nét mực mảnh, màu khoáng nhạt, mờ | `item` |
| Chân dung địch, ngự linh, tu sĩ | **Thủy mặc**: mực đen xám, nền trắng, một điểm son | `enemy`, `portrait` |
| Tranh lớn các màn | Thủy mặc | `scene` |
| Hình chiêu | Thủy mặc, **mực đen đặc** (game tự tô màu hệ) | `skill` |

Mẹo chung:
- **Gắn một ảnh gốc của game làm tham chiếu** cùng loại (tải ở `/img/...` trong game) và ghi "Match the style of the reference image exactly". Đây là cách giữ nét đồng đều hiệu quả nhất.
- Gen nhiều ảnh trong **cùng một cuộc chat** để nét bút đồng đều. Chat dài mà AI bắt đầu lệch (thêm chữ, triện đỏ, nền ngà) thì mở chat mới, gắn lại tham chiếu, dán lại **cả khối prompt** chứ đừng chỉ gõ "same style".
- **Không chữ, không thư pháp, không triện đỏ** trên mọi ảnh. AI hay tự thêm; có thì gen lại.
- **Người không vẽ mặt** (mặt để trống). Phân biệt nhân vật bằng dáng, y phục, vật cầm.
- Mỗi chỗ dễ nhầm thì thêm một câu "NOT …" (ví dụ ngọc đục: `matte opaque jade, NOT glass, NOT shiny metal`).

## Kích thước và nền

Game không xử lý ảnh của mod, nên ảnh phải đúng cỡ và **nền trong suốt** sẵn.

| Loại | Cỡ xuất | Ghi chú |
|---|---|---|
| Icon vật | 128 × 128 | cắt sát vật, chừa mép vài px |
| Chân dung | 384 × 480 (4:5) | thấy trọn dáng, không cụt chân |
| Hình chiêu | 128 × 128 | chỉ cần dáng mực; màu sắc không có tác dụng |
| Tranh màn | 1280 × 720 (16:9) | |

- Định dạng `.webp` (hoặc `.png`), mỗi file ≤ 1 MB.
- Công cụ gen cho nền trong suốt thì dùng luôn (dòng `Background: fully transparent` trong mẫu icon).
- Ảnh thủy mặc nền trắng: tách nền theo độ sáng (trắng thành trong, mực đậm thành đặc, mực nhạt thành bán trong) để giữ nét loang. Công cụ "xóa nền" kiểu cắt viền sẽ làm mất quầng mực.
- Soát icon trên nền tối: chỗ nền bị sót lộ thành viền trắng, vật nhạt màu dễ bị thủng.

## Mẫu: icon vật (công bút)

Thay `<OBJECT>`. Gen nhiều món một lúc thì đổi thành tấm lưới ("a sheet of 3 separate icons … arranged in a single row", liệt kê từng món theo thứ tự) rồi tự cắt ô.

```
A single game item icon for a Chinese xianxia cultivation RPG, aspect ratio 1:1.
Match the painting style of the reference image exactly (it is an existing item icon of the same game).
Style: traditional Chinese gongbi painting with light color washes (gongbi dancai), as if painted with a fine brush on rice paper. Accurate realistic shapes and materials, delicate thin ink outlines, soft muted mineral pigments (celadon, ochre, cinnabar, indigo, malachite, pale gold), matte finish, gentle flat shading. Harmonious with a beige paper and black ink interface.
Not glossy, no 3D render look, no neon colors, not cartoon, not chibi.
The object is large, fills about 70% of the image, centered, never touching the edges.
Background: fully transparent (alpha channel). No frame, no border, no cast shadow on the ground, no text, no labels.
Object: <OBJECT>
Important: one icon only, transparent background, gongbi light-color style, matte, no text anywhere.
```

Ví dụ `<OBJECT>`:
- Đan: `one spherical pill, perfectly round like a marble (not a flat disc), deep ochre-gold like heated bronze, faint darker gold vein lines across its surface, a thin warm amber wisp of qi curling around it`
- Linh quả: `one deep violet spirit fruit, round like a plum with a soft bloom on its skin, a short dark twig with one muted green leaf, a faint violet glow and a thin violet wisp`

Đan dược luôn ghi "perfectly spherical, not a flat disc", không thì AI hay vẽ viên dẹt.

## Mẫu: chân dung (thủy mặc)

Thay `<SUBJECT>` và `<ACCENT>`.

```
Traditional Chinese ink wash painting (shuimo), light and airy, portrait of a single enemy for a xianxia RPG, aspect ratio 3:4.
Match the brush style of the reference image exactly.
Black and grey ink on a plain pure white background (#FFFFFF), no paper texture.
Soft wet washes, dry-brush edges, generous empty white space, subject fades into the white.
Monochrome, with one small accent of vermilion red on <ACCENT>.
Subject: <SUBJECT>
No text, no calligraphy, no red seal stamp, no border, no frame. Humans and humanoid figures have no drawn face (blank face, like a meditation figure). Show the whole figure, centered, with white space around it.
```

- `<ACCENT>`: đúng một chỗ (mắt yêu thú, ngọn lửa, bát máu, sợi chỉ đỏ…). Tên có màu (Xích…, Bích…) thì vẫn ghi rõ chỉ một điểm màu, không thì AI tô cả con.
- Yêu thú vẽ dáng con vật; chỉ bậc rất cao mới có nét người.
- Ví dụ `<SUBJECT>`: `a massive horned sea dragon without wings coiled in a cold mountain lake, ancient scales, a long beard of seaweed, mist and frost on the water`.
- Ngự linh có dạng theo giai (ấu thể, trưởng thành, đại thành, hóa hình): ghi rõ "younger / older than the reference, different pose, do NOT copy the reference pose". Hóa hình: hình người mặt trống, giữ tai / sừng / đuôi / hoa văn của loài.

## Mẫu: hình chiêu (mực đen)

Game dùng hình chiêu làm mặt nạ rồi tô màu theo hệ, nên chỉ có **dáng** mới có tác dụng.

```
A single square icon of a martial arts technique for a xianxia RPG, aspect ratio 1:1, extremely SIMPLE and bold.
Solid black ink silhouette on a plain pure white background, Chinese ink brush style, 3 to 6 strokes, large ink masses that read clearly at 30 px.
No outlines with white inside, no hatching, no engraving-style detail. No text, no runes, no symbols.
The strike flies to the RIGHT (pointed end on the right, fading tail on the left). Nothing touches the image edges.
Subject: <SUBJECT>
```

- Hướng: đòn bay sang phải; đòn từ trên giáng xuống (sét, trấn áp) thì hướng xuống. Game tự lật khi địch dùng.
- Binh khí / pháp bảo to (chiếm từ một phần ba hình), là bóng mực đặc có khe trắng mảnh dọc sống; hiệu ứng bọc sát quanh thành một khối liền.
- Hệ thể hiện bằng dáng, không bằng màu: lửa = lưỡi lửa, thủy = sóng / giọt, băng = tinh thể nhọn, lôi = tia gấp khúc, phong = xoáy gió, thổ = đá nứt, mộc = lá / dây leo, kim = khí sắc nhọn.
- Tay / vuốt đúng giải phẫu, tay năm ngón.

## Mẫu: tranh màn (thủy mặc)

```
Traditional Chinese ink wash painting (shuimo), light and airy, wide scene, aspect ratio 16:9.
Match the brush style of the reference image exactly.
Black and grey ink on a plain pure white background (#FFFFFF), no paper texture.
Soft wet washes, dry-brush edges, generous empty white space, subject fades into the white.
Monochrome, with one small accent of vermilion red on <ACCENT>.
No text, no calligraphy, no red seal stamp, no border, no frame. Figures have no drawn face.
Subject: <SUBJECT>
```
