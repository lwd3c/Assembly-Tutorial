# Chapter 6: Xử lý có điều kiện

- [Chapter 6: Xử lý có điều kiện](#chapter-6-xử-lý-có-điều-kiện)
    - [I. Boolean và Comparison](#i-boolean-và-comparison)
      - [1. Các cờ trạng thái CPU.](#1-các-cờ-trạng-thái-cpu)
      - [2. AND](#2-and)
      - [3. OR](#3-or)
      - [4. XOR](#4-xor)
      - [5. NOT](#5-not)
      - [6. TEST](#6-test)
      - [7. CMP](#7-cmp)
      - [8. Set và Clear Flags](#8-set-và-clear-flags)
    - [II. Các lệnh nhảy có điều kiện](#ii-các-lệnh-nhảy-có-điều-kiện)
    - [III. Vòng lặp có điều kiện](#iii-vòng-lặp-có-điều-kiện)
      - [1. LOOPZ và LOOPE](#1-loopz-và-loope)
      - [2. LOOPNZ và LOOPNE](#2-loopnz-và-loopne)
    - [IV. Cấu trúc có điều kiện](#iv-cấu-trúc-có-điều-kiện)
      - [1. IF](#1-if)
      - [2. Biểu thức phép toán AND](#2-biểu-thức-phép-toán-and)
      - [3. Biểu thức với phép toán OR](#3-biểu-thức-với-phép-toán-or)
      - [4. Vòng lặp WHILE](#4-vòng-lặp-while)
      - [5. Lựa chọn bằng bảng](#5-lựa-chọn-bằng-bảng)
    - [V. Các chỉ thị điều khiển luồng có điều kiện](#v-các-chỉ-thị-điều-khiển-luồng-có-điều-kiện)
      - [1. IF](#1-if-1)
      - [2. .REPEAT](#2-repeat)
      - [3. .WHILE](#3-while)

### I. Boolean và Comparison
#### 1. Các cờ trạng thái CPU.

![alt text](/Chapter-6/images/image.png)

#### 2. AND
 
 ![alt text](/Chapter-6/images/image-1.png)

#### 3. OR
 
 ![alt text](/Chapter-6/images/image-2.png)

#### 4. XOR
 
 ![alt text](/Chapter-6/images/image-3.png)

#### 5. NOT
 
 ![alt text](/Chapter-6/images/image-4.png)

#### 6. TEST
- Để thực hiện AND mà không làm thay đổi giá trị của bất kì toán hạng nào và để kiểm tra điều kiện, ta sử dụng TEST.
- TEST thực hiện AND 2 toán hạng nhưng không lưu kết quả, chỉ ảnh hưởng tới các cờ CPU.
  
![alt text](/Chapter-6/image-5.png)
 
#### 7. CMP
- So sánh đích với nguồn (thực hiện phép trừ nhưng đích không bị thay đổi).
- Cú pháp: 	CMP des, sou
- Ví dụ:
 
 ![alt text](/Chapter-6/image-6.png)
  
  ![alt text](/Chapter-6/image-7.png)

- Với số nguyên có dấu:
 
 ![alt text](/Chapter-6/image-8.png)

#### 8. Set và Clear Flags
 
 ![alt text](/Chapter-6/image-9.png)

### II. Các lệnh nhảy có điều kiện
- Lệnh nhảy có điều kiện: phân nhánh tới 1 label được chỉ định dựa trên trạng thái các thanh ghi hoặc các cờ trên CPU.
- Cụ thể:
  
 ![alt text](/Chapter-6/image-10.png)
 
 ![alt text](/Chapter-6/image-11.png)

 ![alt text](/Chapter-6/image-12.png)

 ![alt text](/Chapter-6/image-13.png)

### III. Vòng lặp có điều kiện
#### 1. LOOPZ và LOOPE
- Cú pháp:	LOOPE des
		LOOPZ des
- Logic: 	+ ECX <- ECX – 1
		+ if ECX > 0 and ZF = 1, jump to des 
- Dùng để duyệt 1 mảng và tìm phần tử đầu tiên khác với giá trị chỉ định.
#### 2. LOOPNZ và LOOPNE
- Cú pháp:	LOOPNE des
		LOOPNZ des
- Logic: 	+ ECX <- ECX – 1
		+ if ECX > 0 and ZF = 0, jump to des 
- Dùng để duyệt 1 mảng và tìm phần tử đầu tiên trùng với giá trị chỉ định.
### IV. Cấu trúc có điều kiện
#### 1. IF
 
 ![alt text](/Chapter-6/images/image-14.png)

 ![alt text](/Chapter-6/images/image-15.png)
 
#### 2. Biểu thức phép toán AND
- Dùng để kiểm tra nhiều điều kiện cùng lúc.
 
 ![alt text](/Chapter-6/images/image-16.png)

#### 3. Biểu thức với phép toán OR
- Dùng để kiểm tra điều kiện nhảy  tới 1 label khi ít nhất 1 trong các điều kiện được đáp ứng.
 
 ![alt text](/Chapter-6/images/image-17.png)

#### 4. Vòng lặp WHILE
 
 ![alt text](/Chapter-6/images/image-18.png)

#### 5. Lựa chọn bằng bảng
- Thay thế cấu trúc lựa chọn đa hướng bằng sử dụng bảng tra cứu.
- Các bước thực hiện:
+ Step 1: Tạo bảng chứa các giá trị cần tra cứu và các địa chỉ offset của label hoặc thủ tục tương ứng.
 
 ![alt text](/Chapter-6/images/image-19.png)
 
 ![alt text](/Chapter-6/images/image-20.png)

+ Step 2: Sử dụng vòng lặp để tìm trong bảng. Khi tìm thấy, nhảy tới nhãn hoặc thủ tục tương ứng trong bảng.
 
 ![alt text](/Chapter-6/images/image-21.png)

### V. Các chỉ thị điều khiển luồng có điều kiện
#### 1. IF
#### 2. .REPEAT
- Thực thi phần thân vòng lặp trước khi kiểm tra điều kiện lặp được liên kết với .UNTIL.
 
 ![alt text](/Chapter-6/images/image-22.png)

#### 3. .WHILE
- Kiểm tra điều kiện lặp trước khi thực thi phần thân vòng lặp.
- Lệnh .ENDW đánh dấu sự kết thúc vòng lặp.
 
 ![alt text](/Chapter-6/images/image-23.png)