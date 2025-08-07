파이드파케 요약기 앱 설계 문서

요약

1. PDF 드래그 앤 드롭
	•	사용자가 PDF를 앱의 지정 영역에 드래그하면 자동 업로드 및 파싱 수행
	•	머리파일 지원 (향후 기다리 가능)

2. 자동 텍스트 추출
	•	PDFKit을 활용하여 텍스트 레이아웃 유지하며 PDF 컨텐츠 추출
	•	페이지별, 세츠이어별로 텍스트 블록 구분 가능

3. GPT 요약 처리
	•	OpenAI GPT API 호출로 전체 문서 요약 생성
	•	자동 텍스트 전처리 후 요약 요청
	•	토큰 수 제한 대응: 페이지 단위 요약 → 전체 통합 요약 가능

4. 세츠별 요약
	•	Table of Contents(TOC) 또는 추론 기반으로 Abstract, Introduction, Conclusion 등 세츠전 자동 분리
	•	각 세츠에 대해 개별 요약 수행

5. 요약 결과 저장 및 복사
	•	요약된 텍스트를 클립보드 복사 또는 저장 (ex: .txt, .md)
	•	앱 내 로커루 저장: CoreData 또는 UserDefaults로 캐시드

6. (예정) 질문/답변 기능 (Q&A)
	•	요약된 내용을 기반으로 사용자 질문에 대해 답변 생성 (RAG 또는 GPT-contextual approach 사용)
	•	예: “이 노릇의 해제 가스루는?”, “실험 결과의 주요 시사점은?”

⸻

키워드

번류	스템
플랫폼	iOS, iPadOS, macOS (SwiftUI 기반)
PDF 파싱	PDFKit
전처리	Natural Language 프매워크, Custom Parser (ex: 정규표현식 기반 세츠검지)
요약	GPT API (OpenAI GPT-4o 참고)
저장	CoreData 또는 UserDefaults
UI 기능	Drag & Drop, SplitView, Copy to Clipboard, 파일 선택기


⸻

테스트 구조 (UI)

페이지 구조

+---------------------------------------------------------+
| Drag here to upload your PDF                            |
+---------------------------------------------------------+
| 문서제목                                                  |  
|                              |
| ┌────────────────────────────└────────────────────────────┘
| │ 원문 미리보기 │      GPT 요약 결과 보기             │
| │ (PDF View)    │   (Section, Abstract, etc 구분)     │
| └────────────────────────────┘────────────────────────────┘

요약 결과 보기
	•	전체 요약
	•	챕터별 요약
	•	Abstract
	•	Introduction
	•	Methods
	•	Results
	•	Conclusion
	•	복사 or 저장 버튼
