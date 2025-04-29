`benchmark.rb` は Ruby の標準ライブラリに含まれている **パフォーマンス測定ツール** です。  
主に、**処理にかかる時間を測定するため**に使われます。

---

## 基本の使い方（Benchmark#measure）

```ruby
require 'benchmark'

time = Benchmark.measure do
  sum = 0
  1.upto(1000000) { |i| sum += i }
end

puts time
```

### 出力例

```
  0.020000   0.000000   0.020000 (  0.019876)
```

| 項目         | 意味                                 |
|--------------|--------------------------------------|
| user         | ユーザCPU時間（ユーザ処理に使ったCPU） |
| system       | システムCPU時間（OS処理に使ったCPU）   |
| total        | 合計CPU時間（user + system）         |
| real         | 実時間（実際にかかった「経過時間」）     |

> 一般的に「real（実時間）」を見て、どれくらい時間がかかったか確認します。

---

## 複数処理を比較する（Benchmark#bm）

```ruby
require 'benchmark'

Benchmark.bm do |x|
  x.report("each:") do
    (1..1000000).each { |i| i * 2 }
  end

  x.report("map:") do
    (1..1000000).map { |i| i * 2 }
  end
end
```

### 出力例

```
             user     system      total        real
each:     0.050000   0.000000   0.050000 (  0.049812)
map:      0.100000   0.000000   0.100000 (  0.101234)
```

→ `each` の方が速いことが分かります。

---

## 精度の高い比較（Benchmark#bmbm）

`bm` はキャッシュなどの影響を受けることがあります。  
それを避けて正確に測るには、`bmbm` を使います。

```ruby
require 'benchmark'

Benchmark.bmbm do |x|
  x.report("each:") do
    (1..1000000).each { |i| i * 2 }
  end

  x.report("map:") do
    (1..1000000).map { |i| i * 2 }
  end
end
```

### 出力例（2回測定される）

```
Rehearsal -----------------------------------------
each:     0.050000   0.000000   0.050000 (  0.049812)
map:      0.100000   0.000000   0.100000 (  0.101234)
-------------------------------- total: 0.150000sec

              user     system      total        real
each:     0.050000   0.000000   0.050000 (  0.048234)
map:      0.100000   0.000000   0.100000 (  0.102456)
```

---

## 測定結果を変数で使いたいとき

```ruby
require 'benchmark'

result = Benchmark.measure do
  sleep(1)
end

puts "かかった時間: #{result.real} 秒"
```

---

## 使いどころ

- 複数のアルゴリズムの性能比較
- 処理高速化の前後比較
- 「体感では速くなった気がする」が本当に正しいかチェック

---

## 補足：requireの場所

標準ライブラリにあるので、Gemのインストールは不要です。
```ruby
require 'benchmark'
```
