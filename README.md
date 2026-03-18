## 長照 3.0 政策諮詢 RAG

建立一個基於 Retrieval-Augmented Generation (RAG) 技術的智能問答系統，用於提供關於「長照十年計畫 3.0 核定本」政策的諮詢服務。由於原始政策文件內容龐大且專業術語繁多，本系統透過自然語言處理技術，讓使用者能夠快速、準確地檢索並理解政策核心內容。
https://1966.gov.tw/LTC/cp-6572-85008-207.html

**核心流程包括：**

1.  **文件讀取與切割**：利用 `PyPDFLoader` 載入 PDF 政策文件，並使用 `RecursiveCharacterTextSplitter` 將文件切分成易於檢索的小片段。
2.  **向量化與建立向量資料庫 (VectorDB)**：採用多語言優化的 `paraphrase-multilingual-MiniLM-L12-v2` 嵌入模型，將文本片段轉換為向量表示，並儲存於 `Chroma` 向量資料庫中，以便進行高效的語義搜索。
3.  **RAG Chain 建構**：整合 LangChain 的 `create_retrieval_chain` 與 Google Gemini 2.5 Flash API。透過 System Prompt，限制 AI 模型的回答僅基於檢索到的文件內容，有效避免「幻覺」現象。
4.  **實際問答與驗證**：系統能夠接受使用者提問，從向量資料庫中檢索相關文本片段，並結合大型語言模型生成具事實基礎的回答。同時，也初步提到了使用 RAGAS 評估系統性能的重要性，關注回答的忠實性 (Faithfulness)、相關性 (Answer Relevancy) 和上下文精確度 (Context Precision)。

透過這個系統，希望能降低民眾理解長照政策的門檻，提升資訊獲取的效率與準確性。
