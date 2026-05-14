**Họ tên**: Đào Văn Công
**Mã sinh viên**: 2A202600031

# Báo cáo Codelab Multi-Agent A2A

## 1. Setup
- Python 3.11+
- uv
- OpenRouter API key
- Model dùng: deepseek/deepseek-v4-flash:free

## 2. Stage 1 - Direct LLM
Đã đổi câu hỏi trong `stages/stage_1_direct_llm/main.py`.
LLM được tạo bằng `get_llm()` trong `common/llm.py`.
Message gồm `SystemMessage` và `HumanMessage`.

## 3. Stage 2 - RAG + Tools
Đã thêm `labor_law` vào `LEGAL_KNOWLEDGE`.
Đã thêm tool `check_statute_of_limitations`.
LLM được bind tool bằng `.bind_tools(tools)`.

## 4. Stage 3 - ReAct Agent
Đã thêm tool `search_case_law`.
Agent tự quyết định gọi `search_legal_database` và `search_case_law`.
Khác Stage 2: Stage 2 dùng manual tool loop, Stage 3 dùng ReAct loop tự động.

## 5. Stage 4 - Multi-Agent
Đã thêm privacy specialist.
Graph gồm:
`analyze_law -> check_routing -> tax/compliance/privacy -> aggregate`.
Dùng `Send()` để chạy các specialist song song.

## 6. Stage 5 - A2A
Các agent chạy độc lập qua HTTP.
Registry dùng để dynamic discovery.
`trace_id` giúp theo dõi request qua nhiều agent.
