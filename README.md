# Bài 1

**a.** Vẽ đồ thị đường 2D biểu diễn hiệu suất xử lý màu theo thời gian ứng với nồng độ xúc tác tại 0,8 và 1,0 g/L. Yêu cầu: đồ thị dạng điểm, các điểm được nối với nhau và 2 đường được vẽ cùng trên một đồ thị.

**b.** Đưa ra phương trình hồi quy tuyến tính (bậc 1) và hệ số tương quan hồi quy R2 của 2 đường trên. Từ đó hãy sử dụng một lệnh để tính giá trị hiệu suất tại phút thứ 65 ứng với từng phương trình.

**c.** Không dựa vào phương trình hồi quy, hãy dự đoán hiệu suất xử lý màu trong 2 trường hợp (0,8 và 1,0 g/L) nếu thực hiện ở phút thứ 65.

**d.** Sử dụng lệnh để chỉ ra các thời điểm hiệu suất xử lý đạt từ 85,00% đến dưới 90,00%

```matlab
clear all
Tg=[10;20;30;40;50;60;70;80;90]
Hs08=[81.06;85.46;84.73;86.93;87.67;86.2;89.13;85.46;88.4]
Hs1=[88.4;91.34;92.8;92.07;93.54;93.54;94.27;93.54;93.54]
scatter(Tg,Hs08)
hold on
scatter(Tg,Hs1)
plot(Tg,Hs1,Tg,Hs08) % câu a
p1=polyfit(Tg,Hs08,1) 
p2=polyfit(Tg,Hs1,1) %tìm điểm nội suy
corr(Tg,Hs08)^2 %hệ số hồi quy
corrcoef(Tg,Hs08).^2
fitlm(Tg,Hs1)
P1=polyval(p1,65) %thay vào ?? tìm điểm 65,polyval của p1 nh? t?c là polyval của phương trình hồi quy này % Câu b
interp1(Tg,Hs08,65) %Dùng cái này sai số ít hơn giảm sai số tối thiểu tối trướcc x trướcc y nội suy thẳng ra số liệu không gian 2 chiều còn 3 chiu thì dùng interp2 Câu C
A=[Tg,Hs08,Hs1]
find(A>=85&A<90)  %?? tìm số liệu Câu D
```

![](C:\Users\Admin 88\AppData\Roaming\Typora\typora-user-images\image-20200925144657995.png)

# Bài 2

Latex 
$$
\frac{\sqrt{x^3+3x-4}}{x-4}+x^3+log_{2}3;
$$
trong đó x là nồng độ chất A và y là tốc độ phản ứng

a) Vẽ đồ thị hàm số trên khoảng nồng độ từ 0 đến 10

b) Xác định thời gian lưu của phản ứng trên khi nồng độ của A thay đổi trong [5,9]?

c) Dùng lệnh để ghi chú lên đồ thị tại vị trí [A]=4 câu ''Tiệm cận của hàm số"?

```matlab
 Cách 2
 y= '(sqrt(x.^3+3*x-4))./(x-4)+x.^3+log(2)/log(3)'
 fplot(y,[0,10])
 S=quad(y,5,9)
 text(4,0,'Tiem can cua ham so')
```

![image-20200927132936033](C:\Users\Admin 88\AppData\Roaming\Typora\typora-user-images\image-20200927132936033.png)

# Bài 3

```matlab
Ca=[0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 1 1.3 2]
r=[0.1 0.3 0.5 0.6 0.5 0.25 0.1 0.06 0.05 0.05 0.04]
RA=1./r;
Ca=Ca';
RA=RA';
plot(Ca,RA)
RA9=interp1(Ca,RA,0.9) %gia tri noi suy Ca truc tung,Ra truc hoanh tai diem 0.9
%kq=['Thoi gian luu: ' num2str(t) ' (phut) '];
%disp(kq)
m=input(' gia tri m: ')
n=input(' gia tri n: ')_
o=find(Ca==m) %phai cho matlab biet minh dang o vi tri nao 
p=find(Ca==n)
KQ=trapz(Ca(o:p),RA(o:p)) %chay tu vi tri ban dau den cuoi
```

# Bài 7

```matlab
Cách 1:
C=input('Nhap nong do (mol/L): ');
r=input('Nhap toc do phan ung (mol/L.s): ');
s=1./r; %L.s/mol
plot(C,s); grid on
a=input('Nhap nong do ban dau (mol/L): ');
b=input('Nhap nong do ung voi do chuyen hoa (mol/L): ');
%c=C*(1-b)
%KO lam duoc nhu sau vi ham FIND ko xac dinh duoc gia tri cua c theo bieu thuc...
...ma chi co the xac dinh duoc khi c la mot gia tri cu the duoc input vao
%b=input('Nhap do chuyen hoa: ');
%c=a*(1-b); %Nong do tai vi tri co do chuyen hoa 80%
%m=find(C==a);
%n=find(C==c);
m=find(C==a);
n=find(C==b);
%Thoi gian luu = S hinh thang
trapz(C(n:m),s(n:m))

%Neu ko may man, gia tri do chuyen hoa dau bai cho ko t/ung voi gia tri C
%va s nao thi phai thuc hien noi suy gia tri C, s roi moi tim vi tri cua 2
%gia tri noi suy do.
%Tuy nhien ham FIND lai ko xac dinh duoc gia tri tinh tu cong thuc ma chi
%xac dinh duoc gia tri la 1 so cu the => tim giai phap khac.
%=> day chua phai cach lam cho bai toan tong quat.
```

```matlab
Cách 2
Ca=[1 2 4 6 8 10];
rA=[0.01 0.02 0.04 0.09 0.16 0.25];
Ra=1./rA;
Ra=Ra';
Ca=Ca';
plot(Ca,Ra),grid on
p1=interp1(Ca,Ra,5)
Ca(3)=5
Ra(3)=p1
o=find(Ca==8)  
p=find(Ca==10)
KQ=trapz(Ca(o:p),Ra(o:p)) 
```

# Giải phương trình bậc 2

```matlab
function pt2(a,b,c)
delta=b^2-4*a*c;
if a==0
    if b==0
        if c==0
            disp('phuong trinh vo so nghiem')
        end
    else
       disp('phuong trinh co mot nghiem duy nhat')
            x=-c/b
    end    
else 
    if delta==0
        disp('phuong trinh co 2 nghiem trung nhau')
        x12=-b/2*a
    elseif delta>0
        disp('phuong trinh co 2 nghiem phan biet')
        x1=-b-sqrt(delta)/2*a
        x2=-b+sqrt(delta)/2*a
    else 
        disp('phuong trinh vo nghiem')
    end
end
```

# Giải Hệ Phương Trình Bậc Nhất 2 Ẩn

```matlab
function hpt(a1,b1,c1,a2,b2,c2)
d=a2/a1;
    if (a1/a2)~=(b1/b2)
        disp('Phuong trinh co mot nghiem duy nhat')
        y=(d*c1-c2)/(d*b1-b2);
        x=(c1-y*b1)/a1;
        fprintf('Gia tri cua x=%d \n',x)
        fprintf('Gia tri cua y=%d \n',y)
    elseif (a1/a2)==(b1/b2)~=(c1/c2)
        disp('Phuong trinh vo nghiem')
    elseif (a1/a2)==(b1/b2)==(c1/c2)
        disp('Phuong trinh vo so nghiem')
    end
end
```

