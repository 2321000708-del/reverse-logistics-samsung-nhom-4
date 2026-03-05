# reverse-logistics-samsung-nhom-4
Sơ đồ quy trình Logistics ngược 5 bước của Samsung
graph TD
    %% Định nghĩa style
    classDef input fill:#e1f5fe,stroke:#01579b,stroke-width:2px;
    classDef home fill:#bbdefb,stroke:#0d47a1,stroke-width:2px;
    classDef agent fill:#ffe6cc,stroke:#d79b00,stroke-width:2px;
    classDef center fill:#fff3e0,stroke:#e65100,stroke-width:3px;
    classDef system fill:#f8cecc,stroke:#b85450,stroke-width:2px;
    classDef transport fill:#d1c4e9,stroke:#512da8,stroke-width:2px;
    classDef rrc fill:#c8e6c9,stroke:#1b5e20,stroke-width:3px;
    classDef process fill:#d5e8d4,stroke:#82b366,stroke-width:2px;
    classDef feedback fill:#e1d5e7,stroke:#4a148c,stroke-width:2px;
    classDef waste fill:#ffccbc,stroke:#bf360c,stroke-width:2px;

    %% 3 DÒNG ĐẦU VÀO
    subgraph Input [BA DÒNG ĐẦU VÀO]
        I1[<div style="font-size:16px"><b>Dòng bảo hành & sửa chữa</b><br/>Người tiêu dùng cuối</div>]:::input
        I2[<div style="font-size:16px"><b>Dòng trả hàng thương mại</b><br/>Đại lý, nhà bán lẻ</div>]:::input
        I3[<div style="font-size:16px"><b>Dòng rác thải điện tử</b><br/>SRD, Trade-in</div>]:::waste
    end

    %% ==================== BƯỚC 1: 4 LỚP ====================
    subgraph Buoc1 [BƯỚC 1: TIẾP NHẬN VÀ KIỂM SOÁT ĐẦU VÀO]
        
        %% LỚP 1: TẠI NHÀ (Tự chẩn đoán từ xa)
        L1[<div style="font-size:16px"><b>LỚP 1: TẠI NHÀ - TỰ CHẨN ĐOÁN TỪ XA</b></div>]:::home
        L1a[Samsung Members Self-Diagnostics<br/>Kiểm tra 15 hạng mục]:::home
        L1b{Kết quả?}:::home
        L1c[Samsung Smart Tutor<br/>Hỗ trợ từ xa]:::home
        L1d[<div style="font-size:16px"><b>GIẢI QUYẾT TỪ XA</b><br/>35-40% trường hợp<br/>Kết thúc - Không vào RL</div>]:::home
        L1e[Cần mang đến điểm tiếp nhận]:::home
        
        I1 --> L1 --> L1a --> L1b
        L1b -->|Lỗi phần mềm| L1c --> L1d
        L1b -->|Lỗi phần cứng/không rõ| L1e

        %% LỚP 1.5: ĐẠI LÝ (Kênh phổ biến)
        L15[<div style="font-size:16px"><b>LỚP 1.5: ĐẠI LÝ / CỬA HÀNG BÁN LẺ</b><br/>(Tiếp nhận từ khách hoặc trả hàng TM)</div>]:::agent
        L15a[Nhân viên đại lý<br/>Kiểm tra sơ bộ]:::agent
        L15b{Phân loại}:::agent
        L15c[Lỗi đơn giản / Hàng mới<br/>Chuyển lên trung tâm bảo hành]:::agent
        L15d[Lỗi phức tạp<br/>Chuyển lên trung tâm bảo hành]:::agent
        L15e[Hướng dẫn khách đến thẳng<br/>trung tâm bảo hành]:::agent
        
        I1 -->|Khách đến đại lý| L15
        I2 -->|Trả hàng thương mại| L15
        L1e -->|Khách chọn đại lý| L15
        
        L15 --> L15a --> L15b
        L15b -->|Tiếp nhận| L15c
        L15b -->|Tiếp nhận| L15d
        L15b -->|Không nhận sửa| L15e

        %% LỚP 2: TRUNG TÂM BẢO HÀNH - GALAXY CONSULTANTS (TIỀN TUYẾN)
        L2[<div style="font-size:16px"><b>LỚP 2: TRUNG TÂM BẢO HÀNH CHÍNH HÃNG</b><br/><b>GALAXY CONSULTANTS</b></div>]:::center
        L2a[Tiếp nhận từ:<br/>- Khách đến thẳng<br/>- Đại lý gửi lên<br/>- Trả hàng thương mại]:::center
        L2b[Chẩn đoán chuyên sâu<br/>Xác định nguyên nhân]:::center
        L2c{Kết quả}:::center
        L2d[Xử lý tại chỗ (thay pin, cập nhật...)<br/><b>Trả khách</b>]:::center
        L2e[Từ chối (hết bảo hành/lỗi người dùng)<br/><b>Ghi nhận từ chối</b>]:::center
        L2f[<b>CẦN XỬ LÝ CHUYÊN SÂU</b><br/>Tạo mã RMA, nhập dữ liệu<br/>Chuẩn bị vận chuyển]:::center
        
        I1 -->|Khách đến thẳng| L2
        L15c --> L2
        L15d --> L2
        L15e -->|Khách đến theo hướng dẫn| L2
        I2 -->|Trả hàng TM chuyển thẳng| L2
        
        L2 --> L2a --> L2b --> L2c
        L2c -->|Xử lý được| L2d
        L2c -->|Không đủ điều kiện| L2e
        L2c -->|Cần chuyên sâu| L2f

        %% LỚP 3: TÍCH HỢP HỆ THỐNG DỮ LIỆU (XUYÊN SUỐT)
        L3[<div style="font-size:16px"><b>LỚP 3: TÍCH HỢP HỆ THỐNG</b><br/>QINGS & CELLO</div>]:::system
        L3a[<div style="font-size:16px"><b>QINGS</b>: Nhập IMEI, mã lỗi,<br/>tình trạng, quyết định</div>]:::system
        L3b[<div style="font-size:16px"><b>CELLO Square</b>: Ghi nhận thông tin<br/>hoàn trả, tạo mã RMA,<br/>kích hoạt vận chuyển</div>]:::system

        L2d -.->|Cập nhật| L3a
        L2e -.->|Ghi nhận| L3a
        L2f -->|Nhập chi tiết| L3a
        L2f -->|Đồng bộ| L3b
    end

    %% ==================== BƯỚC 2: VẬN CHUYỂN NGƯỢC ====================
    subgraph Buoc2 [BƯỚC 2: VẬN CHUYỂN NGƯỢC - QUẢN TRỊ QUA SAMSUNG SDS]
        T1[Nền tảng CELLO điều phối<br/>Tối ưu lộ trình, theo dõi real-time]:::transport
        T2[Phương thức:<br/>Backhauling, Milk-run, Green Logistics]:::transport
        T3[Quản lý rủi ro an toàn<br/>(pin lithium, IATA/DGR, cảm biến)]:::transport
        T4[Mạng lưới 6.100+ đối tác<br/>Kết nối CELLO, chia sẻ định vị]:::transport
        T5[Vận chuyển từ trung tâm bảo hành<br/>về RRCs / Trung tâm tái chế]:::transport
    end

    L3b -->|Kích hoạt| T1 --> T2 --> T3 --> T4 --> T5

    %% Dòng rác thải điện tử đi thẳng vào vận chuyển
    I3 --> T5

    %% ==================== BƯỚC 3: KIỂM TRA, PHÂN LOẠI TẠI RRCs ====================
    subgraph Buoc3 [BƯỚC 3: KIỂM TRA, PHÂN LOẠI & ĐỊNH GIÁ - HẬU PHƯƠNG]
        RRC[<div style="font-size:16px"><b>TRUNG TÂM XỬ LÝ KHU VỰC (RRCs)</b><br/>Xử lý khối lượng lớn</div>]:::rrc
        C1[Công nghệ kiểm tra:<br/>- QINGS (đối chiếu dữ liệu)<br/>- TSI (dự báo lỗi)<br/>- Thị giác máy tính + AI<br/>- Thiết bị đo chuyên dụng]:::rrc
        C2[<div style="font-size:16px"><b>ĐỊNH GIÁ TÀI SẢN THU HỒI</b><br/>4 biến số tài chính</div>]:::rrc
        C3{QUYẾT ĐỊNH PHÂN LUỒNG}:::rrc
    end

    T5 --> RRC --> C1 --> C2 --> C3

    %% ==================== BƯỚC 4: XỬ LÝ CUỐI CÙNG ====================
    subgraph Buoc4 [BƯỚC 4: XỬ LÝ CUỐI CÙNG & TÁI TẠO GIÁ TRỊ]
        P1[<div style="font-size:16px"><b>TÂN TRANG/TÁI SẢN XUẤT</b><br/>Certified Re-Newed<br/>Giảm 40-65% chi phí</div>]:::process
        P2[<div style="font-size:16px"><b>SỬA CHỮA</b><br/>Trả khách / Kho phụ tùng</div>]:::process
        P3[<div style="font-size:16px"><b>THU HỒI LINH KIỆN</b><br/>Phụ tùng chính hãng</div>]:::process
        P4[<div style="font-size:16px"><b>TÁI CHẾ NGUYÊN LIỆU</b><br/>Trung tâm Asan<br/>32.223 tấn (2024)</div>]:::process
    end

    C3 -->|Sản phẩm còn giá trị cao| P1
    C3 -->|Lỗi đơn giản| P2
    C3 -->|Hỏng nặng, linh kiện tốt| P3
    C3 -->|Hỏng hoàn toàn| P4

    %% Vòng lặp DS-DX
    P4 --> Loop[<b>VÒNG LẶP VẬT CHẤT DS-DX</b><br/>Phòng thí nghiệm Kinh tế Tuần hoàn<br/>Tái chế phụ phẩm sản xuất]:::process

    %% ==================== BƯỚC 5: QUẢN TRỊ, GIÁM SÁT & VÒNG LẶP PHẢN HỒI ====================
    subgraph Buoc5 [BƯỚC 5: QUẢN TRỊ, GIÁM SÁT & VÒNG LẶP PHẢN HỒI]
        F1[Tổng hợp dữ liệu từ:]:::feedback
        F1a[• QINGS (Galaxy Consultants)<br/>Mã lỗi, nguyên nhân]:::feedback
        F1b[• CELLO (vận chuyển)<br/>Chi phí, thời gian]:::feedback
        F1c[• RRCs (kiểm tra, định giá)<br/>Kết quả phân luồng]:::feedback

        F2[Báo cáo Phản hồi Chất lượng<br/>hàng tháng]:::feedback
        F3[Gửi đến R&D, Sản xuất,<br/>Quản lý chuỗi cung ứng]:::feedback
        F4[Họp giao ban chất lượng hàng quý]:::feedback
        F5[Cơ chế phản hồi 2 chiều:<br/>R&D phản hồi 14-30 ngày]:::feedback
        F6[Quản trị đối tác G-SRM<br/>71% đối tác đạt Xuất sắc]:::feedback
    end

    L3a -->|Dữ liệu| F1a
    L3b -->|Dữ liệu| F1b
    C1 -->|Dữ liệu| F1c
    F1a & F1b & F1c --> F2 --> F3 --> F4 --> F5
    F6

    F5 ==>|Cải tiến thiết kế| RD[R&D - Thiết kế lại]:::feedback
    F5 ==>|Điều chỉnh quy trình| MFG[Sản xuất]:::feedback
    F5 ==>|Đánh giá lại| SCM[Chuỗi cung ứng]:::feedback

    RD & MFG & SCM ==> Target[<b>GIẢM THIỂU LOGISTICS NGƯỢC<br/>TRONG TƯƠNG LAI</b>]:::feedback

    %% ==================== CHÚ THÍCH ====================
    Note[<b>CHÚ GIẢI:</b><br/>
    • LỚP 1: Tự chẩn đoán từ xa tại nhà (giải quyết 35-40%)<br/>
    • LỚP 1.5: Đại lý - tiếp nhận, chuyển tiếp (kênh phổ biến)<br/>
    • LỚP 2: Trung tâm bảo hành - Galaxy Consultants (tiền tuyến)<br/>
    • LỚP 3: Hệ thống QINGS/CELLO xuyên suốt (tích hợp dữ liệu)<br/>
    • RRCs: Hậu phương xử lý khối lượng lớn, định giá, phân luồng<br/>
    • 3 dòng đầu vào: bảo hành, trả hàng TM, rác thải điện tử]:::feedback
