###  **SheetJSとは？**
**SheetJS**（正式名：**xlsx**ライブラリ）は、**JavaScript**を使って**Excelファイル（.xlsxや.xls）を読み書きできるオープンソースのライブラリ**です。ブラウザやNode.js環境で動作し、**Excelファイルの解析、生成、変換**などを簡単に行うことができます。

---

###  **SheetJSの主な機能**
1. **Excelファイルの読み込みと解析**（.xlsx, .xls, .csv, .ods など）
2. **Excelファイルの生成とエクスポート**（ブラウザから直接ダウンロード可能）
3. **JSON、CSV、HTMLなどのフォーマットへの変換**
4. **複数シートの操作**
5. **データの編集やセルスタイルの設定**（Proバージョンでは高度な機能も提供）

---

###  **なぜSheetJSを使うのか？**
-  **軽量かつ高速**なパフォーマンス  
-  **ブラウザとNode.jsの両方で動作**  
-  **複数のデータフォーマットをサポート**（CSV、JSON、HTML、TXTなど）  
-  **外部ライブラリ不要**でファイル操作が可能  
-  **カスタマイズ性が高い**（プロ版でさらに多機能に）  

---

###  **SheetJSの使い方（基本的な実装例）**

#### 1️ **Excelファイルの読み込み（ブラウザの場合）**

```html
<input type="file" id="uploadExcel" />
<script src="https://cdn.jsdelivr.net/npm/xlsx/dist/xlsx.full.min.js"></script>
<script>
    document.getElementById('uploadExcel').addEventListener('change', function(e) {
        const file = e.target.files[0];
        const reader = new FileReader();

        reader.onload = function(event) {
            const data = new Uint8Array(event.target.result);
            const workbook = XLSX.read(data, { type: 'array' });

            //  最初のシートを取得
            const sheetName = workbook.SheetNames[0];
            const worksheet = workbook.Sheets[sheetName];

            //  ExcelデータをJSONに変換
            const jsonData = XLSX.utils.sheet_to_json(worksheet);
            console.log(jsonData);
        };
        reader.readAsArrayBuffer(file);
    });
</script>
```

---

#### 2️ **データをExcelファイルとしてエクスポート（ダウンロード）**

```html
<button id="downloadExcel">Excelをダウンロード</button>
<script>
    document.getElementById('downloadExcel').addEventListener('click', function() {
        const data = [
            { 名前: "山田太郎", 年齢: 28, 職業: "エンジニア" },
            { 名前: "鈴木花子", 年齢: 32, 職業: "デザイナー" }
        ];

        //  JSONデータをワークシートに変換
        const worksheet = XLSX.utils.json_to_sheet(data);

        //  新しいワークブックを作成
        const workbook = XLSX.utils.book_new();
        XLSX.utils.book_append_sheet(workbook, worksheet, "社員情報");

        //  Excelファイルとして書き出し
        XLSX.writeFile(workbook, "社員データ.xlsx");
    });
</script>
```

---

###  **主要なAPI/関数の説明**

| 関数                         | 説明                                       |
|------------------------------|--------------------------------------------|
| `XLSX.read(data, opts)`      | Excelファイルを解析してワークブックを生成   |
| `XLSX.utils.sheet_to_json()` | シートデータをJSON形式に変換               |
| `XLSX.utils.json_to_sheet()` | JSONデータをシートに変換                   |
| `XLSX.utils.book_new()`      | 新しいワークブックを作成                   |
| `XLSX.utils.book_append_sheet(workbook, worksheet, sheetName)` | ワークブックにシートを追加 |
| `XLSX.writeFile(workbook, filename)` | Excelファイルとして保存                   |

---

###  **応用的な使い方**
-  **複数シートの操作**: 複数のシートを扱うExcelファイルを生成  
-  **セルの書式設定や数式追加**（Pro版で対応）  
-  **Node.js環境でサーバーサイド処理**  
-  **バイナリデータやパスワード保護されたファイルの処理**

---

###  **SheetJSを使うメリットまとめ**
-  **ファイルをサーバーに送信せずにブラウザ上で処理可能**（セキュア）
-  **他のライブラリと組み合わせて高機能なアプリを構築可能**（例: PQGrid、React、Vue.jsなど）
-  **エクセルデータを扱うあらゆるアプリケーションに組み込みやすい**
