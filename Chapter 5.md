Chapter 5: Procedures
Procedures (các thủ tục): là các khối mã lệnh được xác định và gọi từ các vị trí khác nhau trong chương trình, giúp chương trình tổ chức mã nguồn thành các phần dễ quản lý và tái sử dụng.
I. Hoạt động Stack
1. Runtime Stack.
Được quản lý bởi CPU, sử dụng 2 thanh ghi:
- SS (stack segment)
- ESP (stack pointer)
2. PUSH
 
3. POP
 
4. Hướng dẫn liên quan
- PUSHFD và POPFD: push và pop thanh ghi EFLAGS.
- PUSHAD: push các thanh ghi đa năng 32-bit vào stack (EAX, ECX, EDX, EBX, ESP, EBP, ESI, EDI).
- POPAD: pop các thanh ghi ra khỏi stack theo thứ tự ngược lại.
- PUSHA và POPA: thực hiện tương tự  với thanh ghi 16-bit.
II. Xác định và sử dụng các thủ tục
1. CALL và RET
- CALL: gọi 1 thủ tục
	+ push địa chỉ của lệnh tiếp theo vào stack.
	+ Sao chép địa chỉ thủ tục được gọi vào EIP/RIP.
- RET: trở về từ 1 thủ tục
	+ Pop địa chỉ trả về từ Stack
	+ Sao chép địa chỉ đó vào EIP/RIP
2. Parameters
- 1 thủ tục tốt có thể được sử dụng ở nhiều chương trình nếu nó không để cập đến tên biến cụ thể.
- Tham số giúp cho thủ tục linh hoạt bởi giá trị của tham số có thể thay đổi trong quá trình chạy.
 
3. USES
- USES: tự động lưu và khôi phục các thanh ghi được liệt kê khi vào và ra khỏi 1 thủ tục.
III. Liên kết với thư viện ngoài
1. Liên kết thư viện.
- 1 file bao gồm các thủ tục đã được biên dịch thành mã máy, được xây dựng từ 1 hoặc nhiều file OBJ.
- Để build 1 thư viện:
	+ Bắt đầu với 1 hoặc nhiều file ASM.
	+ Tập hợp thành 1 file OBJ.
	+ Tạo file thư viện rỗng ( .LIB)
	+ Thêm file OBJ vào file thư viện, sử dụng Microsoft LIB.
2. Cách hoạt động.
- Chương trình của bạn liên kết với Irvine32.lib bằng lệnh liên kết bên trong 1 file tên make32.bat.
- Chú ý 2 file LIB: Irvine32.lib và kernel32.lib
IV. Thư viện Irvine32
1. Gọi thủ tục thư viện Irvine32.
- Để gọi các thủ tục từ thư viện Irvine32, dùng INCLUDE để bao gồm các khai báo của các thủ tục và dung CALL để gọi các thủ tục này.
 
* Tổng quát các thủ tục:
CloseFile: đóng 1 tệp đĩa đang mở.
Clrscr: xóa màn hình console và đặt con trỏ về góc trên bên trái.
CreatOutputFile: tạo 1 tệp đĩa mới để ghi dữ liệu trong chế độ output.
Crlf: ghi kế tự kết thúc dòng (CRLF) vào console.
Delay: tạm dừng thực thu trong khoảng thời gian n mili giây.
DumpMem: ghi 1 khối bộ nhớ ra đầu ra chuẩn dưới dạng Hex.
DumpRegs: hiển thị các thanh ghi mục đích chung và cờ dưới dạng Hex.
GetCommandtail: sao chép các tham số dòng lệnh vào 1 mảng bytes.
GetDateTime: lấy ngày và giờ hiện tại từ hệ thống.
GetMaxXY: lấy số cột và hàng trong bộ đệm console.
GetMseconds: trả về số mili giây đã trôi qua từ nửa đêm.
GetTextColor: trả về màu nền và chữ trong console.
Gotoxy: đặt con trỏ tại hang và cột trên console.
IsDigit: đặt cờ Zero nếu AL chứa mã ASCII của chữ số thập phân (0-9).
MsgBox: MsgBoxAsk: hiển thị hộp thoại tin nhắn.
OpenInputFile: mở tệp hiện có để đọc dữ liệu.
ParseDecimal32: chuyển đổi chuỗi số nguyên không dấu thành nhị phân.
ParseInteger32: chuyển đổi chuỗi số nguyên có dấu thành nhị phân.
Random32: sinh số nguyên ngẫu nhiên 32-bit trong phạm vi 0 – FFFFFFFFh.
Randommize: khởi tạo bộ sinh số ngẫu nhiên.
RandomRange: sinh số nguyên ngẫu nhiên trong phạm vi xác định.
ReadChar: đọc 1 kí tự từ đầu vào chuẩn.
ReadDec: đọc 1 số nguyên không dấu 32-bit từ bàn phím.
ReadFromFile: đọc dữ liệu từ file vào bộ đệm.
ReadHex: đọc 1 số nguyên 32-bit dưới dạng Hex từ bàn phím.
ReadInt: đọc 1 số nguyên có dấu 32-bit từ bàn phím.
ReadKey: đọc 1 kí tự từ bộ đệm đầu vào bàn phím.
ReadString: đọc 1 chuỗi từ stdin, kết thúc bằng [Enter].
SetTextColor: thiết lập màu chữ và nền console.
Str_compare: so sánh 2 chuỗi.
Str_copy: sao chép 1 chuỗi nguồn vào đích.
Str_lenght: trả về độ dài chuỗi trong EAX.
Str_trim: loại bỉ ký tự không mong muốn khỏi 1 chuỗi.
Str_ucase: chuyển thành chuỗi in hoa.
WaitMsg: hiển thị thông điệp cho tới khi ấn Enter.
WriteBin: ghi số nguyên không dấu 32-bit dưới dạng ASCII.
WriteBinB: ghi số nguyên nhị phân dưới dạng byte, word hoặc dword.
WriteChar: ghi 1 kí tự đơn lên console.
WriteDec: ghi số nguyên không dấu 32-bit dưới dạng thập phân.
WriteHex: ghi số nguyên không dấu 32-bit dưới dạng Hex.
WriteHexB: ghi số nguyên Hex dưới dạng byte, word hoặc dword.
WriteInt: ghi số nguyên có dấu 32-bit dưới dạng thập phân.
WriteStackFrame: ghi khung stack của thủ tục hiện tại lên console.	
WriteStackFrameName: ghi tên thủ tục hiện tại và khung stack của nó lên console.
WriteString: ghi chuỗi kết thúc bằng null lên console.
WriteToFile: ghi bộ đệm vào tệp đầu ra.
WriteWindowsMsg: hiển thị thông báo lỗi gần đây nhất được tạo bởi MS-Windows.

V. Thiết kế chương trình sử dụng thủ tục
- Thiết kế từ trên xuống, bao gồm:
	+ Thiết kế chương trình trước khi code.
	+ Chia nhiệm vụ lớn thành các nhiệm vụ nhỏ hơn.
	+ Sử dụng cấu trúc phân cấp dựa trên lời gọi thủ tục.
	+ Kiểm tra các thủ tục riêng biệt.
- Ví dụ:
 
 
VI. 64-Bit Assembly Programming
1. The x64 Calling Convention.
- Sử dụng với 64-bit Windows API.
- Lệnh CALL trừ 8 từ RSP.
- 4 tham số đầu tiên được đặt trong RCX, RDX, R8 và R9.
- Phải cấp phát ít nhất  32 bytes không gian bóng trên stack.
- Khi gọi 1 hàm con, con trỏ stack phải căn chỉnh 16 byte.
