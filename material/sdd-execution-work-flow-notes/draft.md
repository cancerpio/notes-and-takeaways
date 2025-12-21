SDD + Execution 的工作流程 & AI Agent的選擇 (待驗證 / 修改)
工作模式: (SDD / Execution)
應該可以定義兩個模式: （同一個 repo 內可以切換） 


SDD（Spec-driven）
主要改 spec（需求/結構/驗收），AI 依 spec 施工（偏 Copilot）
Execution（執行階段）
方向已定，要 AI 大範圍把事情做完（偏 Cursor）
SDD + Execution 的工作流程
大致遵照以下步驟循環 / 迭代

每一輪都遵守：SDD（收斂）→ Execution（落地）→ Review（驗收）→ Spec Sync（對齊）
若開始覺得「一直在改Output / 輸出結果，卻越來越怪」：直接回到 SDD，先把 spec 收斂再繼續 Execution

初始化（只做一次）


建立/更新 constitution：寫清楚風格、限制、檔案結構、驗收標準


建立 spec 的「單一真相」位置（例如 .specify/ 或 docs/spec/）
約定：任何大改最後要回寫到這裡


SDD：收斂與一致性（設計師階段）


把需求寫成可驗收的 spec（不要寫成想法；寫成可檢查的條件）


把變更切小：一次只改 1 個主題/1 組驗收標準


產出明確的 tasks / checklist（讓 AI 能「照圖施工」而不是自由發揮）


Gate：spec 必須滿足「清楚、可驗收、無矛盾」才進 Execution


Execution：用 Cursor 落地（施工階段）


先要求 Cursor 產出「Execution Plan」


會改哪些檔案（檔案清單）


每類檔案怎麼改（策略）


風險點與回復方式（rollback / 邊界）


允許 Cursor 大量改檔、重構、搬移、補內容（以「把事情做完」為優先）


你只做兩件事：看 diff + 抽查關鍵行為/段落（不要在這階段重新發散 spec）


Review Gate：變更驗收（人類把關）


用 spec 的驗收條件逐條對照成果（spec 是裁判，不是參考）


若發現偏離：


小偏離：回到 Execution 叫 Cursor 修正


大偏離：回到 SDD 先修 spec（避免越修越亂）


Spec Sync：回寫 spec（重要, 防分裂護欄）


不論你在 Execution 有沒有「刻意動 spec」


最後都要補一個 Spec Sync：把實際落地結果更新回 spec（結構、行為、章節、限制、已知 trade-off）


原則：spec 不能落後到會誤導下一輪施工



Copilot: Spec-driven（主要在改 Spec，實作交給 AI 依 Spec 產出） 
你花最多時間在「spec / outline / acceptance criteria / tasks」上做調整。


AI Agent 的角色是：根據 spec 把實作或文章內容補齊，並且你用 diff/commit 去驗收。


核心價值
Spec-driven 的核心是「收斂與一致性 + 小步快跑」：


收斂：把需求與輸出定義到清楚、可檢查、可驗收，避免 AI 自由發散。


一致性：每次改動都對齊同一份 spec，讓產出風格與行為穩定可預期。


小步快跑：一次只推進一小段 spec → 生成 → review → commit，快速迭代、快速回滾。


要把 AI 當成「施工隊」，人是「設計師」：


人負責：定義結構、需求、限制、驗收標準。


AI 負責：照著圖把東西蓋出來。


工具最重要的不是「創意」，而是「穩定照圖施工」：


能不能按照 spec 做？


變更是不是可控、可 review？


能不能快速迭代而不失控？


為什麼這裡選 Copilot
Copilot 很適合當「規格導向的施工隊」：


你在熟悉的工作流中做小步迭代、看 diff、做 commit。


它更像是在你的 IDE/Repo 節奏裡，穩定地把 spec 轉成可交付的內容。


操作Tips (讓 Spec-driven 穩定)
每一輪都用同一個節奏：Spec 更新 → Agent 產出 → 你 review → commit。


每次只改一個明確可驗收的點（避免 spec 變動太大導致輸出不可控）。



Cursor: Execution-first（不太動 Spec，主要在做工具/底層開發，或大量調整文章內容）
何謂 Execution-first（你的工作型態）
spec 大致已經定型或暫時不想動（心中已有方向）


想快速把一個想法「徹底落地」，並且通常會牽動大量檔案：


refactor


拆模組


搬檔


統一格式/用語


大範圍修改內容


核心價值
Cursor 的「大量檔案操作」體感確實常比較強。
Ex: 大部分在開發 Tool/底層，或針對文章內容大量調整、不太動 Spec 時
尤其當你心中已經有方向，你要的是 agent “把事情做完”，而不是跟你一起反覆定義 spec。


Spec 仍然是最終真相（一定要有護欄）
就算你「不太動 spec」，也最好把 spec 當成最終要對齊的真相，原因是：
你用 Cursor 大改的速度越快，spec 越容易變成過期文件。


一旦 spec 與現況分裂：


你之後回來用 Spec-driven 會失靈（AI 會照錯的 spec 施工）。


你自己也會失去「這個 repo 現在到底在幹嘛」的單一真相。
