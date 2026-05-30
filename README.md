# Multi-dimensional Data Visualization

Dự án này trực quan hóa dữ liệu đa chiều bằng Python. Chương trình đọc ba bộ dữ liệu thời tiết và khí hậu trong thư mục `data/`, xử lý dữ liệu bằng `pandas`, sau đó tạo bốn biểu đồ bằng `matplotlib` và `seaborn`.

## Cấu trúc thư mục

```text
multi-dimensional-data-visualization/
├── data/
│   ├── weather_data.csv
│   ├── global_temp.csv
│   └── minnesota_weather.csv
├── src/
│   └── create_visualizations.py
├── output/
│   ├── weather_heatmap.png
│   ├── weather_scatter.png
│   ├── global_temp_heatmap.png
│   └── minnesota_precip_line.png
├── requirements.txt
└── README.md
```

## Dữ liệu sử dụng

1. `weather_data.csv`: dữ liệu thời tiết hằng ngày của nhiều thành phố, gồm nhiệt độ, độ ẩm, gió, áp suất, lượng mưa và hiện tượng thời tiết.
2. `global_temp.csv`: dữ liệu dị thường nhiệt độ toàn cầu theo tháng và năm từ NASA GISTEMP.
3. `minnesota_weather.csv`: dữ liệu thời tiết hằng tháng tại sáu địa điểm ở Minnesota trong giai đoạn 1927-1936.

## Tiền xử lý dữ liệu

### Weather data

- Đọc file `weather_data.csv` bằng `pandas.read_csv()`.
- Với biểu đồ heatmap, dữ liệu được nhóm theo `city` và `month`, sau đó tính trung bình `avg_temp`.
- Bảng sau khi nhóm được chuyển về dạng ma trận bằng `pivot()`, trong đó hàng là thành phố, cột là tháng và giá trị là nhiệt độ trung bình.
- Với biểu đồ scatter, cột `precip` được chuyển sang dạng số bằng `pd.to_numeric()`. Các giá trị không hợp lệ hoặc thiếu được thay bằng `0` để tránh lỗi khi biểu diễn kích thước điểm.

### Global temperature data

- Đọc file `global_temp.csv` và bỏ dòng tiêu đề phụ bằng `skiprows=1`.
- Các giá trị thiếu được ký hiệu bằng `***` được thay bằng `pd.NA`.
- Các cột tháng từ `Jan` đến `Dec` được chuyển sang dạng số bằng `pd.to_numeric()`.
- Dữ liệu ban đầu ở dạng bảng rộng được chuyển sang dạng dài bằng `melt()`, sau đó pivot lại thành ma trận `Year x Month` để vẽ heatmap.

### Minnesota weather data

- Đọc file `minnesota_weather.csv` bằng `pandas.read_csv()`.
- Tạo cột thời gian `date` từ ba cột `year`, `mo` và ngày giả định là ngày 1 của mỗi tháng.
- Dữ liệu được biểu diễn theo chuỗi thời gian, trong đó mỗi đường tương ứng với một địa điểm `site`.

## Các biểu đồ và nhận xét khoa học

### 1. Weather heatmap

File xuất ra: `output/weather_heatmap.png`

Biểu đồ này thể hiện nhiệt độ trung bình theo từng thành phố và từng tháng. Dữ liệu được nhóm theo `city` và `month`, sau đó tính trung bình `avg_temp` và chuyển thành ma trận để vẽ heatmap.

**Nhận xét khoa học:** Nhiệt độ thể hiện sự khác biệt khí hậu rõ rệt giữa các thành phố. Mumbai có nhiệt độ trung bình cao nhất trong hầu hết các tháng, đặc biệt tháng 5 đạt khoảng `86.6°F`, trong khi Beijing có mùa đông lạnh rõ rệt, thấp nhất vào tháng 1 khoảng `25.1°F`. Điều này cho thấy heatmap giúp nhận diện đồng thời yếu tố không gian, tức thành phố, và yếu tố thời gian, tức tháng.

### 2. Weather scatter plot

File xuất ra: `output/weather_scatter.png`

Biểu đồ này thể hiện mối quan hệ giữa độ ẩm, nhiệt độ, lượng mưa và thành phố. Trong biểu đồ:

- Trục X: độ ẩm trung bình.
- Trục Y: nhiệt độ trung bình.
- Màu sắc: thành phố.
- Kích thước điểm: lượng mưa.

**Nhận xét khoa học:** Quan hệ giữa độ ẩm và nhiệt độ không tuyến tính mạnh trên toàn bộ dữ liệu, hệ số tương quan chỉ khoảng `0.14`. Tuy nhiên lượng mưa có xu hướng xuất hiện nhiều hơn khi độ ẩm cao, với tương quan giữa độ ẩm và lượng mưa khoảng `0.20`. Mumbai và Chicago có nhiều điểm mưa lớn hơn so với các thành phố còn lại, phản ánh sự khác biệt về điều kiện khí hậu địa phương.

### 3. Global temperature heatmap

File xuất ra: `output/global_temp_heatmap.png`

Biểu đồ này thể hiện dị thường nhiệt độ toàn cầu theo năm và tháng. Dị thường nhiệt độ là mức chênh lệch so với mốc trung bình 1951-1980. Dữ liệu ban đầu ở dạng bảng rộng, sau đó được chuyển sang dạng dài và pivot lại thành ma trận `Year x Month` để vẽ heatmap.

**Nhận xét khoa học:** Heatmap cho thấy xu hướng nóng lên toàn cầu rất rõ ở giai đoạn gần đây. Trung bình dị thường nhiệt độ từ năm 2015 trở đi khoảng `1.00°C`, trong khi giai đoạn 1880-1910 khoảng `-0.26°C`. Giá trị cao nhất trong dữ liệu là tháng 9 năm 2023 với khoảng `1.48°C`. Điều này cho thấy biểu đồ không chỉ thể hiện biến động theo mùa mà còn làm nổi bật xu thế tăng nhiệt dài hạn.

### 4. Minnesota precipitation line chart

File xuất ra: `output/minnesota_precip_line.png`

Biểu đồ này thể hiện lượng mưa hằng tháng tại các địa điểm ở Minnesota. Mỗi đường biểu diễn một địa điểm, giúp so sánh xu hướng lượng mưa theo thời gian.

**Nhận xét khoa học:** Lượng mưa tại Minnesota có tính mùa vụ rõ rệt. Trung bình tháng 6 có lượng mưa cao nhất, khoảng `3.33 inches`, trong khi tháng 2 thấp nhất, khoảng `0.67 inches`. Waseca tháng 8 năm 1935 đạt lượng mưa lớn nhất trong dữ liệu, khoảng `10.11 inches`, cho thấy một sự kiện mưa cực trị theo địa điểm và thời gian.

## Cách chạy chương trình

Cài các thư viện cần thiết:

```bash
pip install -r requirements.txt
```

Chạy script từ thư mục gốc của project:

```bash
python src/create_visualizations.py
```

Sau khi chạy thành công, terminal sẽ hiển thị danh sách bốn file ảnh đã được tạo trong thư mục `output/`.

## Ghi chú triển khai

Các hàm chính đã được hoàn thành trong `src/create_visualizations.py`:

- `plot_weather_heatmap()`
- `plot_weather_scatter()`
- `plot_global_temp_heatmap()`
- `plot_minnesota_precip_line()`

Chương trình đã được kiểm tra chạy thành công và tạo đủ bốn biểu đồ đầu ra ở định dạng `.png` với độ phân giải 300 DPI.
