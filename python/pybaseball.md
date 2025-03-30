
###  pybaseballとは？

**pybaseball** は、**Python** を使って **メジャーリーグベースボール（MLB）** に関するデータを簡単に取得できるライブラリです。特に、**Statcast、FanGraphs、Baseball Reference** などの主要な野球データソースから直接データを取得できるのが特徴です。

---

###  主な機能

- **Statcastデータの取得**
  - 選手の打撃、投球、守備に関する詳細なデータを日付・選手別に取得可能。
- **選手のキャリア成績**
  - 打者・投手のシーズン別成績や通算成績。
- **チーム成績や順位表**
- **歴代の試合スケジュールと結果**
- **WAR（Wins Above Replacement）などの高度な指標**

---

###  例：Statcastデータの取得

```python
from pybaseball import statcast

# 2023年4月1日から4月7日までの全試合データを取得
data = statcast(start_dt="2023-04-01", end_dt="2023-04-07")
print(data.head())
```

---

###  インストール方法

```bash
pip install pybaseball
```

---

###  補足

`pybaseball` は、取得したデータをPandasデータフレームとして扱えるため、分析や可視化にもとても便利です。野球データを使った機械学習やデータ分析にもよく利用されています。

