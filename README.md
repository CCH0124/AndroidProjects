# AndroidProjects

## BeerAdviser
- `<Button>` 元素表示按鈕
    - 按鈕動作在 layout 中加入 `android:onClick="cliclMethod"`，在 Activity 中必須加入相對應的方法
- `Spinner` 元素表示下拉式選單
    - `getSelectedItem()` 取得 spinner 中的選項項目。
- 所有 `GUI` 元件型態都是 `View`，都繼承 `View` 類別
- `string.xml` 字串資源檔。將文字值與 layout 和 Activity 分隔開來，與支援當地語系
    - 加入陣列方式
    ```
    <string-array name="array">
        <item>Value</item>
    </string-array>
    ```
- `R.java` 是自動生成的。可用來取得 layout、GUI 元件、字串與其它 java 程式碼的參考

## MyMessenger
- 聯合兩個以上 `activity` 稱為 `task`
- `intent` 是 `Android` 元件用來相互溝通訊息
    - 會明確指定目標元件 `Intent intent = new Intent(this, Tarfet.class)`
    - `putExtra()`，在 Intent 新增額外資訊
    - `getIntent()` 取得啟動這個 `activity` 的 `intent`
    - activity action 功能是描述 `activity` 努執行的標準動作，如：傳送訊息，就使用 `Intent.ACTION_SEND`
    - 建立指定 `action` 的默認 `intent，使用` `Intent intent = new Intent(action)`
    - 描述 `intent` 理資料類型，就使用 `setType()`
- 啟動 `Activity` 的方式是呼叫 `startActivity(intent)`，找不到則會噴出例外
- Android 會根據 `intent` 指定的具名元件、action、資料型態，以及 `category` 來解析 `intent`，他會拿 `intent` 的內容與每一個 app 的 *AndroidManifest.xml* 裡的各個 `intent` `過濾器做比較。activity` 必須具有 `DEFAULT` 的 `category`，才能夠接受默認 `intent`
- `createChooser()` 可覆寫預設的 Android `activity` 選單對話框。
    - 如過沒有 `activity` 能夠接收 `intent`，會顯示訊息讓使用者知道
    - 回傳一個 `intent`
- `getString(R.string.stringname)` 取得字串資源值