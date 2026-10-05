BAI 2: QUAN TRI TUONG LUA UFW CHO CUM DICH VU MULTI-PORT

1. MUC TIEU
- Thiet lap tuong lua UFW de bao mat he thong may chu chay nhieu cong dich vu dong thoi.
- Hieu cach cau hinh mo rong cong cho cac cong dich vu web va co lap cac cong co so du lieu.

2. BOI CANH VA YEU CAU
- Boi canh: May chu chay 4 dich vu gom SSH quan tri (cong 22), Nginx web (cong 80), ung dung Spring Boot (cong 8082) va co so du lieu MySQL (cong 3306).
- Rang buoc:
  - Cau hinh tuong lua UFW chan mac dinh tat ca luu luong di vao (deny incoming).
  - Cho phep luu luong di ra mac dinh (allow outgoing).
  - Cho phep ket noi SSH (port 22/tcp) tu ben ngoai.
  - Cho phep cong ket noi Web HTTP tieu chuan (port 80/tcp).
  - Cho phep cong ung dung Spring Boot (port 8082/tcp) de kiem tra tu xa.
  - Dam bao cong MySQL (3306/tcp) bi chan hoan toan tu Internet (khong them luat allow cho cong nay).

3. CAC BUOC THIET LAP TUONG LUA UFW

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
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
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

4. KIEM TRA TRANG THAI TUONG LUA CHI TIET

Lenh thuc hien:
```bash
sudo ufw status verbose
```

Ket qua dau ra:
```text
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere
80/tcp                     ALLOW IN    Anywhere
8082/tcp                   ALLOW IN    Anywhere
22/tcp (v6)                ALLOW IN    Anywhere (v6)
80/tcp (v6)                ALLOW IN    Anywhere (v6)
8082/tcp (v6)              ALLOW IN    Anywhere (v6)
```

5. DANH GIA VA KET LUAN
- Status: active xac nhan he thong tuong lua UFW dang hoat dong va tu khoi dong cung he thong.
- Default: deny (incoming) dam bao moi ket noi ngoai tru cac cong duoc phep deu bi chan triet de.
- Cac cong dich vu 22/tcp (SSH), 80/tcp (HTTP), 8082/tcp (Spring Boot) duoc mo dung quy dinh cho ca IPv4 va IPv6.
- Cong MySQL (3306/tcp) khong nam trong danh sach ALLOW, tu dong bi co lap va ngan chan moi truy cap tu Internet ben ngoai.
