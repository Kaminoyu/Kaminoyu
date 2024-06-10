# SteloUI

**Tác giả:** Bùi Duy Hải  
**Lần chỉnh sửa gần nhất:** 2024/06/09

## Giới Thiệu

Dự án SteloUI được tạo ra nhằm giúp các lập trình viên sử dụng C++ tạo ra các giao diện người dùng (UI) trên hệ điều hành Windows một cách dễ dàng và hiệu quả. SteloUI cho phép các lập trình viên tự vận hành và kiểm soát vòng lặp chính của ứng dụng, mang lại sự linh hoạt và tùy chỉnh cao trong phát triển ứng dụng.

### Các tính năng chính

- **Sử dụng game loop của lập trình viên**: SteloUI cho phép lập trình viên sử dụng game loop của riêng mình làm vòng lặp chính của ứng dụng, thay vì phải tuân theo vòng lặp cố định từ hệ thống UI.
- **Định nghĩa lớp UI riêng biệt**: Lập trình viên có thể tự định nghĩa các lớp UI riêng biệt theo nhu cầu của mình, mặc dù vẫn phải chịu một phần sự kiểm soát từ hệ thống của SteloUI để đảm bảo tính nhất quán và hoạt động ổn định của giao diện.

## Thiết Lập

### Cách cài đặt

1. **Tải xuống SteloUI**:
    - Vào [trang chủ của SteloUI](https://link-to-steloui-homepage).
    - Chọn mục Download ở phía trên bên phải trang chủ.
    - Chọn phiên bản phù hợp với hệ điều hành của bạn.
2. **Giải nén và sao chép thư mục**:
    - Giải nén thư mục đã tải về.
    - Sao chép thư mục có tên là `SteloUI`.
3. **Thêm vào dự án của bạn**:
    - Mở dự án mà bạn muốn sử dụng SteloUI.
    - Dán thư mục `SteloUI` vào nơi chứa các tệp code của bạn.
4. **Thiết lập dự án** (nếu cần):
    - Nhấn vào mục Project ở thanh tiêu đề và chọn Properties ở dưới cùng.
    - Trong cửa sổ Properties, chọn Linker sau đó chọn System.
    - Kiểm tra và đảm bảo mục SubSystem là `Windows (/SUBSYSTEM:WINDOWS)`. Nếu không, hãy dán `Windows (/SUBSYSTEM:WINDOWS)` vào mục SubSystem và nhấn OK.

## Bắt Đầu

### Tạo các tệp cần thiết

1. Tạo 3 tệp lần lượt là `SampleWindow.h`, `SampleWindow.cpp`, `Main.cpp`.

- **SampleWindow.h** và **SampleWindow.cpp** là để tạo lớp kế thừa từ lớp gốc nhằm mục đích xây dựng hệ thống cửa sổ.
- **Main.cpp** là để định nghĩa hàm main và quản lý vòng lặp chính của ứng dụng.

### Sao chép và dán nội dung vào các file

**File SampleWindow.h**:
```cpp
#include "SteloUI/SteloUI.h"

class SampleWindow : public SteloUI_Window {
public:
    SampleWindow(std::wstring title);

    void OnDestroy();
};
```
**File SampleWindow.cpp**:
```cpp
#include "SampleWindow.h"

SampleWindow::SampleWindow(std::wstring title) :
    SteloUI_Window(nullptr, title, SteloUI_2D(0.0f, 0.0f), SteloUI_2D(800.0f, 500.0f)) {
    Bind(SteloEVT_Destroy, std::bind(&SampleWindow::OnDestroy, this));
}

void SampleWindow::OnDestroy() {
    Destroy();
}
```
**File Main.cpp**:
```cpp
#include "SampleWindow.h"

int WINAPI WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow) {
    SampleWindow* sampleWindow = new SampleWindow(L"SampleWindow");
    sampleWindow->Show(true);

    MSG msg = { 0 };
    while (SteloUI_Update(msg)) {
    }
    return 0;
}
```
### Biên dịch và chạy chương trình
- Biên dịch và chạy chương trình. Nếu mọi thứ đều chính xác, bạn sẽ thấy một cửa sổ được hiển thị với tiêu đề là **SampleWindow**.
