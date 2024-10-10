# Chapter 4: Truyền dữ liệu, Địa chỉ và Số học

- ## **Contents**
  - [I. Truyền dữ liệu](#i-truyền-dữ-liệu)
    - [1. Các loại toán hạng](#1-các-loại-toán-hạng)
    - [2. Toán hạng bộ nhớ trực tiếp](#2-toán-hạng-bộ-nhớ-trực-tiếp)
    - [3. Lệnh MOV](#3-lệnh-mov)
    - [4. Zero Extension](#4-zero-extension)
    - [5. Sign Extension](#5-sign-extension)
    - [6. XCHG](#6-xchg)
  - [II. Addition  and Subtraction](#ii-addition--and-subtraction)
    - [1. INC và DEC](#1-inc-và-dec)
    - [2. ADD và SUB](#2-add-và-sub)
    - [3. NEG](#3-neg)
    - [4. Thực hiện biểu thức số học.](#4-thực-hiện-biểu-thức-số-học)
    - [5. Cờ bị ảnh hưởng bởi số học.](#5-cờ-bị-ảnh-hưởng-bởi-số-học)
    - [6. Số nguyên có dấu và không dấu.](#6-số-nguyên-có-dấu-và-không-dấu)
  - [III. Những chỉ thị và toán tử liên quan đến dữ liệu](#iii-những-chỉ-thị-và-toán-tử-liên-quan-đến-dữ-liệu)
    - [1. OFFSET](#1-offset)
    - [2. PTR](#2-ptr)
    - [3. TYPE](#3-type)
    - [4. LENGTHOF: đếm số lượng phần tử trong 1 khai báo dữ liệu.](#4-lengthof-đếm-số-lượng-phần-tử-trong-1-khai-báo-dữ-liệu)
    - [5. SIZEOF: trả về giá trị (LENGTHOF \* TYPE).](#5-sizeof-trả-về-giá-trị-lengthof--type)
    - [6. LABEL](#6-label)
  - [IV. Địa chỉ gián tiếp](#iv-địa-chỉ-gián-tiếp)
    - [1. Toán hạng gián tiếp.](#1-toán-hạng-gián-tiếp)
    - [2. Ví dụ tính tổng 1 mảng.](#2-ví-dụ-tính-tổng-1-mảng)
    - [3. Toán hạng có chỉ mục.](#3-toán-hạng-có-chỉ-mục)
    - [4. Con trỏ.](#4-con-trỏ)
  - [V. JMP và LOOP](#v-jmp-và-loop)
    - [1. JMP](#1-jmp)
    - [2. LOOP](#2-loop)
    - [3. Tính tổng 1 mảng số nguyên.](#3-tính-tổng-1-mảng-số-nguyên)
    - [4. Sao chép 1 chuỗi.](#4-sao-chép-1-chuỗi)
  - [VI. 64-Bit Programming](#vi-64-bit-programming)


## I. Truyền dữ liệu

### 1. Các loại toán hạng

- Giá trị tức thời (hằng số): là các số nguyên không đổi (8, 16 hoặc 32bits) được mã hóa trong lệnh.
    > Vd: 10, 0x1A, 1234h, …
- Thanh ghi: tên của thanh ghi được chuyển thành số và mã hóa trong lệnh.
	> Vd: AH, AL, AX , BX, SI, DI, EAX, EBX, ESI, ESP, … 
- Địa chỉ bộ nhớ: tham chiếu tới 1 vị trí trong bộ nhớ, địa chỉ bộ nhớ được mã hóa trong lệnh hoặc 1 thanh ghi.
	> Vd: [1234h], [BX], [BX + SI], [CS:1234H], …

### 2. Toán hạng bộ nhớ trực tiếp

- 1 toán hạng bộ nhớ trực tiếp là 1 tham chiếu có tên (Label) tới vùng lưu trữ trong bộ nhớ.
- Label được tự động giải mã thành địa chỉ cụ thể bởi trình biên dịch.
  
### 3. Lệnh MOV

- Di chuyển dữ liệu từ nguồn(source) tới đích(destination).
	
    ``` MOV  destination, source ```

- CS, EIP, IP  và hằng số không thể là đích đến.
- Không thể MOV trực tiếp tới thanh ghi phân đoạn(CS, DS,..)
- Không thể MOV từ bộ nhớ tới bộ nhớ. 
  
### 4. Zero Extension

- Khi copy 1 giá trị nhỏ hơn vào 1 đích lớn hơn, lệnh MOVZX sẽ lấp đầy nửa trên của đích bằng số 0.
- Đích phải là 1 thanh ghi, nguồn không thể là hằng số.
    > Vd : MOVZX AX, BX

### 5. Sign Extension

- Lệnh MOVSX sẽ lấp đầy nửa trên của đích bằng 1 bản sign bit của nguồn.
- Đích phải là 1 thanh ghi, nguồn không thể là hằng số.
    > Vd: MOVSX AX, BL

### 6. XCHG 

- XCHG hoán đổi giá trị của 2 toán hạng. Ít nhất 1 toán hạng là 1 thanh ghi. Không thể là hằng số.
    > Vd: XCHF AX, BX

## II. Addition  and Subtraction

### 1. INC và DEC

 - INC: cộng thêm 1 vào toán hạng đích.
    
    ```INC des```
- DEC: trừ đi 1 ở toán hạng đích.
  
    ```DEC des```

### 2. ADD và SUB

- ADD: cộng nguồn vào đích
  
	```ADD destination, source```
- SUB: trừ nguồn vào đích
  
	```SUB destiantion, source```
- Quy tắc giống MOV.
  
### 3. NEG 
- Đảo ngược dấu của toán hạng. Toán hạng có thể là thanh ghi hoặc bộ nhớ.
- Bất kì toán hạng nào khác 0 đều khiến Carry flag được thiết lập.
![alt text](/Chapter-4/images/image.png)

### 4. Thực hiện biểu thức số học.

![alt text](/Chapter-4/images/image-1.png)

### 5. Cờ bị ảnh hưởng bởi số học.

- ALU (đơn vị tính toán và logic trong CPU) có 1 số cờ trạng thái để phản ánh kết quả các phép toán số học ( và bitwise), dựa trên nội dung của toán hạng đích.
- Flag set khi nó bằng 1 và clear khi nó bằng 0.
- Những cờ cần thiết:
	- Zero flag (ZF) – thiết lập khi kết quả bằng 0, dùng để kiểm tra điều kiện = 0.
	- Sign flag (SF) – thiết lập khi đích mang dấu âm, dùng để kiểm tra điều kiện số âm.
	- Carry flag (CF) – thiết lập = 1 khi kết quả phép tính unsigned làm tràn qua giới hạn 1 thanh ghi.
	- Overflow flag (OF) – thiết lập = 1 khi kết quả phép tính signed làm tràn qua giới hạn 1 thanh ghi. 

![alt text](/Chapter-4/images/image-2.png)

### 6. Số nguyên có dấu và không dấu.

- Tất vả CPU đều hoạt động giống nhau trên cả 2 loại.
- CPU không phân biệt số có dấu hay không dấu.
- Quy tắc: Khi cộng 2 số nguyên, cờ OF chỉ được set khi:
	+ 2 số dương cộng lại và tổng là số âm.
	+ 2 số âm cộng lại và tổng là số dương.
  
## III. Những chỉ thị và toán tử liên quan đến dữ liệu

### 1. OFFSET

- OFFSET trả về khoảng cách tính bằng byte từ 1 label đến đầu của đoạn chứa nhãn đó.
  
  > ![alt text](/Chapter-4/images/image-3.png)

- Giá trị trả về bởi OFFSET là 1 con trỏ.
  
  > ![alt text](/Chapter-4/images/image-4.png)

-  ALIGN: căn chỉnh 1 biến hoặc dữ liệu trên 1 ranh giới byte, word, dword hoặc paragraph.
  
### 2. PTR

- Ghi đè nhãn, biến mặc định. Cung cấp truy cập linh hoạt vào 1 phần của biến.
- Thứ tự Little endian được sử dụng trong lưu trữ dữ liệu trong bộ nhớ của Intel.
- Số nguyên nhiều byte được lưu trữ theo thứ tự ngược lại, với byte ít quan trọng nhất được lưu ở địa chỉ thấp nhất.
    > Vd: 12345678h => 78 56 34 12
- Khi số nguyên được tải từ bộ nhớ vào thanh ghi, các byte được tự động đảo ngược lại theo đúng vị trí.
- PTR cũng được dùng để kết hợp các phần tử của kiểu dữ liệu nhỏ hơn và chuyển chúng tới toán hạng lớn hơn. CPU sẽ tự động đảo ngược các byte.

    > ![alt text](/Chapter-4/images/image-5.png)

### 3. TYPE

- TYPE trả về kích thước bằng byte của 1 phần tử khai báo dữ liệu.
 
    > ![alt text](/Chapter-4/images/image-6.png)

### 4. LENGTHOF

- LENGTHOF đếm số lượng phần tử trong 1 khai báo dữ liệu.

    > ![alt text](/Chapter-4/images/image-7.png)

### 5. SIZEOF

- SIZEOF trả về giá trị (LENGTHOF * TYPE).
 
    >![alt text](/Chapter-4/images/image-8.png)

- **Trải dài nhiều dòng**: Khai báo dữ liệu trải dài trên nhiều dòng nếu mỗi dòng (trừ dòng cuối cùng) kết thúc bằng dấu phẩy. LENGTHOR và SIZEOF bao gồm tất cả các dòng thuộc khai báo.
 
    > ![alt text](/Chapter-4/images/image-9.png)

### 6. LABEL

- Gán 1 tên nhãn thay thế và loại cho 1 vị trí lưu trữ đã tồn tại.
- LABEL không cấp phát bộ nhớ cho riêng nó.
- Loại bỏ sự cần thiết của PTR trong 1 số trường hợp.
 
    > ![alt text](/Chapter-4/images/image-10.png)

## IV. Địa chỉ gián tiếp

### 1. Toán hạng gián tiếp.

- 1 toán hạng gián tiếp chứa địa chỉ của 1 biến, thường là 1 mảng hoặc chuỗi. Nó có thể được giải mã như con trỏ.

    > ![alt text](/Chapter-4/images/image-11.png)

- Sử dụng PTR để làm rõ kích thước của toán hạng bộ nhớ.
  
### 2. Ví dụ tính tổng 1 mảng.

> ![alt text](/Chapter-4/images/image-12.png)

### 3. Toán hạng có chỉ mục.

- Toán hạng có chỉ mục thêm 1 hằng số vào thanh ghi để tạo ra 1 địa chỉ hiệu quả. Gồm 2 kiểu:
	
    ```[Label + Reg]```
    ```Label[Reg]```

    > ![alt text](/Chapter-4/images/image-13.png)

- **Chia tỉ lệ chỉ mục**: bạn có thể chia tỷ lệ 1 toán hạng gián tiếp hoặc toán hạng được lập chỉ mục theo offset của phần tử mảng. Thực hiện bằng cách nhân chỉ mục với TYPE của mảng.

    > ![alt text](/Chapter-4/images/image-14.png)

### 4. Con trỏ.
- Bạn có thể khai báo 1 biến con trỏ chứa offset của 1 biến khác.
  
    > ![alt text](/Chapter-4/images/image-15.png)

## V. JMP và LOOP

### 1. JMP

- JMP là nhảy không điều kiện tới nhãn mà thường nằm trong cùng 1 thủ tục. Khhi JMP thực thi, luồng điều khiển sẽ chuyển đến nhãn chỉ định mà không kiểm tra điều kiện nào.
    ```
    Cú pháp: JMP target
    Logic: EIP <- target
    ```

### 2. LOOP

- LOOP: tạo 1 vòng lặp.
    ```
    Cú pháp: LOOP target
    Logic:   	ECX <- ECX -1 
    If ECX != 0, jump to target
    ```
    
- Trình biên dịch tính khoảng cách bằng byte giữa offset của the following instruction và offset của target label. Được gọi là offset tương đối, được thêm vào EIP.
    > VD:
    > 
    > ![alt text](/Chapter-4/images/image-16.png)
- Vòng lặp lồng nhau: nếu bạn cần code 1 vòng lặp trong 1 vòng lặp, bạn phải lưu giá trị ECX của vòng lặp ngoài.
 
    > ![alt text](/Chapter-4/images/image-17.png)

### 3. Tính tổng 1 mảng số nguyên.

> ![alt text](/Chapter-4/images/image-18.png)

### 4. Sao chép 1 chuỗi.

> ![alt text](/Chapter-4/images/image-19.png)

## VI. 64-Bit Programming

- MOV trong 64-bit chấp nhận toán hạng 8, 16, 32 hoặc 64 bits.
- Khi chuyển 1 hằng số 8, 16 hoặc 32-bit vào 1 thanh ghi 64-bit, các bit trên của đích sẽ được xóa (đặt thành 0). 
- Khi chuyển 1 toán hạng bộ nhớ tới thanh ghi 64-bit:
	+ Di chuyển 32-bit: xóa các bit trên ở đích (đặt thành 0).
	+ Di chuyển 8 và 16-bit: không ảnh hướng tới các bit cao của đích.
- MOVSXD: mở rộng 1 giá trị 32 có dấu thành 1 giá trị 64 và lưu vào thanh ghi 64.
- OFFSET tạo ra 1 địa chỉ 64-bit.
- LOOP sử dụng thanh ghi RCX để đếm vòng lặp.
- RSI và RDI là các thanh ghi lưu chỉ số phổ biến nhất trong truy cập mảng.
- ADD và SUB ảnh hướng tới các cờ như trong 32-bit mode.
