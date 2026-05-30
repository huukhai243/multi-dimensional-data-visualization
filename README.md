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

## Các biểu đồ đã thực hiện

### 1. Weather heatmap

File xuất ra: `output/weather_heatmap.png`

Biểu đồ này thể hiện nhiệt độ trung bình theo từng thành phố và từng tháng. Dữ liệu được nhóm theo `city` và `month`, sau đó tính trung bình `avg_temp` và chuyển thành ma trận để vẽ heatmap.

### 2. Weather scatter plot

File xuất ra: `output/weather_scatter.png`

Biểu đồ này thể hiện mối quan hệ giữa độ ẩm, nhiệt độ, lượng mưa và thành phố. Trong biểu đồ:

- Trục X: độ ẩm trung bình.
- Trục Y: nhiệt độ trung bình.
- Màu sắc: thành phố.
- Kích thước điểm: lượng mưa.

### 3. Global temperature heatmap

File xuất ra: `output/global_temp_heatmap.png`

Biểu đồ này thể hiện dị thường nhiệt độ toàn cầu theo năm và tháng. Dữ liệu ban đầu ở dạng bảng rộng, sau đó được chuyển sang dạng dài và pivot lại thành ma trận `Year x Month` để vẽ heatmap.

### 4. Minnesota precipitation line chart

File xuất ra: `output/minnesota_precip_line.png`

Biểu đồ này thể hiện lượng mưa hằng tháng tại các địa điểm ở Minnesota. Mỗi đường biểu diễn một địa điểm, giúp so sánh xu hướng lượng mưa theo thời gian.

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

Chương trình đã được kiểm tra chạy thành công và tạo đủ bốn biểu đồ đầu ra.
