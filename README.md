# Bài 1. Vách trụ hai lớp đường kính tròn cùng d1 = 20 cm, bề dày và hệ số dẫn nhiệt hai lớp tương ứng là δ1 = 2 cm, λ1 = 1.2 W/m.độ và δ2 = 3 cm, λ2 = 0.8 W/m.độ. Nhiệt độ mặt trong cùng và ngoài cùng là tm1 = 80°C, tm2 = 20°C. Xác định:
**a. Dòng
điện dài qL qua vách nhiệt độ tại chỗ tiếp xúc?

**b. Mật độ dòng tại chỗ tiếp xúc?

**c. Gradt tại mặt trong cùng?

# Code mẫu

**bai1.m**
```matlab
function bai1
delta = input('Nhap ma tran gia tri do day (m) :');
lamda = input('Nhap ma tran co he so dan nhiet (W/m.k): ');
t1=input('Nhap gia tri nhiet do lop trong cung: ');
t2=input('Nhap gia tri nhiet do lop ngoai cung: ');
qL=input('Nhap nhiet luong cua dong: ');
d1 = input('Duong kinh cua lop trong cung: '),
% nhap 'phang' neu can tinh vach phang
% nhap 'tru' neu can tinh vach tru
barrier = 'tru';
R = nhiettro(barrier,lamda,delta,d1);
if strcmp(t1,'no')
    t1=t2+q/sum(R);
elseif strcmp(t2,'no')
    t2=t1-q/sum(R);
elseif strcmp(qL,'no')
    disp('Gia tri cua qL la :')
    qL=density(t1,t2,R);
end
disp('Mat do dong tai lop tiep xuc');
q = qtiepxuc(qL,d1,delta);
disp('Gia tri cua gradien');
gradt = gradiel(q,lamda)
```

**nhietttro.m**
```matlab
function R = nhiettro(barrier,lamda, delta,d1)
d(1) = d1
for i = 1:length(delta),
d(i+1) = d(i)+2*delta(i),
R(i) = 1/(2*pi*lamda(i))*log(d(i+1)/d(i)),
end
end
```

**density.m**
```matlab
function qL=density(t1,t2,R)
    qL=(t1-t2)/sum(R),     
end
```

**gradiel.m**
```matlab
function gradt = gradiel(q,lamda)
if q>0
  for i = 1:length(lamda)
    gradt(i) = q/lamda(i);
  end
end
end
```

**nhietdotiepxuc.m**
```matlab
function ttx = nhietdotiepxuc(q,t1,R)
ttx(1) = t1-q*R(1);
for i = 2:length(R)
ttx(i) = ttx(i-1)-q*R(i);
end
```

**qtiepxuc.m**
```matlab
function q = qtiepxuc(qL,d1,delta)
    d(1) = d1;
    for i = 1:length(delta),
    d(i+1) = d(i)+2*delta(i);
    if i>=2 
        q(i)=qL/(pi*d(i));
    end
    end
end
```
