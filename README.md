# Streamlit + Groq API 聊天機器人

使用 Python、Streamlit 與 Groq API 建立的簡易 AI 聊天網頁應用程式。使用者可以在網頁中輸入訊息，取得 AI 回覆，並在同一個對話中保留聊天紀錄。

## 專案功能

- **網頁聊天介面**：使用 Streamlit 的聊天元件輸入訊息及顯示回覆。
- **Groq API 串接**：透過 Groq API 呼叫指定的語言模型。
- **保留對話紀錄**：使用 `st.session_state` 暫存目前工作階段的對話內容，並將對話紀錄一併傳送給模型。
- **建立新聊天**：點擊「新聊天」按鈕即可清空目前的聊天紀錄。
- **錯誤處理**：發生 API 呼叫錯誤時，顯示錯誤訊息。

## 使用技術

- Python
- Streamlit
- Groq Python SDK
- Groq API 上可用的語言模型（目前程式設定為 `openai/gpt-oss-120b`）

## 專案結構

```text
.
├── groq_chat.py       # Streamlit 聊天應用程式
├── requirements.txt   # Python 套件清單（需自行建立，範例如下）
└── README.md          # 專案說明文件
```

## 環境需求

- 已安裝 Python（建議使用 Python 3.10 或更新版本）
- 可使用的 Groq API Key
- 可連上網際網路

## 安裝與設定

### 1. 下載專案

```bash
git clone <你的 GitHub Repository URL>
cd <你的專案資料夾>
```

也可以直接下載此 GitHub Repository 的 ZIP 檔並解壓縮。

### 2. 建立虛擬環境（建議）

Windows：

```bash
python -m venv .venv
.venv\Scripts\activate
```

macOS / Linux：

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. 安裝套件

建立 `requirements.txt`，內容如下：

```text
streamlit
groq
```

接著執行：

```bash
pip install -r requirements.txt
```

### 4. 設定 Groq API Key

請先至 [Groq Console](https://console.groq.com/) 取得 API Key。

建議使用環境變數設定金鑰，**不要將 API Key 直接寫進程式碼，也不要上傳到 GitHub**。

Windows PowerShell：

```powershell
$env:GROQ_API_KEY="你的 Groq API Key"
```

macOS / Linux：

```bash
export GROQ_API_KEY="你的 Groq API Key"
```

Groq Python SDK 通常會自動讀取 `GROQ_API_KEY` 環境變數，程式中的 `Groq()` 可使用此設定建立客戶端。

## 執行程式

在專案資料夾中執行：

```bash
streamlit run groq_chat.py
```

啟動後，依照終端機顯示的網址開啟網頁（通常是 `http://localhost:8501`），即可開始聊天。

## 使用方式

1. 在網頁底部的輸入框輸入訊息。
2. 按下 Enter，等待 AI 回覆。
3. 後續訊息會連同目前工作階段的聊天紀錄一起傳送給模型，以提供對話上下文。
4. 點擊「新聊天」即可清空目前顯示的對話紀錄，開始新的對話。

## 模型設定

目前程式指定的模型為：

```python
model="openai/gpt-oss-120b"
```

若要使用其他模型，請先確認該模型目前可透過 Groq API 使用，再修改 `groq_chat.py` 中的 `model` 設定。

## 注意事項

- **API Key 安全**：不要將金鑰提交到公開 Repository。若金鑰曾經意外公開，請立即至 Groq Console 撤銷或重新產生。
- **對話紀錄範圍**：目前聊天紀錄儲存在 Streamlit 的工作階段狀態中，不是永久資料庫；重新開始工作階段後，紀錄可能不再保留。
- **新聊天功能**：此功能會清除目前工作階段的對話紀錄，不會刪除外部資料庫中的資料。
- **模型可用性**：模型名稱、API 配額與服務可用性可能變動；若呼叫失敗，請確認模型名稱、API Key、網路連線及帳戶配額。
- **Token 與費用**：每次請求會傳送目前工作階段的完整聊天紀錄，對話越長，使用的 Token 可能越多。

## 未來可擴充方向

- 支援串流輸出，逐步顯示 AI 回覆。
- 加入系統提示詞，調整 AI 的回答風格。
- 支援匯出或儲存聊天紀錄。
- 增加模型選擇與參數設定。
- 改善錯誤訊息及載入狀態的呈現。

## License

目前尚未指定授權條款。如需讓其他人依特定條件使用、修改或散布本專案，請在 Repository 中新增適合的 `LICENSE` 檔案。
