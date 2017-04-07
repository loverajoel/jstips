# 如何提交你的 tip

如果要提交 tip 到目錄，fork 這個儲存庫（repository）並加入你的 tip 到檔案內，放入到正確的資料夾（根據語系）。檔案名稱應該為 `2016-xx-xx-name-of-your-tip`。

當你撰寫你的 tip 時，請使用[這個格式](POST_TEMPLATE.md)。

### 要求

- tip 應該至少可以在兩分鐘內讀懂。
- 你可以連結到其他的網站或者是影片讓我們了解更多。
- 程式碼區塊使用 ```js。
- 避免在 title 提到「JavaScript」（因為我們的 tips 都是與 JavaScript 相關的）。
- 使用反引號（`）來標記程式碼 - _警告_：tip **標題**和 **tip-tldr** 不要使用反引號。


當你的 tip 準備好了，依據這個 [PR 樣板](PULL_REQUEST_TEMPLATE.md)，[發送一個 PR](https://help.github.com/articles/using-pull-requests/) 你的 tip 將會被校閱。每天都會有 tip 從可用的 PR 中被合併（merged）。

## 注意

使用 **xx** 為日期和 tip 的編號。當我們決定合併你的 PR 你可以把它們增加並 [squash](https://davidwalsh.name/squash-commits-git) 到你的 commits。

## Tip 工作流程

**Tip 發送** ⇒ **Tip 審查** ⇒ **Tip 接受並發布**

- 當你提交 tip 時，如果 tip 正在校閱流程，則 tip 狀態為 `under-review`。
- 如果 tip 經過 5 位專業的人士校閱，而且他們都給了 :shipit:，tip 將會被合併（`merge`）到 tip 清單。
