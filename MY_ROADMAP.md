# 我的 AI 學習路線（概念閱讀版）

> 目標：理解底層概念，更合理、高效地使用 AI
> 讀法：每課讀 `docs/en.md` 的 **The Problem** 與 **The Concept**，Build It 的程式先跳過，數學公式看懂直覺就好
> 每課路徑：`phases/<phase>/<lesson>/docs/en.md`；時間為課程標示的預估值，只讀概念約 30–40 分鐘
> 核心 54 課，約 33–40 小時；每週 5 小時約 2 個月

---

## ① 機器怎麼「學習」（8 課）

> 重點：模型 = 一堆數字（權重）；訓練 = 不斷調整權重讓損失變小
> 對使用 AI 的幫助：理解 AI 是從資料學到統計規律，不是真的「懂」

- [ ] **02/01 什麼是機器學習**（~45 分）
  - 監督式、非監督式、強化學習的差別
  - 分類 vs 回歸
  - 判斷一個商業問題該用 ML 還是寫規則就好
- [ ] **02/02 線性回歸**（~90 分）
  - ML 的 Hello World：找一條最貼近資料的直線
  - 梯度下降的直覺：沿著讓誤差變小的方向一步步調整
  - Ridge 正則化防止過擬合
- [ ] **02/10 偏差與變異的取捨**（~75 分）
  - 誤差 = 偏差 + 變異 + 雜訊
  - 欠擬合 vs 過擬合，從訓練 / 測試誤差判斷
  - L1、L2、dropout、early stopping 怎麼調整取捨
- [ ] **03/01 感知器**（~60 分）
  - 神經網路的最小單位：權重、偏差、決策
  - 單一感知器解不了 XOR，疊多層才能解
- [ ] **03/02 多層網路與前向傳播**（~90 分）
  - 資料一層一層往前算出結果
  - 非線性激活讓網路能畫出曲線邊界
- [ ] **03/03 反向傳播** ⭐（~120 分）
  - 神經網路能學習的關鍵：從誤差往回推每個權重該怎麼調
  - 連鎖律、計算圖的直覺
  - 梯度消失問題
- [ ] **03/05 損失函數**（~75 分）
  - 損失 = 模型錯得有多離譜；選錯損失，模型就會優化錯目標
  - MSE、交叉熵、對比學習損失（InfoNCE）
- [ ] **03/06 優化器**（~75 分）
  - 梯度告訴你方向，優化器決定走多遠多快
  - SGD、Momentum、Adam、AdamW

## ② 文字怎麼變成數字（3 課）

> 重點：token 與 embedding（語意向量）
> 對使用 AI 的幫助：為什麼中文較耗 token、為什麼 AI 數不清字母、為什麼語意搜尋比關鍵字強

- [ ] **10/01 Tokenizer：BPE、WordPiece、SentencePiece**（~90 分）
  - LLM 讀的是整數，不是文字
  - 字典大小的取捨；不同語言與程式碼的切詞問題
- [ ] **11/04 Embeddings 與向量表示**（~75 分）
  - 把文字變成向量，用 cosine similarity 比較語意
  - 為什麼語意搜尋能解決「用詞不同但意思相同」的問題
- [ ] **05/22 Embedding Models 深入**（~60 分）
  - 現代 embedding 模型：一段文字一個向量、跨語言、dense / sparse / multi-vector
  - 選錯 embedding 模型會讓 RAG 撈到錯的內容

## ③ Transformer：LLM 的大腦（5 課）

> 重點：attention（每個字判斷哪些字跟自己有關）；GPT 只是在預測下一個字
> 對使用 AI 的幫助：幻覺的本質是產生「看起來合理的下一個字」而非查資料；context 的位置與內容會影響結果

- [ ] **07/01 為什麼需要 Transformer**（~45 分）
  - RNN 一次處理一個 token；Transformer 一次處理全部，這是 2017 年後一切規模化的基礎
- [ ] **07/02 Self-Attention** ⭐（~90 分）
  - 每個詞問「誰對我重要？」：Query / Key / Value
  - Causal mask：讓模型只能看前面的字
- [ ] **07/03 Multi-Head Attention**（~75 分）
  - 一個 head 學一種關係，多個 head 同時學多種
- [ ] **07/04 位置編碼**（~45 分）
  - Attention 本身不知道詞的順序
  - 三種解法：Sinusoidal、RoPE、ALiBi
- [ ] **07/07 GPT：因果語言模型**（~75 分）
  - BERT 看兩邊、GPT 只看前面
  - 三角形 mask 是現代 AI 最關鍵的一行程式

## ④ LLM 怎麼煉成 ChatGPT（4 課）

> 重點：預訓練 → 指令微調（SFT）→ 人類偏好訓練（RLHF）
> 對使用 AI 的幫助：AI 為什麼會討好、附和你；temperature 在調什麼；benchmark 分數為什麼不可全信

- [ ] **10/04 預訓練一個 mini GPT**（~120 分）
  - GPT-2 架構：embedding、transformer 層、輸出層
  - 用「預測下一個字」訓練
  - 生成時的 temperature、top-k / top-p 取樣
- [ ] **10/06 指令微調（SFT）**（~90 分）
  - 基礎模型只會接話，SFT 讓它變成會回答問題的助理
  - Chat template 格式（system / user / assistant）
- [ ] **10/07 RLHF：獎勵模型 + PPO**（~90 分）
  - 用人類偏好（A 比 B 好）訓練獎勵模型
  - 再用強化學習優化模型，KL 懲罰防止模型鑽漏洞
- [ ] **10/10 評估：Benchmark 與 Eval**（~90 分）
  - Goodhart 定律：指標變成目標就失效
  - 真正重要的是在「你的任務、你的資料」上評估

## ⑤ 推論與限制（3 課）

> 重點：KV cache、量化、輸出為什麼是一個字一個字跑出來
> 對使用 AI 的幫助：context 越長越貴越慢；固定前綴能被快取（prompt caching）；本機小模型為什麼較笨

- [ ] **07/12 KV Cache 與 Flash Attention**（~75 分）
  - 訓練受運算量限制、推論受記憶體限制
  - KV cache 避免重複計算
- [ ] **10/11 量化**（~120 分）
  - 70B 模型 FP16 要 140GB，INT4 一台 MacBook 就跑得動
  - 精度與品質的取捨
- [ ] **10/12 推論優化**（~120 分）
  - Prefill（一次讀完 prompt）vs Decode（一個字一個字產生）
  - Continuous batching、PagedAttention、speculative decoding

## ⑥ 怎麼跟 AI 溝通（5 課）

> 重點：prompt 寫法、推理引導、context engineering、結構化輸出、安全
> 對使用 AI 的幫助：最直接提升日常使用效率的一段

- [ ] **11/01 Prompt Engineering**（~90 分）
  - 核心模式：角色、上下文、限制、輸出格式
  - 寫有明確行為規則的 system prompt
  - 診斷並修正幻覺、拒答、格式錯誤
- [ ] **11/02 Few-shot、Chain-of-Thought、Tree-of-Thought**（~45 分）
  - 給範例（few-shot）提升準確率
  - 讓模型分步推理（CoT）處理多步驟問題
  - 同一個模型，換推理策略準確率可從 78% 到 91%
- [ ] **11/05 Context Engineering** ⭐（~90 分）
  - Context 包含：system 指令、檢索文件、工具定義、對話歷史、範例、prompt
  - Token 預算分配；對話歷史的截斷、摘要、滑動視窗
  - 排列 context 讓模型注意到最重要的資訊
- [ ] **11/03 Structured Outputs**（~90 分）
  - 讓 LLM 穩定輸出 JSON；驗證失敗帶錯誤訊息重試
  - Constrained decoding：在 token 層級強制合法格式
- [ ] **14/27 Prompt Injection 防禦**（~75 分）
  - 間接注入：攻擊者把指令藏在 AI 會讀到的資料裡
  - 五類攻擊：竊資、蠕蟲、記憶污染、生態污染、任意工具呼叫
  - 防禦原則：外部內容一律不可信、白名單、人工確認

## ⑦ 讓 AI 接上外部世界（6 課）

> 重點：RAG（讓 AI 讀你的資料）、function calling（讓 AI 呼叫程式）、MCP
> 對使用 AI 的幫助：看懂企業 AI 產品怎麼組成；何時用 RAG、何時用微調

- [ ] **05/23 RAG 的切塊策略（Chunking）**（~60 分）
  - 文件要切成小段才能檢索；切法對品質的影響和 embedding 模型一樣大
- [ ] **11/06 RAG（檢索增強生成）** ⭐（~90 分）
  - 流程：切塊 → embedding → 向量資料庫 → 檢索 → 塞進 prompt → 生成
  - 為什麼企業知識問答選 RAG 而不是微調（成本、即時更新、可追溯來源）
- [ ] **11/07 Advanced RAG**（~90 分）
  - 混合搜尋：關鍵字 + 向量 + 重排序
  - 查詢改寫：HyDE、multi-query、step-back
  - 常見失敗：撈錯段落、答案不在 context、多跳推理失敗
- [ ] **11/09 Function Calling 與工具使用**（~75 分）
  - LLM 本身只會產生文字；「Agent」就是 LLM 輸出 JSON 指定要呼叫哪個函式，再由程式執行
- [ ] **13/01 工具介面**（~45 分）
  - 工具呼叫四步驟：描述 → 決定 → 執行 → 觀察
  - 純函式工具 vs 有副作用的工具，為何影響安全性
- [ ] **13/06 MCP 基礎**（~55 分）
  - MCP 是讓 AI 統一接上各種工具與資料的協定
  - Host、client、server 的角色；JSON-RPC 請求格式

## ⑧ Agent：AI 自己做事（7 課）

> 重點：Agent 迴圈、workflow vs agent、失敗模式、多 Agent 架構
> 對使用 AI 的幫助：看懂 Claude Code、Cursor 怎麼運作、何時容易出錯

- [ ] **14/01 Agent 迴圈：觀察、思考、行動**（~60 分）
  - ReAct 迴圈（Thought / Action / Observation）是所有 Agent 的基礎
  - 為什麼各家框架底層都還是這個迴圈
- [ ] **14/12 Anthropic 的 Workflow 模式** ⭐（~60 分）
  - Workflow（固定流程）vs Agent（動態決定）
  - 五種模式：prompt chaining、routing、parallelization、orchestrator-workers、evaluator-optimizer
  - 原則：能用固定流程就不要用 Agent
- [ ] **14/26 Agent 的失敗模式**（~60 分）
  - 五種常見問題：捏造動作、範圍蔓延、連鎖錯誤、遺失 context、誤用工具
- [ ] **15/01 從聊天機器人到長程 Agent**（~45 分）
  - Agent 能連續工作的時間約每 7 個月翻倍
- [ ] **15/09 Coding Agent 生態（2026）**（~45 分）
  - SWE-bench 三年內從 4% 到 80%；外圍框架的影響和模型一樣大
- [ ] **16/01 為什麼需要多 Agent**（~60 分）
  - 單一 Agent 的瓶頸：context 爆掉、專業混雜、只能循序執行
  - 編排模式：pipeline、平行、supervisor、階層式；複雜度的代價
- [ ] **16/05 Supervisor / Orchestrator-Worker 模式**（~75 分）
  - 主 Agent 規劃分派、子 Agent 平行執行（Anthropic Research 系統的做法）

## ⑧-2 MCP 與 Harness（13 課）

> 重點：MCP 進階概念與安全、Agent 外圍的執行框架（harness / workbench）、Skills
> 對使用 AI 的幫助：看懂 Claude Code 的組成——CLAUDE.md、權限模式、skills、subagents、MCP 各自負責什麼

### MCP 進階
- [ ] **13/10 MCP Resources 與 Prompts**（~60 分）
  - 三種原語的分工：tools 執行動作、resources 提供可定址的內容、prompts 提供訊息範本
  - 依使用者意圖選擇用哪一種；快取設定不可洩漏使用者資料
  - resource 內容與 prompt 範本都要視為不可信的輸出
- [ ] **13/11 MCP Sampling（讓 server 借用 client 的模型）**（~75 分）
  - 新版 MCP 已不建議用 sampling，新設計應直接整合模型
  - 舊流程改用多輪請求（MRTR）：server 回「需要輸入」，client 帶結果重試
  - 用輪數上限、核准、驗證限制模型迴圈
- [ ] **13/12 Roots 與 Elicitation（範圍與向使用者要輸入）**（~60 分）
  - Roots 已棄用，而且從來不是安全沙盒；範圍要明確寫在參數或 URI，並由 server 授權
  - Elicitation：工具需要使用者確認或輸入時的流程（接受 / 拒絕 / 取消）
  - 破壞性操作的確認要綁定使用者身分、原始參數與期限
- [ ] **13/15 MCP 安全：工具投毒** ⭐（~60 分）
  - 工具描述、註解、server 資訊都是不可信資料
  - 偵測描述被竄改、跨 server 工具名稱衝突
  - 授權與限流要綁定使用者，而不是連線

### Harness / Agent Workbench
- [ ] **14/17 Claude Agent SDK：把 Harness 做成函式庫**（~75 分）
  - Client SDK（原始 API）vs Agent SDK（完整 harness：內建工具、hooks、session）
  - Subagent：平行處理與隔離 context
- [ ] **14/31 為什麼強模型仍會失敗** ⭐（~45 分）
  - 模型再強也不夠，可靠的 Agent 需要工作台：指令、狀態、範圍、回饋、驗證、審查、交接
- [ ] **14/32 最小工作台**（~45 分）
  - 三個檔案：指令路由（類似 CLAUDE.md）、狀態檔、任務板
- [ ] **14/33 把指令變成可檢查的約束**（~50 分）
  - 散文式的指令只是願望；寫成約束才能在執行時檢查、事後驗證
- [ ] **14/38 驗證關卡**（~55 分）
  - Agent 不能自己宣告完成；由關卡依範圍、執行紀錄、diff 判斷是否真的完成
- [ ] **14/39 Reviewer Agent**（~55 分）
  - 寫程式的 Agent 不能自己打分；用不同 prompt、唯讀權限的第二個 Agent 審查
- [ ] **15/10 Claude Code 權限模式**（~45 分）
  - 權限階梯：從每個動作都問、到只問高風險、到自動核准
  - Harness 如何控管 Agent 的自主程度

### Skills
- [ ] **13/22 Agent Skills**（~90 分）
  - Skill 不是較長的 prompt，而是可被發現的指令 + 資源 + 輔助程式包
  - 區分 skill、prompt、repo 指令、工具、hook、subagent、plugin
  - 何時該用 skill、MCP 工具、hook、subagent 或一般程式
- [ ] **13/24 Skill 的發現與漸進式載入**（~105 分）
  - 三層載入：目錄中只放名稱與描述 → 用到才載入指令 → 需要時才讀深層資源
  - 節省 context 的設計方式

---

## ⑨ 選讀（有興趣再看）

### 圖片生成
- [ ] **08/01 生成模型分類與歷史**：所有生成模型可歸入五大類
- [ ] **08/06 Diffusion 模型**：逐步加雜訊破壞資料，訓練網路反向去噪
- [ ] **08/07 Stable Diffusion**：在壓縮後的潛在空間做 diffusion，大幅降低運算

### 強化學習細節
- [ ] **09/01 MDP**：所有 RL 演算法的共同框架（狀態、動作、獎勵）
- [ ] **09/08 PPO**：RLHF 使用的主要演算法

### MCP 與 Harness 完整版
- [ ] **MCP 完整路線**（13/06–18、28–31，共 17 課）：見 `phases/13-tools-and-protocols/README.md`
- [ ] **Agent Workbench 其餘課程**（14/34–37、40–42）：repo 狀態、初始化腳本、範圍契約、執行回饋、跨對話交接、實戰比較
- [ ] **Skills 其餘課程**（13/25–27）：skill 路由、權限與沙盒、評估與打包

### 上線與維運
- [ ] **02/19 ML 系統設計**：商業問題框成 ML 任務、指標、上線策略
- [ ] **02/20 監控與漂移**：模型不會報錯，只會慢慢不準
- [ ] **15/12 Durable Execution**：長時間 Agent 的 checkpoint、重試、重播
- [ ] **15/13 成本控管**：防止 Agent 陷入迴圈燒錢
- [ ] **15/14 Kill Switch / Circuit Breaker**：Agent 的緊急停止機制
- [ ] **15/16 Checkpoint 與回滾**：每個動作都要有回滾計畫
- [ ] **16/22 生產擴展**：佇列、checkpoint、冪等
- [ ] **16/23 多 Agent 失敗模式**：最大宗是規格不清
- [ ] **Phase 17**：可觀測性（17/13）、模型路由（17/16）、AI Gateway（17/19）、AI SRE（17/23）

---

## 之後若要轉職做作品

讀完概念後，回頭把 ⑥⑦⑧ 的 Build It 程式實際跑過，再挑一個做成作品：
- RAG 文件問答 + 引用來源（11/06、11/07、11/13）
- 自己的 MCP Server（13/07）
- 用 Spring AI / LangChain4j 以 Java 重做一次
