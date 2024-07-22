# ネットワーク基礎概念
## 用語集
- DNS (Domain Name System)：ホスト名とIPアドレスの対応付けを行う
- FQDN (Fully Qualified Domain Name)：完全修飾ドメイン名
- NIC (Network Interface Card)
- MAC (Media Access Control)
- PCI (Protocol Control Information)
- ICI (Interface Control Information)
- SDU (Service Data Unit)：積み荷だけ
- PDU (Protocol Data Unit)：積み荷＋木簡
- UDP (User Datagram Protocol)：コネクション取らずに送り付ける。軽い。Broadcast
- TCP (Transmission Control Protocol)：コネクション取る。信頼性。１対１
- HTTP (Hypertext Transfer Protocol)
- SSL/TLS (Secure Sockets Layer/Transport Layer Security)：公開鍵暗号系利用。改竄検出
- PKI (Public Key Infrastructure)：公開鍵基盤、証明書の正しさをCAが保証
- CA (Certificate Authority)：公開鍵証明書の認証局
- DV (Domain Validation)：ドメイン認証
- A, AAAA：FQDN → IPアドレス
- CNAME (Canonical NAME)：ホストの別名を登録FQDN → FQDN
- MX：メールドメイン → メールサーバー
- CDN (Content Delivery Network)：Webコンテンツを世界に配信するネットワーク
- ALOHA：競合形MAC、自己中送信
- CSMA (Carrier Sense Multiple Access)：競合形MAC、空気読み送信
- CSMA/CD (Collision Detection)：送受信を同時にするので、衝突を検出できる
- CSMA/CA (Collision Avoidance)：衝突を検出できない
- FEC (Forward Error Correction)：前方誤り訂正、受信側が直しちゃう
- ARQ (Automatic Repeat reQuest)：自動再送要求、データリンク層・トランスポート層
- Stop and Wait ARQ：１つずつ確認しつつ送る
- Go-back-N ARQ：まとめて送り、失敗したところからやり直す
- 選択的再送ARQ：まとめて送り、失敗したのだけやり直す
- ACK (Acknowledgement)：成功
- NAK (Negative Acknowledgement)：失敗
- ARP (Address Resolution Protocol)：アドレス関係を探索する
- DHCP (Dynamic Host Configuration Protocol)：IPアドレスやDNSを自動割り当て
- VCI (Virtual Channel Identifier)：Virtual Channel型の識別用
- RIB (Routing Information Base)：経路作成のための情報
- FIB (Forwarding Information Base)：ルータが経路決定に使う表
- ICMP (Internet Control Message Protocol)：IPの補助メッセージ
- ECN (Explicit Congestion Notification)：明示的な輻輳通知
- AM (Amplitude Modulation)：振幅変調
- PM (Phase Modulation)：位相変調
- FM (Frequency Modulation)：周波数変調
- ASK (Amplitude Shift Keying)：振幅シフトキー方式
- APSK (Amplitude Phase Shift Keying)：多値変調方式の１つ
- QAM (Quadrature Amplitude Modulation)：2bit/信号の4QAM、4bit/信号の16QAM
- FDMA (Frequency Division Multiple Access)：周波数分割多元接続
- TDMA (Time Division Multiple Access)：時分割多元接続
- CDMA (Code Division Multiple Access)：符号分割多元接続
- FDD (Frequency Division Duplex)：異なる周波数帯を利用した１伝送路の路双方向通信
- TDD (Time Division Duplex)：異なる時間で１伝送路の双方向通信
- FDM (Frequency Division Multiplexing)：周波数の多重化（１伝送路で複数の通信）
- TDM (Time Division Multiplexing)
- CDM (Code Division Multiplexing)
- PN (Pseudo Noise)信号：直接拡散方式によるスペクトラム拡散、多元接続に使うノイズ


## IP アドレス

- 各ネットワーク機器やインタフェースを識別するための番号
- IPv4では32ビットで表現
- 例: 158.199.240.27
- 8ビット（0-255）ごとに区切って表記
- 論理アドレスとも呼ばれる（物理アドレスとの対比）

### 物理アドレスと論理アドレスの違い

- 物理アドレス：各機器に基本固定で割り振るもの
- 論理アドレス：ネットワーク接続状況に応じて割り振るもの
  - Wi-Fi接続先を変えると論理アドレスは変わるが、物理アドレスは同じ
  - Wi-Fiと有線LANで別のIPアドレスを使用可能
  - 仮想マシンにもそれぞれIPアドレスが割り当てられる

### ネットワーク部とホスト部

- 同一ネットワークでは、IPアドレスの上位ビットが共通
- 例: 上位24ビットが192.168.1で共通、下位8ビットはホスト毎に割当て
- ネットワーク部を192.168.1.0/24（24はビット数）などと表記
- ホスト部の最大値（例：255）は、ブロードキャスト用に利用

## ホスト名とDNS

- ホスト名の例: www.konan-u.ac.jp
- FQDN (Fully Qualified Domain Name): 完全修飾ドメイン名
- DNS (Domain Name System): ホスト名とIPアドレスの対応づけを行う分散システム
  - 名前の登録・検索などを複数のサーバ群で担当
  - DNSサーバー: DNSの名前解決を行うサーバ

## ネットワーク設定

- DHCPサーバー: クライアントにネットワーク設定情報を提供
- 静的指定（固定）の例:
  - IPアドレス: 192.168.1.101
  - サブネットマスク: 255.255.255.0（ネットワーク部の幅を指定）
  - デフォルトゲートウェイ: 192.168.1.1（外に出ていくための出口、通常はルーターのIPアドレス）
  - DNSサーバー: 8.8.8.8（例）

## ポート番号

- 通信相手のアプリケーションを識別するための番号
- 16ビットの整数（0-65535）
- 代表的なアプリ・サービスのポート番号が決められている
  - 例: Webサーバー（HTTP）は80番ポートを使用

## 通信速度とデータ量の単位

- bps (bit per second): 1秒間に送れるビット数
- B/s (Bytes/s): 1秒間に送れるバイト数（1B/s = 8bps）
- データ量: B (Bytes)

## ネットワーク技術

### 有線LAN (Ethernet)

- LANケーブル: ツイストペアケーブル（UTPケーブル）、光ファイバーケーブル
- ネットワークスイッチ
- 通信規格例: 1000BASE-T（UTP、1000Mbps、最大100m）

### 無線LAN (Wi-Fi)

- IEEE 802.11で規格化
- 2.4GHz帯や5GHz帯を利用
- 規格例: IEEE 802.11n（Wi-Fi 4）、IEEE 802.11ac（Wi-Fi 5）、IEEE 802.11ax（Wi-Fi 6）
- アクセスポイント: 無線LAN端末（station）と通信
- SSID: アクセスポイントを識別
- 暗号化: WPAなど

### モバイルネットワーク

- LTE（3.9世代）: 最大150Mbps
- 5G: 
  - 通信の大容量化（Massive MIMO）
  - ヘテロジニアスネットワーク
  - 低遅延化（無線技術+エッジコンピューティング）

## ネットワーク通信方式

### 回線交換方式

- 始点から終点まで回線をつなぐ
- 接続要求に応じて通信路を準備し、回線を占有
- 特徴:
  - 他の通信と回線を共有できない
  - 接続後は回線は安定して利用可能

### パケット交換方式

- 送信情報をパケットに分割して送信
- パケット = ヘッダ + ペイロード
- 特徴:
  - 複数の通信で経路を共有可能
  - 他の通信の影響で通信速度が低下する可能性あり
- 蓄積交換方式（store and forward switching）とも呼ばれる

## ネットワークトポロジー

- Bus: 1本線にすべてがぶら下がり、全員が全情報を見れる
- Star: 交換機に端末がつながる
- Ring: 環状
- Tree: 循環がない。2点間の経路が一つに決まる
- Mesh: 循環あり。複数経路可能
- Hybrid: 複数の形状が混在

## 通信形態

- ユニキャスト: 単一の送信相手
- ブロードキャスト: 同じメッセージを全員に同時送信
- マルチキャスト: 決められた複数の相手に同時送信
- エニーキャスト: あるホストグループの内の一つ（例：一番近い相手）に送信

## CIDR (Classless Inter-Domain Routing)

- ネットワーク部を任意の長さに設定可能
- CIDR表記例: 192.168.1.0/24（ネットワーク部が24ビット）
- サブネットマスク: ネットワーク部を求めるためのビットマスク
  - 例: 255.255.255.0（ネットワーク部が24ビットの場合）

## 特殊なIPアドレス (IPv4)

- ブロードキャスト用: 例 192.168.1.0/24に対し192.168.1.255
- マルチキャスト用: 224.0.0.0/4 (224.0.0.0-239.255.255.255)
- localhost: 自分自身を指すアドレス 127.0.0.0/8
  - Loopback interface: 計算機が自分にアクセスするためのネットワークインタフェース

# DNS (Domain Name System)

## はじめに

### DNS とは?
- ドメイン名の管理をしている
- 例: www.konan-u.ac.jp から IP address への変換

### FQDN (Fully Qualified Domain Name)
- ホスト名、ドメイン名を省略せずに指定した記述形式
- ホスト名: www
- ドメイン名: jp, ac.jp, konan-u.ac.jp, www.konan-u.ac.jp

### 特徴
- 世界にまたがった分散システム

## DNS サーバの役割2種類

1. 端末からの要望に応えて名前引きを担当
   - 世界各地のホスト名を調査(代行)
   - 各クライアントが設定するのはこちら
   - キャッシュサーバなどと呼ばれる

2. 世界中のドメイン・ホスト名を分散して管理
   - 各ドメインごとにサーバ
   - 権威サーバ・コンテンツサーバと呼ばれる

両方の役割を兼務してもよい

### DNS サーバの役割
- 各種ホスト名・ドメイン名の登録
- 各ドメインを担当する権威サーバが存在

## 再帰的問い合わせ

- DNS サーバの役割 1 (キャッシュサーバ)
- 端末からの要望に応えて名前引きを担当
- 自分の管理ドメインは知っている
- 他のドメインは、以前の問い合わせ結果もしばらくキャッシュしている
- 知らない場合は、root から探索

## DNS とキャッシュ

### キャッシュサーバ
- 問い合わせ内容を保持

### セカンダリサーバ
- 権威サーバの情報をZone単位でキャッシュ

### キャッシュ指定
- serial: 最新情報のバージョン番号
- refresh: 3600秒たったら、新しい情報取得してね
- retry: 900秒, refresh できなかったら 900秒後再トライよろしく
- expire: refreshできないときも 604800秒たったら、捨ててね。
- minimum: 存在しなかった時も、1800秒はそのままだと思ってね

## DNS キャッシュの役割

- 内部利用者が多数いる場合、キャッシュにより外部への問い合わせ数を大幅に削減できる
- Cache: もともと貯蔵庫の意味。最近使ったデータを置いておくことで効率化。データ一貫性が議論にもなる。

## 各種 DNS レコード

- A, AAAA: FQDN から IP address へ(A: IPv4, AAAA: IPv6)
- MX: mail domain から mail server (FQDN)
- CNAME: ホストの別名を登録 (FQDN->FQDN)
- NS: ドメインに対する name server を登録
- SOA: ドメイン・Zoneに関する情報
- PTR: IP address から FQDN
- HTTPS: HTTPS のレコード (2023年11月から標準化)

## DNS と IP address

- IP address 空間と DNS 空間は1対1対応する必要なし
- 例:
  - www.abc.konan-u.ac.jp を学外サーバで運用することは可能
  - konan-u.ac.jp の mail domainは、学外サーバで運用可能
  - konan-u.ac.jp の DNS 権威サーバでサーバの IP address を指定

## DNS の階層構造

- Root は 13 clusters からなる (実機はもっと沢山, Anycast 利用)
- JP は JPRS (日本レジストリサービス) が管理
- jp, com などの NS は Top Level Domain (TLD) server と呼ばれる
- サブドメイン登録は、上部組織への申請が必要

## DNS と IP Anycast

- Root server の IP address は合計 13 個
- IP Anycast: 同じ IP address に複数ホスト割り付け、通信は最寄りのホストに routing をおこなう
- Public DNS server などでも利用 (例: 1.1.1.1, 8.8.8.8)

## DNS を用いた負荷分散

### Round-robin DNS
- 単一FQDNに対し、複数の IP address を持ち、先頭の IP address を順番に変えていく手法
- Client のアクセス先を振り分け

## DNS とセキュリティ

### 危険性
- DNS を使って偽サイトに誘導 (DNS cache poisoning)

### 対応
- DNSSEC: 権威 NS とキャッシュ server 間のやりとりを署名検証
- DNS over HTTPS: HTTPS 経由で DNS
- TLS + PKI によるサーバ認証

### DNS と Privacy
- 利用サイト情報の流出
- コンテンツフィルタへの応用

## Web Proxy Server

### 役割
- Web へのアクセスを中継する
- コンテンツをキャッシュして効率化
- コンテンツの監視・ブロック

### 透過型プロキシ
- HTTP アクセスを、ネットワーク的にプロキシに転送

### HTTPS, TLS との関係
- 暗号化した情報ならキャッシュは無意味
- Proxy が仲介するとサーバ認証で失敗

## CDN (Content Delivery Network)

- Web コンテンツなどを世界に配信するためのネットワーク
- 各地にデータ配信用キャッシュサーバ(エッジサーバ)を配置
- 従来は static data 中心だが、最近は関係データベースの分散配置なども

## DNS record: CNAME

- ホスト名の別名(alias)を定義するために利用
- サービス(www など)から担当マシンへの対応関係を定義する際に利用することが多い

## ネットワークプロトコル階層:
   - OSI参照モデル: 国際標準化機構(ISO)による7層モデル
   - Internet Protocol Suite (TCP/IP): インターネットで使用される4層モデル

## TCP/IPの各層:
   - アプリケーション層: HTTP, IMAP, SSLなど
   - トランスポート層: TCP, UDP
   - インターネット層: IP, IPsec
   - ネットワークインターフェース層: Ethernet, IEEE802.11

## プロトコル階層の機能:
   - アプリケーション層: ネットワーク上でアプリケーションを実現
   - トランスポート層: スタートからゴールの接続管理
   - インターネット層: スタートからゴールまで繋ぐ
   - ネットワークインターフェース層: 隣とつなぐ

## データ送信におけるカプセル化:
   - PCI (Protocol Control Information): 各層で付加される制御情報
   - SDU (Service Data Unit): 各層で運ぶペイロード
   - PDU (Protocol Data Unit): SDU + 制御情報

## データリンク層の機能:
   - フレーム化: データを分けて送る
   - メディアアクセス制御 (MAC): 通信タイミングの制御
   - 誤り制御: ノイズ除去や再送処理

## MACアドレス (物理アドレス):
   - ネットワークインターフェースに割り当てられた固有の識別子
   - Ethernetや IEEE 802.11では48ビット

## フレーム化の方式:
   - キャラクタ型: ASCII符号などの制御文字を使用
   - ビット志向型: 特定ビット列で判別
   - プリアンブル型: 物理層が信号で開始を判別

## メディアアクセス制御 (MAC) の方式:
   - 固定割当形: 時間帯、周波数帯、通信符号を事前に割り当て
   - 要求割当形: ポーリングやトークンパッシング
   - 競合形: ALOHA, CSMA/CD, CSMA/CA

## 誤り制御:
   - 前方誤り訂正 (FEC): 受信側で誤りを訂正
   - 自動再送要求 (ARQ): 送信側に再送を要求
     - Stop and Wait ARQ
     - Go-back-N ARQ
     - 選択的再送 ARQ

## ネットワーク技術の進化:
    - イーサネット: バス結合から木構造へ
    - 通信方式: 半二重通信から全二重通信へ

## 物理層の主要トピック:
   - 情報のディジタル化: 標本化・量子化
   - ディジタル情報の伝送: ベースバンド方式、ディジタル変調
   - 伝送路符号: 同期実現、直流成分抑制、必要帯域抑制
   - アナログ変調: AM, PM, FM
   - ディジタル変調: ASK, PSK, FSK, APSK, QAM, 適応変調
   - 多元接続: スペクトル拡散、CDMA

## 情報のディジタル化:
   - 標本化（サンプリング）: アナログデータを一定間隔で測定し離散データ化
   - 量子化: 信号の大きさを離散的な値で近似化

## ディジタル情報の伝送:
   - 伝送路符号: 物理信号による表現のための符号パターン
   - 変調/復調: 元の信号の振幅・周波数・位相を変化/復元

## ディジタル伝送方式:
   - ベースバンド方式: ディジタル情報をパルス波形として伝送（例：イーサネット）
   - ディジタル変調方式/ブロードバンド方式: ディジタル情報をアナログ波に変換して伝送（例：無線、光ファイバ）

## 伝送路符号:
   - ビット表現: Unipolar, Polar, Bipolar
   - 主な符号化方式: RZ, マンチェスター, AMI, 4B5B, 8b/10b

## アナログ変調:
   - AM (Amplitude Modulation): 振幅変調
   - PM (Phase Modulation): 位相変調
   - FM (Frequency Modulation): 周波数変調

## ディジタル変調:
   - 基本3方式: ASK, PSK, FSK
   - 組み合わせ方式: APSK, QAM
   - 適応変調: ノイズに応じて変調方式を変更

## 多元接続:
   - FDMA (Frequency Division Multiple Access): 周波数分割多元接続
   - TDMA (Time Division Multiple Access): 時分割多元接続
   - CDMA (Code Division Multiple Access): 符号分割多元接続

## メディアアクセス制御:
   - 固定割当形: 時間帯、周波数帯、通信符号を事前に割り当て
   - 要求割当形: ポーリング、トークンパッシング
   - 競合形: 各ノードが自律的にアクセス

## 多重化:
    - FDD (Frequency Division Duplex): 周波数分割複信
    - TDD (Time Division Duplex): 時分割複信
    - FDM (Frequency Division Multiplexing): 周波数分割多重
    - TDM (Time Division Multiplexing): 時分割多重
    - CDM (Code Division Multiplexing): 符号分割多重

## スペクトラム拡散:
    - 目的: ノイズ耐性向上、CDMA での利用
    - 手法: 周波数ホッピング、直接拡散（DS, Direct Sequence）
    - 直接拡散方式: PN信号（Pseudo Noise）を使用した拡散と復調

