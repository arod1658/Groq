# Streamlit × Groq API 聊天機器人

這是一個使用 **Streamlit** 建立的網頁聊天介面，透過 **Groq API** 呼叫大型語言模型並回覆訊息。

> **模型說明：** 程式目前設定為 `openai/gpt-oss-120b`，並非 Llama 模型；原程式中的「Llama」僅是註解與函式命名。

## 功能

- 使用 Streamlit 在瀏覽器中輸入訊息、顯示 AI 回覆。
- 使用 `st.session_state` 保留目前瀏覽器工作階段的聊天紀錄。
- 每次發問時將目前工作階段的完整對話傳送至 Groq API，以延續對話脈絡。
- 點擊「新聊天」按鈕清空聊天紀錄。
- 呼叫 API 失敗時顯示錯誤資訊。

## 專案結構

```text
.
├── ch16-2-3.py        # Streamlit 應用程式
├── requirements.txt   # Python 相依套件
└── README.md          # 專案說明文件
```

## 執行環境

建議使用 Python 3.10 以上版本，並準備可使用的 Groq API Key。

## 安裝步驟

1. 開啟終端機並進入專案資料夾。
2. 安裝相依套件：

   ```bash
   python -m pip install -r requirements.txt
   ```

3. 前往 [Groq Console](https://console.groq.com/keys) 取得自己的 API Key。
4. 設定 `GROQ_API_KEY` 環境變數（請選擇你的終端機對應方式）：

   **Windows PowerShell（只對目前視窗有效）：**

   ```powershell
   $env:GROQ_API_KEY = "你的_Groq_API_Key"
   ```

   **Windows 命令提示字元 CMD（只對目前視窗有效）：**

   ```cmd
   set GROQ_API_KEY=你的_Groq_API_Key
   ```

   **macOS / Linux：**

   ```bash
   export GROQ_API_KEY="你的_Groq_API_Key"
   ```

   若使用 Windows 系統設定新增**永久**環境變數，須重開終端機、VS Code 或 Jupyter Kernel，讓新程序讀取到該變數。

5. 啟動應用程式：

   ```bash
   python -m streamlit run ch16-2-3.py
   ```

6. 依照終端機提示開啟網址，通常是 `http://localhost:8501`。

## 如何使用

1. 在底部「請輸入您的訊息」欄位輸入問題。
2. 送出後，程式呼叫 Groq API 產生回覆。
3. 繼續輸入問題即可在同一個工作階段延續對話。
4. 若要重新開始，點擊「新聊天」。

## 模型與 API 參數

目前程式 `ch16-2-3.py` 的主要設定如下：

| 參數 | 值 | 說明 |
| --- | --- | --- |
| `model` | `openai/gpt-oss-120b` | 使用的模型名稱 |
| `temperature` | `0` | 降低回覆的隨機性 |
| `max_completion_tokens` | `1024` | 回覆的最大 token 數 |
| `top_p` | `0.5` | 核取樣參數 |
| `stream` | `False` | 等待回覆完成後一次顯示 |

模型的實際可用性依 Groq 平台與帳戶權限而定。

## 部署到 Streamlit Community Cloud（選用）

1. 將 `ch16-2-3.py`、`requirements.txt` 與 `README.md` 上傳至 GitHub 儲存庫。
2. 透過 [Streamlit Community Cloud](https://share.streamlit.io/) 建立 App，主程式選擇 `ch16-2-3.py`。
3. 在 App 的 **Secrets** 中加入：

   ```toml
   GROQ_API_KEY = "你的_Groq_API_Key"
   ```

4. 儲存設定並部署。Groq Python SDK 可讀取 `GROQ_API_KEY` 環境變數；部署平台的 Secrets 會提供給應用程式。

**安全提醒：** 不要將 API Key 寫入 Python 程式、README 或推送到 GitHub。公開部署時請留意 Groq API 使用額度及費用。

## 常見問題

**出現 `The api_key client option must be set`**  
請確認 `GROQ_API_KEY` 已設定，並在設定永久環境變數後重新開啟終端機／執行環境。

**出現 `ModuleNotFoundError`**  
確認已於正確的 Python 環境執行 `python -m pip install -r requirements.txt`。

**模型名稱無效或無法使用**  
請到 Groq 官方控制台檢查目前帳戶可用的模型，必要時修改 `model` 參數。

## 使用技術

- Python
- Streamlit
- Groq Python SDK
- GPT-OSS 120B（透過 Groq API）
# Groq
