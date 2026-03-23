# 영어는 기다림과 채움의 감각으로 - 이은식어학원
안녕하세요

<img width="155" height="97" alt="image" src="https://github.com/user-attachments/assets/401aeb55-1530-4ce7-b68e-e0efe3ebbca6" />



<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>이은식어학원 - TOEIC 실전 모의고사</title>
    <link rel="stylesheet" as="style" crossorigin href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/static/pretendard.min.css" />
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <style>
        :root {
            --primary-blue: #1a4f8b;
            --light-blue: #eef4fb;
            --accent-gold: #d4af37;
            --text-dark: #333;
            --bg-gray: #f8f9fa;
        }

        * {
            box-sizing: border-box;
            font-family: 'Pretendard', -apple-system, sans-serif;
            /* 보안: 텍스트 선택 방지 */
            -webkit-user-select: none;
            -moz-user-select: none;
            -ms-user-select: none;
            user-select: none;
        }

        body {
            margin: 0;
            background-color: var(--bg-gray);
            color: var(--text-dark);
            line-height: 1.6;
            overflow-x: hidden;
        }

        /* 보안 만료 오버레이 */
        #expiry-overlay {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: white; z-index: 9999;
            flex-direction: column; align-items: center; justify-content: center;
            text-align: center;
        }

        /* 안내문 가이드 오버레이 */
        #guide-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.85);
            z-index: 2000;
            display: flex;
            align-items: center; justify-content: center;
        }

        .guide-content {
            background: white;
            padding: 3rem;
            border-radius: 15px;
            max-width: 550px;
            width: 90%;
            text-align: center;
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
        }

        header {
            background: var(--primary-blue);
            color: white;
            padding: 1.5rem;
            text-align: center;
            position: sticky;
            top: 0;
            z-index: 1000;
        }

        .header-top h1 { margin: 0; font-size: 1.6rem; font-weight: 800; }
        .header-top p { margin: 5px 0 0; font-weight: 300; font-size: 0.9rem; opacity: 0.9; }

        .sticky-controls {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(5px);
            padding: 12px 20px;
            border-bottom: 2px solid var(--primary-blue);
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 88px;
            z-index: 999;
        }

        .progress-container {
            width: 100%;
            height: 6px;
            background: #eee;
            position: fixed;
            top: 88px;
            left: 0;
            z-index: 1001;
        }

        #progress-bar {
            height: 100%;
            background: var(--accent-gold);
            width: 0%;
            transition: width 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .timer { font-weight: 800; color: #d9534f; font-size: 1.3rem; min-width: 80px; }

        main {
            max-width: 1200px;
            margin: 2rem auto;
            padding: 0 1.5rem;
        }

        /* 2단 그리드 */
        .question-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 2.5rem;
            align-items: start;
        }

        @media (max-width: 950px) {
            .question-grid { grid-template-columns: 1fr; }
        }

        .card {
            background: white;
            padding: 2rem;
            border-radius: 12px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
            border-left: 6px solid #e1e1e1;
            transition: transform 0.2s;
        }

        .card.bookmarked { border-left-color: var(--accent-gold); background: #fffdf2; }

        .q-header { display: flex; justify-content: space-between; margin-bottom: 1.2rem; }
        .q-num { font-weight: 900; color: var(--primary-blue); font-size: 1.2rem; }
        .bookmark-btn { cursor: pointer; color: #ddd; font-size: 1.4rem; transition: 0.2s; }
        .bookmark-btn.active { color: var(--accent-gold); }

        .q-text { font-size: 1.15rem; margin-bottom: 1.8rem; line-height: 1.8; color: #222; }

        .options { display: flex; flex-direction: column; gap: 0.9rem; }
        .option {
            padding: 12px 18px;
            border: 1.5px solid #eee;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: 500;
        }
        .option:hover { background: var(--light-blue); border-color: var(--primary-blue); }
        .option.selected {
            background: var(--primary-blue);
            color: white;
            border-color: var(--primary-blue);
        }

        /* 해설 섹션 */
        .explanation-box {
            margin-top: 2rem;
            padding: 1.5rem;
            background: #fdfdfd;
            border: 1px solid #eee;
            border-radius: 10px;
            display: none;
        }

        .result-tag {
            display: inline-block;
            padding: 5px 12px;
            border-radius: 6px;
            font-weight: 800;
            margin-bottom: 15px;
            font-size: 0.9rem;
        }
        .tag-correct { background: #e6ffed; color: #22863a; }
        .tag-wrong { background: #ffeef0; color: #d73a49; }

        .exp-section { margin-bottom: 1.2rem; }
        .exp-title { font-weight: 800; color: var(--primary-blue); font-size: 0.95rem; margin-bottom: 6px; display: block; }
        .exp-content { font-size: 0.95rem; color: #444; }
        .translation { font-style: normal; color: #444; background: #f0f4f8; padding: 12px; border-radius: 8px; font-size: 0.95rem; }
        .vocab-list { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 8px; }
        .vocab-item { background: #fff; border: 1px solid #ddd; padding: 3px 10px; border-radius: 20px; font-size: 0.85rem; }

        .tts-btn {
            background: #f1f3f5;
            color: var(--primary-blue);
            border: 1px solid var(--primary-blue);
            padding: 8px 16px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 0.85rem;
            font-weight: 700;
            margin-top: 10px;
            display: inline-flex;
            align-items: center;
            gap: 6px;
        }
        .tts-btn:hover { background: var(--primary-blue); color: white; }

        footer { background: #222; color: #999; text-align: center; padding: 3rem; margin-top: 5rem; font-size: 0.9rem; }

        .btn-main { background: var(--primary-blue); color: white; border: none; padding: 14px 35px; border-radius: 10px; font-weight: 800; cursor: pointer; font-size: 1.1rem; box-shadow: 0 4px 15px rgba(26, 79, 139, 0.3); }
        .btn-main:active { transform: translateY(2px); }

        #score-board {
            display: none;
            background: white;
            padding: 2.5rem;
            border-radius: 20px;
            text-align: center;
            margin-bottom: 3rem;
            box-shadow: 0 15px 40px rgba(0,0,0,0.1);
            border: 2px solid var(--primary-blue);
        }

        .filter-btns { display: flex; gap: 8px; }
        .btn-sm { padding: 6px 14px; font-size: 0.85rem; border-radius: 20px; border: 1.5px solid #ddd; cursor: pointer; background: white; font-weight: 600; }
        .btn-sm.active { background: var(--primary-blue); color: white; border-color: var(--primary-blue); }
    </style>
</head>
<body oncontextmenu="return false" ondragstart="return false">

    <div id="expiry-overlay">
        <h2 style="color:var(--primary-blue); font-size: 2rem;">🔒 학습 기간이 만료되었습니다.</h2>
        <p>본 콘텐츠는 보안 정책에 따라 생성 후 7일간만 열람 가능합니다.</p>
    </div>

    <div id="guide-overlay">
        <div class="guide-content">
            <h2 style="color:var(--primary-blue); margin-top:0;">TOEIC 실전 모의고사</h2>
            <p style="font-size: 1.1rem; color:#555;">"영어는 기다림과 채움의 감각으로"<br><strong>이은식어학원</strong> 전문 교육 시스템에 오신 것을 환영합니다.</p>
            <div style="text-align:left; background:#f8f9fa; padding:1.5rem; border-radius:10px; margin: 1.5rem 0; font-size:0.95rem;">
                <li style="margin-bottom:8px;">본 시험은 총 <strong>20문항</strong>으로 구성되어 있습니다.</li>
                <li style="margin-bottom:8px;">제한 시간 <strong>10분</strong> 경과 시 자동 채점됩니다.</li>
                <li>채점 후 문장 TTS 듣기 및 상세 해설이 제공됩니다.</li>
            </div>
            <button class="btn-main" onclick="startExam()">테스트 시작</button>
        </div>
    </div>

    <header>
        <div class="header-top">
            <h1>영어 제대로 알려주는 <strong>이은식어학원</strong></h1>
            <p>TOEIC 실전 모의고사 유사문제</p>
        </div>
    </header>

    <div class="progress-container"><div id="progress-bar"></div></div>

    <div class="sticky-controls">
        <div class="timer" id="timer-display">10:00</div>
        <div class="filter-btns">
            <button class="btn-sm" onclick="shuffleQuestions()">🔀 셔플</button>
            <button class="btn-sm" id="bookmark-filter-btn" onclick="toggleBookmarkFilter()">⭐ 북마크</button>
        </div>
        <button class="btn-main" style="padding: 10px 25px; font-size: 0.95rem;" onclick="submitExam()">제출 및 채점</button>
    </div>

    <main>
        <div id="score-board">
            <h2 id="score-text" style="margin-top:0; font-size: 1.8rem;"></h2>
            <div id="answer-grid" style="display: grid; grid-template-columns: repeat(10, 1fr); gap: 6px; max-width: 500px; margin: 1.5rem auto;"></div>
            <p style="color:#666; font-size: 0.9rem;">스크롤을 내려 각 문제의 <b>이은식어학원 전용 해설</b>을 확인하세요.</p>
        </div>

        <div class="question-grid" id="main-grid">
            </div>
    </main>

    <footer>
        "영어는 기다림과 채움의 감각으로 - 이은식어학원"<br>
        <small>Copyright All rights reserved.</small>
    </footer>

    <script>
        // 1. 보안 설정: 7일 만료 로직
        const EXPIRY_KEY = 'ens_exam_expiry_time';
        const now = new Date().getTime();
        let expiryDate = localStorage.getItem(EXPIRY_KEY);

        if (!expiryDate) {
            localStorage.setItem(EXPIRY_KEY, now);
        } else {
            if (now - parseInt(expiryDate) > 7 * 24 * 60 * 60 * 1000) {
                document.getElementById('expiry-overlay').style.display = 'flex';
            }
        }

        // 보안: 단축키 차단
        window.addEventListener('keydown', e => {
            if ((e.ctrlKey && ['c','v','s','u'].includes(e.key)) || e.keyCode === 123) {
                e.preventDefault();
            }
        });

        // 2. 데이터 (18번 수정 반영)
        const rawQuestions = [
            { id: 1, q: "The updated safety manuals for the manufacturing plant -------- to all employees by the human resources department next Monday morning.", options: ["distribute", "are distributing", "will be distributed", "have distributed"], ans: 2, exp: "주어인 safety manuals와 distribute의 관계를 봅니다. 매뉴얼은 배포되는 대상이므로 **수동형용사(P.P)**가 결합된 수동태가 정답입니다.", wrong: "(B)는 현재 진행 능동형으로, 뒤에 목적어가 없으므로 성립할 수 없습니다.", trans: "업데이트된 안전 매뉴얼은 / 제조 공장을 위한 / 배포될 것이다 / 모든 직원들에게 / 인사과에 의해 / 다음 월요일 아침에.", vocab: ["manufacturing 제조", "distribute 배포하다", "department 부서"] },
            { id: 2, q: "Mr. Harrison -------- the final draft of the research proposal before the laboratory assistants arrived at the facility yesterday afternoon.", options: ["finishes", "had finished", "was finished", "is finishing"], ans: 1, exp: "과거 시점(arrived)보다 더 이전에 완료된 사건이므로 과거완료 시제가 정답의 자리입니다.", wrong: "(C)는 수동태입니다. 주어인 Harrison 씨가 초안을 끝내는 주체이므로 능동이 와야 합니다.", trans: "Harrison 씨는 / 마쳤다 / 최종 초안을 / 연구 제안서의 / 실험실 조교들이 도착하기 전에 / 시설에 / 어제 오후에.", vocab: ["final draft 최종 초안", "proposal 제안서", "facility 시설"] },
            { id: 3, q: "Several critical errors in the central financial database -------- by the IT department since the system upgrade was implemented last month.", options: ["have been corrected", "correct", "were corrected", "are correcting"], ans: 0, exp: "since(~이래로)가 이끄는 시점이 과거이므로 주절은 현재완료가 와야 합니다. 에러는 수정되는 것이므로 수동형을 선택합니다.", wrong: "(C)는 단순 과거로, 과거부터 지금까지의 상태를 나타내는 since와 호응할 수 없습니다.", trans: "몇몇 치명적인 오류들이 / 중앙 재무 데이터베이스의 / 수정되어 왔다 / IT 부서에 의해 / 시스템 업그레이드가 실시된 이래로 / 지난달에.", vocab: ["critical 치명적인", "financial 재무의", "implement 실시하다"] },
            { id: 4, q: "The marketing director -------- the promotional video for the upcoming global campaign right now in the main conference room.", options: ["reviews", "was reviewed", "has reviewed", "is reviewing"], ans: 3, exp: "right now는 현재 진행 중인 동작을 나타냅니다. 이사가 비디오를 검토하는 주체이므로 능동 진행형이 정답입니다.", wrong: "(B)는 수동태입니다. 뒤에 목적어(video)가 존재하므로 수동태는 올 수 없습니다.", trans: "마케팅 이사는 / 검토하고 있다 / 홍보 영상을 / 다가오는 글로벌 캠페인을 위한 / 지금 당장 / 메인 회의실에서.", vocab: ["promotional 홍보의", "upcoming 다가오는", "review 검토하다"] },
            { id: 5, q: "All necessary architectural blueprints -------- by the chief engineer by the time the construction crew arrives at the site tomorrow.", options: ["will revise", "will have been revised", "are revising", "have revised"], ans: 1, exp: "by the time 뒤에 현재시제가 미래를 나타낼 때, 주절은 미래완료 시제를 씁니다. 설계도는 수정되는 것이므로 수동형입니다.", wrong: "(A)는 미래 능동태로, 설계도가 스스로 무언가를 수정한다는 논리가 되어 어색합니다.", trans: "모든 필수적인 건축 설계도들은 / 수정되어 있을 것이다 / 수석 엔지니어에 의해 / 건설팀이 현장에 도착할 때쯤 / 내일.", vocab: ["architectural 건축의", "blueprint 설계도", "revise 수정하다"] },
            { id: 6, q: "The logistics company -------- its primary distribution center to a much larger facility in the suburban area two years ago.", options: ["relocated", "is relocated", "relocates", "was relocated"], ans: 0, exp: "two years ago라는 확실한 과거 시점이 있습니다. 회사가 센터를 이전한 것이므로 능동 과거형이 정답입니다.", wrong: "(D)는 수동태입니다. 이전시킨 목적어(center)가 뒤에 바로 나오므로 능동태가 필요합니다.", trans: "그 물류 회사는 / 이전했다 / 그것의 주요 유통 센터를 / 훨씬 더 큰 시설로 / 교외 지역에 있는 / 2년 전에.", vocab: ["logistics 물류", "distribution 유통", "suburban 교외의"] },
            { id: 7, q: "Extensive repairs on the main suspension bridge -------- by the city’s highly skilled maintenance crew at this very moment.", options: ["perform", "are performing", "have performed", "are being performed"], ans: 3, exp: "at this very moment는 진행을 의미합니다. 수리 작업은 수행되는 대상이므로 진행 수동태(be being P.P)가 정답입니다.", wrong: "(B)는 능동 진행형입니다. 수리가 스스로를 수행한다는 뜻이 되어 논리적으로 틀립니다.", trans: "광범위한 수리 작업들이 / 메인 현수교에 대한 / 수행되는 중이다 / 시의 숙련된 유지보수 팀에 의해 / 바로 이 순간에.", vocab: ["extensive 광범위한", "suspension bridge 현수교", "perform 수행하다"] },
            { id: 8, q: "The CEO -------- the official merger agreement with the international conglomerate during the televised press conference held yesterday afternoon.", options: ["signed", "was signed", "has been signed", "signs"], ans: 0, exp: "yesterday afternoon이 있으므로 과거 시제 자리이며, CEO가 직접 서명한 능동 관계입니다.", wrong: "(B)는 수동태입니다. CEO가 서명된 대상이 아니므로 오답입니다.", trans: "CEO는 / 서명했다 / 공식 합병 계약서에 / 국제 대기업과의 / TV로 중계된 기자회견 동안 / 어제 오후에 열린.", vocab: ["merger 합병", "conglomerate 대기업", "press conference 기자회견"] },
            { id: 9, q: "Updated software training manuals -------- to all department heads by the administrative staff by the end of this week.", options: ["distribute", "will be distributed", "are distributing", "have distributed"], ans: 1, exp: "by the end of this week은 미래를 뜻합니다. 매뉴얼은 배포될 대상이므로 미래 수동태가 정답입니다.", wrong: "(D)는 현재완료 능동으로, 미래 시점과는 어울리지 않는 시제입니다.", trans: "업데이트된 소프트웨어 교육 매뉴얼은 / 배포될 것이다 / 모든 부서장들에게 / 행정 직원에 의해 / 이번 주 말까지.", vocab: ["administrative 행정의", "department head 부서장", "distribute 배포하다"] },
            { id: 10, q: "Mr. Henderson -------- for this prestigious law firm for exactly twenty-five years when he finally retires next month.", options: ["works", "is worked", "will have worked", "has been worked"], ans: 2, exp: "next month(미래)에 은퇴할 때를 기점으로 '25년'이라는 기간이 완성되므로 미래완료 시제를 씁니다.", wrong: "(B)는 사람이 수동으로 일 당한다는 뜻이 되어 문맥상 어색합니다.", trans: "Henderson 씨는 / 일해 온 것이 된다 / 이 명성 있는 법률 회사를 위해 / 정확히 25년 동안 / 그가 마침내 은퇴할 때 / 다음 달에.", vocab: ["prestigious 명성 있는", "exactly 정확히", "retire 은퇴하다"] },
            { id: 11, q: "The urgent delivery of the medical supplies -------- due to the unexpected shipment delay at the international port yesterday.", options: ["was delayed", "delay", "is delaying", "has delayed"], ans: 0, exp: "yesterday는 과거 시제입니다. 배송(delivery)은 지연되는 것이므로 과거 수동태가 정답입니다.", wrong: "(D)는 현재완료입니다. yesterday와 같은 명확한 과거 부사와는 함께 사용할 수 없습니다.", trans: "긴급 배송은 / 의료 용품의 / 지연되었다 / 예상치 못한 선적 지연 때문에 / 국제 항구에서의 / 어제.", vocab: ["urgent 긴급한", "shipment 선적", "unexpected 예상치 못한"] },
            { id: 12, q: "We -------- the client’s detailed proposal and will provide our comprehensive feedback within the next few business hours.", options: ["have reviewed", "were reviewed", "are being reviewed", "review"], ans: 0, exp: "과거에 검토하여 현재 그 결과를 가지고 있다는 현재완료 능동의 자리입니다.", wrong: "(B)는 우리가 검토 대상이 된다는 뜻이 되어 뒤의 목적어(proposal)를 설명하지 못합니다.", trans: "우리는 / 검토했다 / 고객의 상세 제안서를 / 그리고 제공할 것이다 / 우리의 포괄적인 피드백을 / 몇 영업 시간 이내에.", vocab: ["comprehensive 포괄적인", "feedback 피드백", "within ~이내에"] },
            { id: 13, q: "The annual budget report -------- by the board of directors in the executive lounge during the meeting next Tuesday.", options: ["discusses", "is discussing", "will be discussed", "had been discussed"], ans: 2, exp: "next Tuesday는 미래입니다. 예산 보고서는 논의되는 것이므로 미래 수동태를 선택합니다.", wrong: "(B)는 보고서가 스스로를 논의한다는 뜻의 능동 진행이라 논리적 오류입니다.", trans: "연간 예산 보고서는 / 논의될 것이다 / 이사회에 의해 / 임원 라운지에서 / 회의 동안 / 다음 주 화요일에.", vocab: ["annual 연간의", "budget 예산", "board of directors 이사회"] },
            { id: 14, q: "Our experienced technicians -------- the complex server connectivity issues continuously since the system crashed early this morning.", options: ["are repaired", "have been repairing", "were repaired", "repair"], ans: 1, exp: "since와 continuously는 완료 진행과 잘 어울립니다. 기술자들이 수리하는 주체이므로 능동형이 맞습니다.", wrong: "(A)는 기술자들이 수리 당한다는 뜻의 수동태라 오답입니다.", trans: "우리의 숙련된 기술자들은 / 수리해오고 있다 / 복잡한 서버 연결 문제를 / 계속해서 / 시스템이 다운된 이후로 / 오늘 아침 일찍.", vocab: ["technician 기술자", "connectivity 연결성", "continuously 계속해서"] },
            { id: 15, q: "The grand opening of the new downtown shopping mall -------- last Friday because of the extremely inclement weather conditions.", options: ["was postponed", "postpones", "is postponing", "has postponed"], ans: 0, exp: "last Friday 과거 시제이며, 개업식 행사는 연기되는 대상이므로 과거 수동태가 정답입니다.", wrong: "(D)는 현재완료로, 특정 과거 시점 부사와는 결합할 수 없습니다.", trans: "성대한 개업은 / 새로운 시내 쇼핑몰의 / 연기되었다 / 지난주 금요일에 / 극심한 악천후 때문에.", vocab: ["postpone 연기하다", "inclement (날씨가) 궂은", "condition 상태"] },
            { id: 16, q: "By the end of this fiscal quarter, the legal department -------- all the necessary contracts for the new partnership.", options: ["will be signed", "has signed", "signs", "will have signed"], ans: 3, exp: "By the end of (미래시점)은 미래완료를 부르는 단서입니다. 부서가 서명하는 능동 관계입니다.", wrong: "(A)는 미래 수동태로, 뒤에 서명할 대상(contracts)이 있으므로 불가합니다.", trans: "이번 회계 분기 말까지 / 법무 부서는 / 서명 완료했을 것이다 / 모든 필수 계약서에 / 새로운 파트너십을 위한.", vocab: ["fiscal quarter 회계 분기", "legal 법률의", "contract 계약서"] },
            { id: 17, q: "Detailed instructions for the online registration process -------- to all registered participants before the international seminar begins.", options: ["send", "are sending", "will be sent", "had sent"], ans: 2, exp: "지침은 발송되는 것이며, 세미나 시작 전이라는 미래 시점을 나타내므로 미래 수동태가 정답입니다.", wrong: "(B)는 능동 진행형입니다. 지침이 스스로를 보낸다는 뜻이 되어 틀립니다.", trans: "상세 지침은 / 온라인 등록 절차를 위한 / 발송될 것이다 / 모든 등록된 참가자들에게 / 국제 세미나가 시작되기 전에.", vocab: ["instruction 지침", "registration 등록", "participant 참가자"] },
            { 
                id: 18, 
                q: "The head chef -------- a special five-course menu for the charity gala scheduled for this Saturday evening.", 
                options: ["was prepared", "is preparing", "have prepared", "prepare"], 
                ans: 1, 
                exp: "셰프가 직접 메뉴를 준비하는 '능동' 관계이며, 현재 준비하고 있는 상태를 나타내는 진행형이 정답입니다.", 
                wrong: "(C) **have prepared**는 주어인 The head chef(단수)와 수 일치가 맞지 않아 답이 될 수 없습니다.", 
                trans: "수석 주방장은 / 준비하고 있다 / 특별한 5코스 메뉴를 / 자선 행사를 위한 / 이번 토요일 저녁으로 예정된.", 
                vocab: ["charity gala 자선 행사", "prepare 준비하다", "scheduled 예정된"] 
            },
            { id: 19, q: "The internal system upgrade -------- by the IT staff while most of the office employees were at lunch yesterday.", options: ["was completed", "completes", "is completing", "had completed"], ans: 0, exp: "yesterday는 과거입니다. 업그레이드는 IT 직원에 의해 완료되는 것이므로 과거 수동태를 씁니다.", wrong: "(D)는 과거완료 능동형으로 업그레이드가 무언가를 끝낸다는 뜻이 되어 논리상 틀립니다.", trans: "내부 시스템 업그레이드는 / 완료되었다 / IT 직원에 의해 / 대부분의 사무실 직원들이 점심 식사 중인 동안 / 어제.", vocab: ["internal 내부의", "upgrade 업그레이드", "employee 직원"] },
            { id: 20, q: "New environmental safety regulations -------- by the local government in response to the recent accidents at the industrial site.", options: ["propose", "are proposing", "have proposed", "have been proposed"], ans: 3, exp: "규정이 제안되어 온 상태를 나타냅니다. 규정은 제안되는 수동 관계이므로 현재완료 수동태가 정답입니다.", wrong: "(C)는 능동형으로 목적어가 필요하며 의미상으로도 규정이 스스로 제안한다는 뜻이라 오답입니다.", trans: "새로운 환경 안전 규정들이 / 제안되었다 / 지방 정부에 의해 / 최근 사고들에 대한 대응으로 / 산업 현장에서의.", vocab: ["regulation 규정", "industrial 산업의", "propose 제안하다"] }
        ];

        let questions = [...rawQuestions];
        let userAnswers = {};
        let bookmarks = new Set();
        let timeLeft = 600;
        let timerId = null;
        let isSubmitted = false;
        let filterOnlyBookmarked = false;

        // 3. 실행 함수
        function startExam() {
            document.getElementById('guide-overlay').style.display = 'none';
            renderQuestions();
            startTimer();
        }

        function startTimer() {
            timerId = setInterval(() => {
                timeLeft--;
                const mins = Math.floor(timeLeft / 60);
                const secs = timeLeft % 60;
                document.getElementById('timer-display').innerText = `${mins}:${secs.toString().padStart(2, '0')}`;
                if (timeLeft <= 0) { clearInterval(timerId); submitExam(); }
            }, 1000);
        }

        function renderQuestions() {
            const grid = document.getElementById('main-grid');
            grid.innerHTML = '';
            
            let displayList = filterOnlyBookmarked 
                ? questions.filter(q => bookmarks.has(q.id))
                : questions;

            displayList.forEach((q, idx) => {
                const card = document.createElement('div');
                card.className = `card ${bookmarks.has(q.id) ? 'bookmarked' : ''}`;
                card.innerHTML = `
                    <div class="q-header">
                        <span class="q-num">Q ${idx + 1}</span>
                        <span class="bookmark-btn ${bookmarks.has(q.id)?'active':''}" onclick="toggleBookmark(${q.id})">⭐</span>
                    </div>
                    <div class="q-text">${q.q.replace('--------', '<span style="border-bottom: 2px solid #555; padding: 0 20px;">&nbsp;</span>')}</div>
                    <div class="options">
                        ${q.options.map((opt, i) => `
                            <div class="option ${userAnswers[q.id] === i ? 'selected' : ''}" onclick="selectOption(${q.id}, ${i})">
                                (${String.fromCharCode(65+i)}) ${opt}
                            </div>
                        `).join('')}
                    </div>
                    <div class="explanation-box" id="exp-${q.id}">
                        <div class="result-tag" id="tag-${q.id}"></div>
                        <div class="exp-section"><span class="exp-title">정답 근거</span><div class="exp-content">${q.exp}</div></div>
                        <div class="exp-section"><span class="exp-title">오답 분석</span><div class="exp-content">${q.wrong}</div></div>
                        <div class="exp-section"><span class="exp-title">직독직해</span><div class="translation">${q.trans}</div></div>
                        <div class="vocab-list">${q.vocab.map(v => `<span class="vocab-item">${v}</span>`).join('')}</div>
                        <button class="tts-btn" onclick="playTTS(${q.id})">🔊 정답 문장 듣기</button>
                    </div>
                `;
                grid.appendChild(card);
            });
            updateProgress();
        }

        function selectOption(qId, i) { if(isSubmitted) return; userAnswers[qId] = i; renderQuestions(); }
        function toggleBookmark(qId) { if(bookmarks.has(qId)) bookmarks.delete(qId); else bookmarks.add(qId); renderQuestions(); }
        function shuffleQuestions() { if(isSubmitted) return; questions.sort(() => Math.random() - 0.5); renderQuestions(); }
        function toggleBookmarkFilter() { 
            filterOnlyBookmarked = !filterOnlyBookmarked; 
            document.getElementById('bookmark-filter-btn').classList.toggle('active');
            renderQuestions(); 
        }
        function updateProgress() { 
            const p = (Object.keys(userAnswers).length / questions.length) * 100;
            document.getElementById('progress-bar').style.width = p + '%';
        }

        function submitExam() {
            if(isSubmitted) return;
            if(!confirm('채점하시겠습니까?')) return;
            isSubmitted = true;
            clearInterval(timerId);

            let score = 0;
            const ansGrid = document.getElementById('answer-grid');
            ansGrid.innerHTML = '';

            questions.sort((a,b)=>a.id-b.id).forEach((q, idx) => {
                const isCorrect = userAnswers[q.id] === q.ans;
                if(isCorrect) score++;

                const dot = document.createElement('div');
                dot.style.padding = '4px';
                dot.style.fontSize = '0.75rem';
                dot.style.borderRadius = '4px';
                dot.style.background = isCorrect ? '#e6ffed' : '#ffeef0';
                dot.style.color = isCorrect ? '#22863a' : '#d73a49';
                dot.style.border = `1px solid ${isCorrect ? '#22863a' : '#d73a49'}`;
                dot.innerText = `${idx+1}:${String.fromCharCode(65+q.ans)}`;
                ansGrid.appendChild(dot);

                const expBox = document.getElementById(`exp-${q.id}`);
                const tag = document.getElementById(`tag-${q.id}`);
                if(expBox) {
                    expBox.style.display = 'block';
                    tag.className = `result-tag ${isCorrect ? 'tag-correct' : 'tag-wrong'}`;
                    tag.innerText = isCorrect ? 'CORRECT' : 'INCORRECT';
                }
            });

            document.getElementById('score-board').style.display = 'block';
            document.getElementById('score-text').innerText = `SCORE: ${Math.round(score/questions.length*100)}점 (${score}/${questions.length})`;
            
            if(score === questions.length) confetti({ particleCount: 200, spread: 80, origin: { y: 0.6 } });
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function playTTS(qId) {
            const q = rawQuestions.find(x => x.id === qId);
            const text = q.q.replace('--------', q.options[q.ans]);
            const u = new SpeechSynthesisUtterance(text);
            u.lang = 'en-US';
            u.rate = 0.85;
            window.speechSynthesis.speak(u);
        }
    </script>
</body>
</html>
