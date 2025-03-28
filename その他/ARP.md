### **ARP（Address Resolution Protocol）とは？**
ARP（Address Resolution Protocol）は、IPアドレスからMACアドレスを取得するためのプロトコルです。TCP/IPネットワークにおいて、通信を行う際に必須となる技術です。

---

## **1. なぜARPが必要なのか？**
ネットワークで通信を行う場合、デバイスはIPアドレスを使って相手を特定します。しかし、実際のデータ転送はイーサネットやWi-Fiといったレイヤー2（データリンク層）で行われるため、MACアドレスが必要になります。

例えば、PCがルーターにデータを送る場合：
1. PCはルーターのIPアドレス（例：192.168.1.1）を知っている。
2. しかし、MACアドレスが分からないと通信できない。
3. そこで、PCはARPを使ってルーターのMACアドレスを取得する。

---

## **2. ARPの仕組み**
### **(1) ARPリクエスト**
IPアドレスからMACアドレスを知りたい場合、送信元デバイスは「ARPリクエスト」をブロードキャスト（全デバイス宛）で送ります。

#### **ARPリクエストのフォーマット**
| フィールド | 説明 |
|-----------|------|
| 送信元MACアドレス | 自分のMACアドレス |
| 送信元IPアドレス | 自分のIPアドレス |
| 宛先MACアドレス | 不明（空欄） |
| 宛先IPアドレス | 調べたいIPアドレス |

**例**
> 「192.168.1.1（ルーター）を持つデバイスは誰ですか？MACアドレスを教えてください！」

このリクエストは同じネットワーク内の全デバイスに送られます（ブロードキャスト: `FF:FF:FF:FF:FF:FF`）。

---

### **(2) ARPリプライ**
対象のIPアドレスを持つデバイス（ルーターなど）は、自分のMACアドレスを含めた「ARPリプライ」を送信元にユニキャスト（直接）で返信します。

#### **ARPリプライのフォーマット**
| フィールド | 説明 |
|-----------|------|
| 送信元MACアドレス | 自分のMACアドレス |
| 送信元IPアドレス | 自分のIPアドレス |
| 宛先MACアドレス | リクエストを送ったデバイスのMACアドレス |
| 宛先IPアドレス | リクエストを送ったデバイスのIPアドレス |

**例**
> 「192.168.1.1を持っているのは私です！MACアドレスは `AA:BB:CC:DD:EE:FF` です！」

---

### **(3) ARPキャッシュ**
頻繁にARPリクエストを送るのは非効率なので、デバイスはMACアドレスを一時的に保存する「ARPキャッシュ」を持っています。

- **キャッシュの有効期限**: 数分～数十分で削除される
- **キャッシュの確認（Windowsの場合）**
  ```
  arp -a
  ```
- **キャッシュの削除**
  ```
  arp -d
  ```

---

## **3. ARPの種類**
### **(1) 通常のARP**
上記のようにIPアドレスからMACアドレスを取得するための標準的なARP。

### **(2) Gratuitous ARP（無償ARP）**
自分自身のIPアドレスに対して「自分のMACアドレス」を通知する特殊なARP。
- **目的**
  - IPアドレスの重複を検出
  - ネットワークの変更を通知
  - 新しいデバイスがネットワークに追加されたことを通知

**例**
> 「私は192.168.1.100で、MACアドレスは `11:22:33:44:55:66` です！」

### **(3) Reverse ARP（RARP）**
MACアドレスからIPアドレスを取得するプロトコル（現在はDHCPに置き換えられた）。

---

## **4. ARPのセキュリティリスク**
### **(1) ARPスプーフィング（偽装）**
悪意のあるデバイスが偽のARPリプライを送り、通信を傍受したり、なりすましを行う攻撃。

**攻撃例**
1. PCが「192.168.1.1（ルーター）のMACアドレスは？」とARPリクエストを送信。
2. 攻撃者が偽のARPリプライを返し、「192.168.1.1は `XX:XX:XX:XX:XX:XX`（攻撃者のMAC）」と騙す。
3. PCは攻撃者をルーターだと誤認し、すべての通信が攻撃者を経由する。

**対策**
- **静的ARPエントリー**（固定登録）
  ```
  arp -s 192.168.1.1 AA:BB:CC:DD:EE:FF
  ```
- **ARPスプーフィング検出ツールの使用**
- **VPNやHTTPSでデータを暗号化**

---

## **5. まとめ**
| 項目 | 内容 |
|------|------|
| **ARPとは？** | IPアドレスからMACアドレスを取得するプロトコル |
| **役割** | ネットワーク通信のために必要なMACアドレスを取得 |
| **基本動作** | ARPリクエスト（ブロードキャスト）→ ARPリプライ（ユニキャスト） |
| **ARPキャッシュ** | MACアドレスを一時保存して効率化 |
| **種類** | 通常のARP、Gratuitous ARP、RARP |
| **リスク** | ARPスプーフィング（偽装攻撃） |
| **対策** | 静的ARP登録、スプーフィング検出、暗号化通信 |

