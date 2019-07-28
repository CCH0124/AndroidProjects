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

## stopWatch
- 預設情況，每一個 APP 都會在自己的程序裡執行
- 只有**主執行緒**可以更新使用者介面
- `Handler` 可以用來安排程式碼的執行時間，或將程式碼發送到不同的執行緒
- 改變裝置組態會導致 `activity` 被銷毀和重建
    - 畫面旋轉
- `activity` 會從 `Activity` 類別繼承生命週期方法
- `onSaveInstanceState(Bundle)` 在 `activity` 被銷毀之前保存它的狀態，可以在 `onCreate` 裡使用 `Bundle` 物件來回復狀態
    - bundle.put\*("name", value) 將值加入 `Bundle`
    - bundle.get\*("name") `Bundle` 取值
-  `onCreate` 負責 `activity` 生；`onDestroy` 負責 `activity` 死
- `onRestart`、`onStart` 和 `onStop` 負責 `activity` 顯示與否
- `onResume` 與 `onPause` 負責處裡 `activity` 被聚焦與失焦情況

##### 生命週期指南
|方法|呼叫時機|下一個方法|
|---|---|---|
|onCreate()|當 `activity` 第一次被建立時。使用此方法做一般靜態設定，項是建立視區等，它會給 `Bundle` 物件，包含先前保存的 activity 狀態。|onStart()|
|onRestart()|當 `activity` 已經停止，緊接著就要再次啟動時。|onStart()|
|onStart()|當 `activity` 正要顯示出來時。假如 `activity` 進入前景，這個方法結束之後會執行 `onResume()` 或者如果 `activity` 隱藏起來，隨後會執行 `onStop()`| onResume() Or onStop()|
|onResume()|當 `activity` 在前景時|onPause()|
|onPause()|當 `acticity` 因為其它的 `acticity` 恢復執行而不再處於前景時。下一個 `activity` 在這個方法結束之前都不會恢復，所以這個方法的程式碼必須盡快執行完畢。假如 `activity` 回到前景，這個方法結束後會執行 `onResume()`，或者如果它隱藏起來，會執行 `onStop()`| onResume() Or onStop()|
|onStop()|當 `activity` 隱藏起來時。原因可能是其他的 `activity` 完全遮蓋它，或因為這個 `activity` 被銷毀。如果 `activity` 再度顯示，這個方法結束後會執行 `onRestart()`；如果 `activity` 即將被銷毀，後面就接著 `onDestroy()`|onRestart() Or onDestroy()|
|onDestroy()|當 `activity` 即將被銷毀時，或著因為 `activity` 結束了|none|

![](https://i.imgur.com/FPXTs7H.png)

##### Example

1. 使用者啟動 `activity`，並開始使用它。
onCreate -> onStart -> onResume
2. 使用者啟動 `activity`，開始使用它，然後切換到其它 APP
onCreate -> onStart -> onResume > onPause -> onStop
3. 使用者啟動 `activity`，開始使用它，接著旋轉裝置，在切換到其它 APP，然後回到我們的 `activity`
onCreate -> onStart -> onResume > onPause -> onStop > onDestroy -> onCreate -> onStart -> onResume -> onPause -> onStop -> onRestart -> onStart -> onResume


## Duck 
### View 的介紹
- 所有 GUI 元件都是 `android.view.View` 類別的子類別
- 所有版面都是 `android.view.ViewGroup` 類別的子類別，`ViewGroup` 是一個能夠容納多個 `View` 的 `View`
- 版面 XML 檔會被轉換樹狀結構的 `ViewGroup`
- `LinearLayout` 版面可用 `orientation` 指定直向或橫向
- `FrameLayout` 會將 `View` 堆疊起來
- 可使用 `android:padding*` 指定周圍邊距
![](https://thinhme.files.wordpress.com/2015/10/padding_margin.png?w=445&h=279)
- `android:weight`，在使用 `LinearLayout` 希望 `View` 元件使用剩餘版面的空間
![](https://thinhme.files.wordpress.com/2015/10/layout_weight1.png?w=525&h=334)
- `android:layout_gravity` 可指定 `View` 在其可用空間中的位置
- `android:gravity` 用來指定 `View` 元件內容在 `View` 裡面的位置
![](https://thinhme.files.wordpress.com/2015/10/gravity1.png?w=531&h=351)
- `<ToogleButton>` 定義開關狀態
- `<Switch>` 可用來定義開關
- `<ScrollView>` 或 `<HorizontalScrollView>` 添加卷軸

[Ref](https://thinhme.wordpress.com/2015/10/24/lesson-6layout-in-android/)

## MyConstraintLayout
- 約束版面是為了搭配 Android Studio 的設計編輯器一起使用而設計的
- 要夠過加入約束來定位 `View`。每一個 `View` 都需要一個橫向或直向的約束
- 將 `View` 置中，必須為 `View` 的對邊加上約束，並更改 `View` 偏移值，來改變他在兩個約束之間的位置
- 如果 `View` 對邊有約束，你可以更改 `View` 的尺寸，讓它符合上限
- 你可以設定 `View` 尺寸的長寬比
- 按下 `Infer Constraints` 按鈕後，Android Studio 會根據 `View` 在藍圖上的位置來加入約束

## Starbuzz
- 將腦中點子分成`頂層 activity`、`分類 activity`、`詳情/編輯 activity`
    - 分類用途是從頂層 `activity` 巡覽到詳情/編輯 `activity`
- `list View`（ListView） 會在一個清單裡顯示項目
    - 用 `ListView` 元素加入至版面設定
- 可以在版面裡面使用 `android:entries`，用在 `string.xml` 裡面設定的陣列幫 `ListView` 填入項目
- 配接器扮演 `AdapterView` 與資料來源之間的橋樑
    - `ListView` 和 `Spinners` 都屬於 `AdapterView` 型態
- `ArrayAdapter` 是搭配陣列一起使用的配接器
- 處裡 `Button` 的按下事件，要在版面設定中使用 `android:onClick`
    - 要在其他地方處裡按下事件，要建立監聽器（AdapterView.OnItemClickListener）並實作案下的動作