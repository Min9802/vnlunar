# vnLunar - Thư Viện Âm Lịch Việt Nam

Thư viện JavaScript hoàn chỉnh để làm việc với Âm lịch Việt Nam, bao gồm đầy đủ các tính năng từ cơ bản đến nâng cao.

## ✨ Tính Năng

### 🔹 Cơ Bản

- ✅ Chuyển đổi Dương lịch ↔ Âm lịch (1800-2199)
- ✅ Tính Julian Day Number (JDN)
- ✅ Can Chi (Thiên Can, Địa Chi)
- ✅ Ngũ hành (Kim, Mộc, Thủy, Hỏa, Thổ)
- ✅ Con giáp 12 con

### 🔹 Xem Ngày

- ✅ 12 Sao Kiến Trừ
- ✅ 28 Tú Sao (Nhị Thập Bát Tú)
- ✅ 60 Nạp Âm (Nayin)
- ✅ Hoàng Đạo / Hắc Đạo
- ✅ Giờ Hoàng Đạo
- ✅ 24 Tiết Khí

### 🔹 Xuất Hành & Phong Thủy

- ✅ **Ngọc Hạp Thông Thư** - Xem hướng tốt xấu theo ngày
- ✅ **Hướng xuất hành theo tuổi** - Theo 12 con giáp
- ✅ **Giờ xuất hành Lý Thuần Phong** - 6 giờ tốt/xấu mỗi ngày
- ✅ Kỵ tuổi, xung khắc

## 📦 Cài Đặt

### Node.js
```bash
npm install @min98/vnlunar
```

### Browser
```html
<script src="https://cdn.jsdelivr.net/npm/@min98/vnlunar@1.0.0/dist/index.js"></script>
```

Or download and use locally:
```html
<script src="dist/index.js"></script>
```

## 🚀 Sử Dụng Nhanh

### Node.js
```javascript
const vnLunar = require('@min98/vnlunar');

// Lấy thông tin ngày hôm nay
const today = vnLunar.getFullInfo(6, 11, 2025);
console.log(today);

// Chuyển đổi Dương → Âm
const lunar = vnLunar.get_lunar_date(6, 11, 2025);
console.log('Âm lịch:', lunar.day + '/' + lunar.month + '/' + lunar.year);

// Xem ngày tốt xấu
const jd = vnLunar.jdn(6, 11, 2025);
const stars = vnLunar.get_12_stars(lunar.day, lunar.month);
console.log('12 Stars:', stars.name, '-', stars.status);

// Xem hướng xuất hành
const directions = vnLunar.get_travel_direction(jd, 1995);
console.log('Good directions:', directions.common_good_text);

// Xem giờ xuất hành
const hours = vnLunar.get_travel_hours(jd);
console.log('Auspicious hours:', hours.good_text);
```

## 📚 Tài Liệu

### Hướng Dẫn Chi Tiết
- [**API Reference**](docs/API.md) - Danh sách đầy đủ các hàm API
- [**Chuyển Đổi Lịch**](docs/CONVERSION.md) - Hướng dẫn chuyển đổi Dương/Âm lịch
- [**Xem Ngày**](docs/XEMNGAY.md) - 12 Sao, 28 Tú, Hoàng Đạo/Hắc Đạo
- [**Xuất Hành**](docs/XUATHANH.md) - Ngọc Hạp, Lý Thuần Phong
- [**Can Chi & Ngũ Hành**](docs/CANCHI.md) - Can Chi, Ngũ hành, Con giáp

### Ví Dụ Thực Tế
- [**Lịch Âm Cơ Bản**](examples/basic-calendar.js)
- [**Xem Ngày Tốt Xấu**](examples/xem-ngay.js)
- [**Tìm Ngày Cưới**](examples/tim-ngay-cuoi.js)
- [**Xuất Hành & Di Chuyển**](examples/xuat-hanh.js)
- [**Kiểm Tra Tuổi Xung**](examples/kiem-tra-tuoi.js)

## 🎯 Ví Dụ Nhanh

### 1. Xem thông tin ngày
```javascript
const info = vnLunar.getFullInfo(6, 11, 2025);

console.log('Dương lịch:', info.solar.day + '/' + info.solar.month + '/' + info.solar.year);
console.log('Âm lịch:', info.lunar.day + '/' + info.lunar.month + '/' + info.lunar.year);
console.log('Can Chi:', info.can_chi.day);
console.log('12 Sao:', info.stars_12.name, '(' + info.stars_12.status + ')');
console.log('28 Tú:', info.mansions_28.name, '(' + (info.mansions_28.good ? 'Tốt' : 'Xấu') + ')');
console.log('Nạp Âm:', info.nayin.name);
console.log('Hoàng/Hắc:', info.day_type.type);
```

### 2. Tìm ngày tốt để cưới
```javascript
const jd = vnLunar.jdn(6, 11, 2025);
const ketQua = vnLunar.check_good_day(jd, 'wedding');

if (ketQua.good) {
  console.log('✅ Ngày tốt để cưới!');
} else {
  console.log('❌ Không nên cưới vào ngày này');
}

// Tìm tất cả ngày tốt trong tháng
const ngayTot = vnLunar.find_good_days(11, 2025, 'wedding');
console.log('Số ngày tốt:', ngayTot.length);
```

### 3. Xem hướng & giờ xuất hành
```javascript
const jd = vnLunar.jdn(6, 11, 2025);
const namSinh = 1995;

// Xem hướng
const huong = vnLunar.get_travel_direction(jd, namSinh);
console.log('Hướng tốt:', huong.common_good_text || 'Không có hướng chung');
console.log('Lời khuyên:', huong.advice);

// Xem giờ
const gio = vnLunar.get_travel_hours(jd);
console.log('Giờ tốt:', gio.good_text);
console.log('Giờ xấu:', gio.bad_text);

// Kiểm tra giờ cụ thể
const ketQua = vnLunar.check_travel_hour(jd, 7); // 7h sáng
console.log('7h sáng:', ketQua.good ? 'TỐT' : 'XẤU');
```

### 4. Kiểm tra tuổi xung
```javascript
const ketQua = vnLunar.check_age_conflict(1990, 1996);

if (ketQua.conflict) {
  console.log('⚠️ CẢNH BÁO:', ketQua.description);
} else {
  console.log('✅ HÒA HỢP:', ketQua.description);
}
```

## 🔧 API Chính

### Chuyển đổi lịch
- `jdn(dd, mm, yyyy)` - Tính Julian Day Number
- `jdn2date(jd)` - Chuyển JDN → Dương lịch
- `get_lunar_date(dd, mm, yyyy)` - Dương → Âm lịch
- `get_solar_date(day, month, year, leap)` - Âm → Dương lịch
- `get_month(mm, yyyy)` - Lấy tất cả ngày trong tháng

### Can Chi & Ngũ hành
- `get_can_chi(lunar)` - Can Chi ngày/tháng/năm
- `get_year_can_chi(year)` - Can Chi năm
- `get_can_element(canIndex)` - Ngũ hành của Can
- `get_chi_element(chiIndex)` - Ngũ hành của Chi
- `get_year_element(year)` - Ngũ hành năm
- `get_element_relation(element1, element2)` - Quan hệ sinh khắc

### Xem ngày
- `get_12_stars(day, month)` - 12 Sao Kiến Trừ
- `get_28_mansions(jd)` - 28 Tú Sao
- `get_nayin(jd)` - 60 Nạp Âm
- `get_day_type(jd)` - Hoàng Đạo/Hắc Đạo
- `get_auspicious_hours(jd)` - Giờ Hoàng Đạo
- `check_good_day(jd, activity)` - Xem ngày tốt cho việc cụ thể
- `find_good_days(mm, yyyy, activity)` - Tìm ngày tốt trong tháng

### Xuất hành
- `get_direction_info(jd)` - Hướng tốt xấu theo ngày
- `get_age_direction(birthYear)` - Hướng theo tuổi
- `get_travel_direction(jd, birthYear)` - Tổng hợp hướng (ngày + tuổi)
- `get_travel_hours(jd)` - Giờ tốt xấu (Lý Thuần Phong)
- `check_travel_hour(jd, hour)` - Kiểm tra giờ cụ thể
- `get_time_frame(chiIndex)` - Lấy khung giờ từ Địa Chi

### Kỵ tuổi
- `get_conflicting_ages(chiIndex)` - Lấy tuổi xung
- `check_age_conflict(year1, year2)` - Kiểm tra 2 tuổi xung nhau

### Tổng hợp
- `getFullInfo(dd, mm, yyyy)` - Lấy tất cả thông tin

## 🧪 Test

```bash
# Chạy test đầy đủ
npm test

# Hoặc
node tests/test-all.js
```

Kết quả test: **43/43 tests passed (100%)** ✅

## 📊 Hiệu Năng

- Chuyển đổi Dương → Âm: **< 0.001ms/lần**
- Tính toán đầy đủ: **< 0.01ms/lần**
- Hỗ trợ: **1800-2199** (400 năm)

## 🌐 Tích Hợp Python

Sử dụng package Python: [**vnlunar**](https://pypi.org/project/vnlunar/)

```bash
pip install vnlunar
```

```python
from vnlunar import get_full_info

# Lấy thông tin đầy đủ
info = get_full_info(6, 11, 2025)
print(f"Âm lịch: {info['lunar']['day']}/{info['lunar']['month']}/{info['lunar']['year']}")
print(f"Can Chi: {info['can_chi']['day']}")
print(f"12 Sao: {info['stars_12']['name']}")
```

Xem thêm: [**vnlunar Documentation**](https://github.com/Min9802/pyvnlunar)

## 🎨 Demo

Xem demo trực quan: [https://vnlunar.min-services.com](https://vnlunar.min-services.com)

## 📖 Tham Khảo

- **Thuật toán gốc**: Hồ Ngọc Đức (2004)
- **Ngọc Hạp Thông Thư**: Sách cổ về hướng xuất hành
- **Lý Thuần Phong**: Phương pháp xem giờ truyền thống

## 📝 Giấy Phép

MIT License - Miễn phí sử dụng cho mọi mục đích.

## 🤝 Đóng Góp

Mọi đóng góp đều được chào đón! Vui lòng tạo Pull Request hoặc Issue trên GitHub.

## 📞 Liên Hệ

- **Website**: https://vnlunar.min-services.com
- **Repository**: https://github.com/Min9802/vnlunar
- **Issues**: https://github.com/Min9802/vnlunar/issues

---

**Version**: 1.0.0  
**Updated**: November 2025  
**Made with ❤️ by vnLunar Min**
