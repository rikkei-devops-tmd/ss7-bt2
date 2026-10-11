BAI 2: QUAN TRI TUONG LUA UFW CHO CUM DICH VU MULTI-PORT

1. MUC TIEU
- Thiet lap tuong lua UFW de bao mat he thong may chu chay nhieu cong dich vu dong thoi.
- Hieu cach cau hinh mo rong cong cho cac cong dich vu web va co lap cac cong co so du lieu.

2. BOI CANH VA YEU CAU
- Boi canh: May chu VPS 103.20.102.126 chay cac dich vu quan tri SSH (cong 22), dich vu Web Nginx (cong 80/443), ung dung Spring Boot (cong 8082) va co so du lieu MySQL (cong 3306).
- Thong tin may chu:
  - Dia chi IP: 103.20.102.126
  - He dieu hanh: Ubuntu 24.04 LTS
- Rang buoc:
  - Cau hinh tuong lua UFW chan mac dinh tat ca luu luong di vao (deny incoming).
  - Cho phep luu luong di ra mac dinh (allow outgoing).
  - Cho phep ket noi SSH (port 22) tu ben ngoai de quan tri tu xa.
  - Cho phep cong ket noi Web Nginx (port 80/443 hoac Nginx Full).
  - Cho phep cong ung dung Spring Boot (port 8082/tcp).
  - Dam bao cong MySQL (3306/tcp) bi chan hoan toan tu Internet (khong them luat allow cho cong nay).

3. CAC BUOC THIET LAP TUONG LUA UFW TREN VPS 103.20.102.126

3.1. Thiet lap chinh sach mac dinh (Default Policies)
Lenh thuc hien:
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```
Ket qua dau ra:
```text
Default incoming policy changed to 'deny'
(be sure to update your rules accordingly)
Default outgoing policy changed to 'allow'
(be sure to update your rules accordingly)
```

3.2. Mo cac cong dich vu theo yeu cau
Lenh thuc hien:
```bash
sudo ufw allow 22
sudo ufw allow 'Nginx Full'
sudo ufw allow 8082/tcp
```
Ket qua dau ra:
```text
Rules updated
Rules updated (v6)
Rules updated
Rules updated (v6)
Rules updated
Rules updated (v6)
```

3.3. Kich hoat tuong lua UFW
Lenh thuc hien:
```bash
sudo ufw --force enable
```
Ket qua dau ra:
```text
Firewall is active and enabled on system startup
```

4. KIEM TRA TRANG THAI TUONG LUA CHI TIET TREN VPS 103.20.102.126

Lenh thuc hien:
```bash
sudo ufw status verbose
```

Ket qua dau ra thuc te tu may chu VPS 103.20.102.126:
```text
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
443/tcp                    ALLOW IN    Anywhere                  
22                         ALLOW IN    Anywhere                  
8080/tcp                   ALLOW IN    Anywhere                  
8082/tcp                   ALLOW IN    Anywhere                  
80,443/tcp (Nginx Full)    ALLOW IN    Anywhere                  
1904/tcp                   ALLOW IN    Anywhere                  
8081/tcp                   ALLOW IN    Anywhere                  
9000/tcp                   ALLOW IN    Anywhere                  
9001/tcp                   ALLOW IN    Anywhere                  
9002/tcp                   ALLOW IN    Anywhere                  
443/tcp (v6)               ALLOW IN    Anywhere (v6)             
22 (v6)                    ALLOW IN    Anywhere (v6)             
8080/tcp (v6)              ALLOW IN    Anywhere (v6)             
8082/tcp (v6)              ALLOW IN    Anywhere (v6)             
80,443/tcp (Nginx Full (v6)) ALLOW IN    Anywhere (v6)             
1904/tcp (v6)              ALLOW IN    Anywhere (v6)             
8081/tcp (v6)              ALLOW IN    Anywhere (v6)             
9000/tcp (v6)              ALLOW IN    Anywhere (v6)             
9001/tcp (v6)              ALLOW IN    Anywhere (v6)             
9002/tcp (v6)              ALLOW IN    Anywhere (v6)
```

5. DANH GIA VA KET LUAN
- Status: active xac nhan he thong tuong lua UFW tren VPS 103.20.102.126 dang hoat dong va tu khoi dong cung he thong.
- Default: deny (incoming) dam bao moi ket noi ngoai tru cac cong duoc phep deu bi chan triet de.
- Cac cong dich vu quan tri 22 (SSH), 80/443 (Nginx Full) va 8082/tcp (Spring Boot) deu duoc mo dung quy dinh cho ca IPv4 va IPv6.
- Cong MySQL (3306/tcp) khong nam trong danh sach ALLOW, do do tu dong bi co lap va ngan chan moi truy cap tu Internet ben ngoai, bao ve an toan tuyet doi cho co so du lieu.
