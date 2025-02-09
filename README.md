# Dialog for Windows

## 初期設定

`npm install`

`npm ci`

## 証明書の設定（既存のものを使う場合は、省略してください。）

Open SSH の使用の場合

### 1. 秘密鍵 (key.pem) の作成

RSA 4096bit の秘密鍵を作成する

`openssl genpkey -algorithm RSA -out key.pem -pkeyopt rsa_keygen_bits:4096`

key.pem (秘密鍵) が生成されます。

### 2. 公開鍵 (perms.pub.pem) の作成

作成した秘密鍵 (key.pem) から公開鍵 (perms.pub.pem) を抽出

`openssl rsa -in key.pem -pubout -out perms.pub.pem`

perms.pub.pem (公開鍵) が生成されます。

### 3. 証明書署名要求 (CSR) の作成

証明書を作成するための csr.pem を作成

`openssl req -new -key key.pem -out csr.pem`

実行すると、以下のような情報を求められます

Country Name (2 letter code) [AU]:

State or Province Name (full name) [Some-State]:

Locality Name (eg, city) []:

Organization Name (eg, company) [Internet Widgits Pty Ltd]:

Organizational Unit Name (eg, section) []:

Common Name (e.g. server FQDN or YOUR name) []: localhost

Email Address []:

Common Name は localhost などを指定。

Email Address は空でも OK。

### 4. 自己署名証明書 (cert.pem) の作成

csr.pem を使って、cert.pem を作成：

`openssl x509 -req -days 365 -in csr.pem -signkey key.pem -out cert.pem`

-days 365 は証明書の有効期限 (1 年)。

cert.pem (自己署名証明書) が生成されます。

CSR (csr.pem) は不要なので削除してもよい

### 5. 保存場所

certs フォルダに、key.pem、cert.pem、perms.pub.pem を保存してください。

perms.pub.pem の内容は、reticulum に使用します。

## 起動

`npm start`
