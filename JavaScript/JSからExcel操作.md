
### 1. **ブラウザ上でExcelファイルを操作**
- **[SheetJS (xlsx)](https://sheetjs.com/)**  
  - Excelファイル（`.xlsx`）を読み書きできるライブラリです。
  - ブラウザやNode.jsで使用可能。
  - **使用例:**
    ```javascript
    /* Excelファイルを読み込む */
    const fileInput = document.getElementById('fileInput');
    fileInput.addEventListener('change', (e) => {
      const file = e.target.files[0];
      const reader = new FileReader();
      reader.onload = (event) => {
        const data = new Uint8Array(event.target.result);
        const workbook = XLSX.read(data, { type: 'array' });
        const firstSheetName = workbook.SheetNames[0];
        const worksheet = workbook.Sheets[firstSheetName];
        const jsonData = XLSX.utils.sheet_to_json(worksheet, { header: 1 });
        console.log(jsonData);
      };
      reader.readAsArrayBuffer(file);
    });
    ```

---

### 2. **Excel Online (Office 365) を操作**
- **[Office JavaScript API (Office.js)](https://learn.microsoft.com/ja-jp/javascript/api/overview/excel?view=excel-js-1.5)**  
  - Microsoftの公式ライブラリで、Excel Onlineやデスクトップ版のExcelで動作します。
  - Excelアドインを作成して、より高度な操作が可能です。

  **例: Excelのセルにデータを書き込む:**
  ```javascript
  Excel.run(function (context) {
    const sheet = context.workbook.worksheets.getActiveWorksheet();
    sheet.getRange("A1").values = [["こんにちは、Excel!"]];
    return context.sync();
  }).catch(function (error) {
    console.log(error);
  });
  ```

---

### 3. **Node.jsでサーバーサイド操作**
- **exceljs** や **xlsx-populate** などのライブラリを使用して、Excelファイルを生成・編集できます。

**ExcelJSの使用例:**
```javascript
const ExcelJS = require('exceljs');

async function createExcel() {
  const workbook = new ExcelJS.Workbook();
  const sheet = workbook.addWorksheet('シート1');
  sheet.addRow(['名前', '年齢']);
  sheet.addRow(['太郎', 25]);
  await workbook.xlsx.writeFile('sample.xlsx');
  console.log('Excelファイルを作成しました。');
}

createExcel();
```

---

### どの方法を選ぶべき？
| **用途**              | **おすすめの方法**                |
|--------------------|------------------------------|
| WebアプリでExcelを読み書き | SheetJS (xlsx)               |
| Office 365のExcelを操作   | Office.js (Office JavaScript API) |
| Node.jsでExcelファイルを生成 | ExcelJSやxlsx-populate       |

