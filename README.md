# CNTT1-nh-p-m-n-c-ng-ngh-th-ng-tin-Session07_EXontap
## Phần 1 – Đọc và định vị tệp tin

1. `Get-Content logs\server.log`
2. Notepad nạp toàn bộ file vào RAM gây tràn bộ nhớ; PowerShell đọc dạng luồng dòng nên tiết kiệm RAM.
3. `Get-ChildItem -Recurse -Filter *.log`

---

## Phần 2 – Lọc dữ liệu và Pipe

1. `Get-Content logs\server.log | Select-String "ERROR"`
2. **Bảng phân biệt:**

| Câu hỏi | Lệnh PowerShell |
| --- | --- |
| Tìm vị trí file `server.log` | `Get-ChildItem -Recurse -Filter server.log` |
| Tìm dòng chứa lỗi 404 | `Select-String "404" logs\server.log` |

* Lệnh Pipe lọc 404: `Get-Content logs\server.log | Select-String "404"`

3. `Get-ChildItem -Recurse -Filter *.log | Get-Content | Select-String -NotMatch "INFO"`

---

## Phần 3 – Toán tử chuyển hướng > và >>

1. `Get-Content logs\server.log | Select-String "404" > reports\daily_report.txt`
2. * Ghi nối: `Get-Content logs\server.log | Select-String "404" >> reports\daily_report.txt`
* Dùng nhầm `>`: Báo cáo cũ bị ghi đè hoàn toàn, mất hết dữ liệu cũ.



---

## Phần 4 – Shell Script và lệnh echo

1. * `Write-Output "Dang loc log..."`
* `Write-Output "=== LOG REPORT ===" > reports\daily_report.txt`


2. **Nội dung `scripts\auto_report.ps1`:**
```powershell
# Script tu dong loc loi 404
Write-Output "Dang chay..."
Get-Content logs\server.log | Select-String "404" > reports\daily_report.txt

```



---

## Phần 5 – Viết, chạy và thẩm định Script AI

1. * Chạy script: `.\scripts\auto_report.ps1`
* Kiểm tra kết quả: `Get-Content reports\daily_report.txt`


2. * **(a) Dòng nguy hiểm:** `Remove-Item -Recurse -Force C:\*` -> Xóa sạch toàn bộ hệ điều hành và file trên ổ C.
* **(b) Sửa an toàn:** `Remove-Item -Recurse -Force devops-lab\temp\*`
