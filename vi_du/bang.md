# Bảng dữ liệu (CSV / Excel)

Xem và sửa chỉ số bằng bảng tính thay vì viết YAML. Thiết kế: gdd 60 §21.

## Lấy bảng

- Trong game: **Cấu hình → Mods → "Tải bảng dữ liệu"**. Ra một `.zip`, dựng từ nội dung đang chạy (gốc + mod đang bật), nên khớp đúng bản game bạn có.
- Hoặc tải `/mod/bang.zip` của bản build (chỉ nội dung gốc).

Mỗi file CSV là một loại, mỗi dòng một mục:

| File | Gồm |
|---|---|
| `enemy.csv` | địch, yêu thú |
| `chieu.csv` | chiêu của địch |
| `item_<loai>.csv` | vật phẩm, tách theo `loai` (`item_phap_khi`, `item_dan_duoc`, `item_nguyen_lieu`…) |
| `dp.csv` | đan phương / công thức |
| `npc.csv`, `ho_quai.csv`, `toc.csv`, `the_chat.csv`, `linh_can.csv`, `origin.csv`… | các loại còn lại |

Không có bảng cho sự kiện (`ev.`), chuỗi (`chain.`), lore: đó là cây lời kể, viết YAML (lấy mẫu bằng `tuTien.yaml(id)`, xem [README.md](tai-lieu-api.md)).

Cách ghi ô:

- Số, chữ, `true` / `false`: ghi thẳng.
- Danh sách giá trị đơn: `a|b|c` (vd `kim|moc`, `chieu.can_xe|chieu.vo`).
- Trường lồng (object, danh sách object): JSON gọn, vd `[{"linh_thach":14},{"tu_vi":0.5}]`.
- Cột `_file`: file gốc của mục, chỉ để tra.

## Sửa cho mod

Đặt file CSV vào `content/bang/` của gói (tên file tùy ý), cạnh `content/**.yaml`:

```
mod_cua_toi/
  mod.yaml
  content/
    bang/
      chinh_gia.csv
```

```csv
id,gia,he,chieu+,roi.0.linh_thach
item.thiet_khoang,6,,,
item.thiet_kiem,,kim|hoa,,
enemy.cuong_thi,,,chieu.thi_doc,30
item.mod_cua_toi_truc_tinh,8,moc,,
```

- Dòng đầu là tiêu đề, phải có cột `id`. Chỉ cần những cột muốn đổi; cột khác bỏ đi được.
- **Id đã có** (của game hoặc mod khác): chỉ sửa ô có chữ, ô trống giữ nguyên, ô `~` xóa trường. Đi chung đường với `patch` của `mod.yaml`: hai mod cùng sửa một chỗ thì màn Mods báo "Mod đè nhau".
- **Id mới** dạng `<tiền tố>.<id mod>_<tên>`: thêm mục mới. Phải đủ trường bắt buộc như viết YAML (chép một dòng gần giống từ bảng tải về rồi sửa là nhanh nhất).
- Cột có chấm sửa sâu: `roi.0.linh_thach` (phần tử đầu của `roi`), `ngu_linh.do_kho`.
- Cột đuôi `+` nối vào danh sách, không thay: `chieu+` thêm chiêu vào cuối, giữ chiêu cũ.
- Kiểu giá trị theo kiểu trường đó trong game (trường là số thì ô phải là số; trường là danh sách thì `a` cũng thành `[a]`). Số thập phân ghi `0.5` hay `0,5` đều được.
- Dòng sai (số viết chữ, JSON hỏng, id tiền tố lạ, id lặp) bị bỏ, ghi vào nhật ký mod kèm `file:dòng`; dòng khác vẫn nạp. Mục mới sai trường bắt buộc thì validator báo như YAML.
- Chữ trong CSV là tiếng Việt như YAML; bản dịch vẫn qua `i18n/`.

## Excel, Google Sheets

- Excel: **Lưu thành → "CSV UTF-8 (Comma delimited)"**. Lưu "CSV" thường sẽ hỏng dấu tiếng Việt. Máy đặt vùng Việt Nam lưu bằng dấu `;` cũng đọc được.
- Excel hay tự đổi ô: `1|2` không sao, nhưng id kiểu `1e5` hay ô bắt đầu `=` sẽ bị đổi. Mở bằng **Dữ liệu → Từ văn bản/CSV** và đặt cột là Văn bản nếu gặp.
- Google Sheets: **Tệp → Tải xuống → .csv**.

Thử nhanh: "Mở thư mục đang làm" ở màn Mods, sửa CSV, bấm "Nạp lại"; lỗi từng dòng hiện trong nhật ký mod.
