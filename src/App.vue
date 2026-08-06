<script setup>
import { computed, nextTick, onMounted, onUnmounted, ref } from 'vue'
import {
  AppWindow,
  Award,
  Blocks,
  BookOpenCheck,
  Bot,
  Building2,
  CalendarDays,
  Code2,
  Eye,
  Factory,
  GitPullRequest,
  GraduationCap,
  ListChecks,
  Recycle,
  ShieldCheck,
  TableProperties
} from '@lucide/vue'

const language = ref('ko')
const selectedProject = ref(null)

const workIcons = {
  UI: TableProperties,
  FW: Blocks,
  BD: AppWindow,
  GD: BookOpenCheck
}

const aboutMetricIcons = [Factory, BookOpenCheck, GraduationCap]
const projectIcons = {
  framework: Blocks,
  manufacturing: Factory,
  recycle: Recycle
}
const frameworkIcons = [BookOpenCheck, CalendarDays, AppWindow, GraduationCap]
const workflowIcons = [Bot, Code2, ShieldCheck, GitPullRequest]

const profile = {
  nameKo: '김신예',
  nameEn: 'Shinye Kim',
  phone: '010-8539-4655',
  positionKo: '주임',
  positionEn: 'Assistant Manager',
  departmentKo: '제조솔루션2팀',
  departmentEn: 'Manufacturing Solution Team 2',
  educationKo: '학사 졸업 (2020.02.26)',
  educationEn: "Bachelor's degree (Graduated Feb 26, 2020)",
  techCategoryKo: 'MES',
  techCategoryEn: 'MES',
  companyKo: 'LS 티라유텍',
  companyEn: 'LS ThiraUtech',
  tenureKo: '2023.11.01 ~ 현재',
  tenureEn: 'Nov 1, 2023 ~ Present',
  email: 'sykim01224@gmail.com'
}

const navItems = [
  { id: 'about', label: 'About' },
  { id: 'skills', label: 'Skills' },
  { id: 'projects', label: 'Projects' },
  { id: 'experience', label: 'Experience' },
  { id: 'ai-workflow', label: 'AI Workflow' },
  { id: 'contact', label: 'Contact' }
]

const stackIcons = {
  HTML: { image: 'https://cdn.simpleicons.org/html5/E34F26', mark: 'H' },
  CSS: { image: 'https://cdn.simpleicons.org/css/663399', mark: 'C' },
  JavaScript: { image: 'https://cdn.simpleicons.org/javascript/F7DF1E', mark: 'JS' },
  jQuery: { image: 'https://cdn.simpleicons.org/jquery/0769AD', mark: 'JQ' },
  'Vue.js': { image: 'https://cdn.simpleicons.org/vuedotjs/4FC08D', mark: 'V' },
  'Element Plus': { image: '', mark: 'EP' },
  ECharts: { image: 'https://cdn.simpleicons.org/apacheecharts/AA344D', mark: 'EC' },
  'Node.js': { image: 'https://cdn.simpleicons.org/nodedotjs/5FA04E', mark: 'N' },
  'Electron.js': { image: 'https://cdn.simpleicons.org/electron/47848F', mark: 'EL' },
  MSSQL: { image: '', mark: 'MS' },
  Oracle: { image: '', mark: 'OR' },
  PostgreSQL: { image: 'https://cdn.simpleicons.org/postgresql/4169E1', mark: 'PG' },
  TypeScript: { image: 'https://cdn.simpleicons.org/typescript/3178C6', mark: 'TS' },
  Flutter: { image: 'https://cdn.simpleicons.org/flutter/02569B', mark: 'FL' },
  'Java / Spring': { image: 'https://cdn.simpleicons.org/spring/6DB33F', mark: 'SP' }
}

function stackMeta(item) {
  return stackIcons[item] ?? { image: '', mark: item.slice(0, 2).toUpperCase() }
}

const translations = {
  ko: {
    profileName: profile.nameKo,
    company: profile.companyKo,
    tenure: profile.tenureKo,
    heroEyebrow: 'MES · B2B Frontend',
    heroRole: 'B2B 프론트엔드 개발자',
    heroText:
      '제조업 MES 프로젝트에서 그리드, 폼, 팝업, API 연동 중심의 업무 화면을 개발하고, 사내 UI 프레임워크 운영과 가이드·교육을 함께 수행하고 있습니다.',
    current: 'Current',
    tenureLabel: 'Tenure',
    emailLabel: 'Email',
    primaryAction: '대표 프로젝트 보기',
    secondaryAction: '연락하기',
    aboutTitle: '실무에 강한 프론트엔드 개발자',
    aboutKicker: 'Frontend Focus',
    aboutLead: '요구사항을 안정적인 업무 화면으로 연결합니다',
    aboutText:
      'B2B 업무 시스템에서 사용자가 매일 쓰는 화면의 흐름과 완성도를 중요하게 봅니다. 프로젝트 화면 개발 경험과 사내 UI 프레임워크 운영 경험을 바탕으로, 팀이 일관된 방식으로 화면을 만들 수 있는 환경까지 함께 개선해 왔습니다.',
    aboutMetrics: [
      ['6건+', '구축·개발 프로젝트 수행'],
      ['90%+', '사내 UI 가이드 작성 기여'],
      ['약 10회', '사내·고객사 개발자 교육']
    ],
    labels: {
      name: '이름',
      phone: '연락처',
      position: '직위',
      department: '부서',
      education: '최종학력',
      techCategory: '기술구분',
      company: '재직 회사',
      tenure: '재직 기간'
    },
    strengths: [
      'Vue 3 기반 MES·B2B 업무 시스템 개발',
      '사내 UI 프레임워크 및 공통 컴포넌트 운영·개선',
      'AUIGrid 기반 데이터 관리 화면과 동적 그리드 개발',
      'UI Builder 및 메타데이터 기반 화면 구성 기능 개선',
      '개발 가이드 작성, 개발자 교육, 프로젝트 UI 이슈 해결'
    ],
    coreWorksTitle: '핵심 업무',
    coreWorks: [
      {
        icon: 'UI',
        title: 'MES 업무 화면',
        text: '그리드, 공정 화면, 리포트, 바코드 입력 UI 구현'
      },
      {
        icon: 'FW',
        title: 'UI 프레임워크',
        text: '공통 컴포넌트와 Core 패키지 운영·개선'
      },
      {
        icon: 'BD',
        title: 'UI Builder',
        text: '메타데이터 기반 화면 구성과 빌더 기능 유지보수'
      },
      {
        icon: 'GD',
        title: '가이드·교육',
        text: 'VitePress 문서 작성, 개발자 교육, 프로젝트 이슈 지원'
      }
    ],
    strengthKicker: 'Core Work',
    strengthTitle: '업무 화면 개발 강점',
    snapshotTitle: '현재 핵심 업무',
    snapshotName: 'WEBUI 2.0 사내 UI 프레임워크',
    snapshotText:
      '공통 컴포넌트, Core 패키지, UI Builder, 개발 가이드를 운영하며 여러 프로젝트가 안정적으로 사용할 수 있는 UI 개발 환경을 개선하고 있습니다.',
    snapshotItems: [
      ['화면', 'MES 업무 화면 90개 이상 개발'],
      ['Builder', 'UI Builder 약 1년 운영·개선'],
      ['Guide', 'VitePress 기반 개발 가이드 작성'],
      ['Award', '2026년 상반기 우수사원 선정']
    ],
    skillsTitle: '기술 스택',
    skillGroups: [
      { title: 'Language', items: ['JavaScript', 'HTML', 'CSS', 'SCSS'] },
      { title: 'Framework', items: ['Vue.js', 'Vite', 'Pinia', 'Vue Router', 'jQuery'] },
      { title: 'UI / Chart', items: ['AUIGrid', 'Element Plus', 'ECharts'] },
      { title: 'Tool', items: ['Node.js', 'Electron.js', 'VitePress', 'Git', 'SVN', 'DBeaver', 'VSCode'] },
      {
        title: 'Database',
        note: '데이터 확인 및 기본 조회 쿼리 작성 용도',
        items: ['MSSQL', 'Oracle', 'PostgreSQL']
      }
    ],
    projectsTitle: '대표 프로젝트',
    projectLabels: ['개요', '역할', '기여'],
    projectModalLabel: '자세히 보기',
    closeLabel: '닫기',
    projects: [
      {
        icon: 'framework',
        category: 'Internal Platform',
        status: '진행 중',
        name: 'WEBUI 2.0 사내 UI 프레임워크 및 UI Builder',
        period: '2024.09 ~ 현재',
        stack: 'Vue 3, UI Framework, UI Builder, VitePress, Electron.js',
        summary: '사내 UI 프레임워크와 UI Builder를 운영·개선하며 공통 UI 개발 환경을 관리하고 있습니다.',
        detail: {
          overview: 'Vue 3 기반 B2B 업무 시스템 개발에 사용되는 사내 UI 프레임워크와 UI Builder를 운영하고 개선하는 프로젝트입니다.',
          role: [
            'Core 패키지와 표준 UI 프로젝트의 분리 구조 관리',
            '공통 컴포넌트 기능 개선 및 오류 수정',
            'UI Builder 기능 추가, 구조 개선 및 유지보수',
            'VitePress 기반 UI 개발 가이드 작성 및 교육'
          ],
          contribution: [
            '대형 모니터 공정 화면을 위한 폰트 크기, 다크 모드, 화면 확장 기능 개선',
            'keep-alive와 메뉴 상태 저장·복원 로직으로 화면 전환 안정성 개선',
            '프로젝트 요구사항을 개별 화면이 아닌 공통 프레임워크 기능으로 확장',
            '약 1년간 UI Builder 기능 추가, 오류 수정, 테스트 및 프로젝트 이슈 대응'
          ]
        }
      },
      {
        icon: 'manufacturing',
        category: 'Manufacturing MES',
        status: '구축 완료',
        name: 'G2 MES 구축',
        period: '2025.06 ~ 2025.10',
        stack: 'WEBUI 1.0, JavaScript, AUIGrid, MSSQL, LPS/ZPL',
        summary: '공정 화면, 동적 그리드, 바코드 입력, 라벨 출력 연동을 구현했습니다.',
        detail: {
          overview: '제조업 MES 구축 프로젝트에서 공정 화면 중심의 복잡한 UI와 대량 데이터 입력 흐름을 구현했습니다.',
          role: [
            '약 40개 규모의 MES 업무 화면 개발',
            '조건에 따라 변경되는 동적 그리드 구성',
            '엑셀 Copy & Paste 기반 대량 데이터 입력 처리',
            '바코드 스캔 및 LPS/ZPL 라벨 출력 연동 흐름 분석'
          ],
          contribution: [
            '빠른 연속 바코드 입력 시 일부 데이터가 누락되는 문제 분석',
            'Key 이벤트와 콜백 처리 타이밍 차이를 확인하고 순차 반영 방식으로 개선',
            '처리 상태를 확인할 수 있도록 로딩 UI 적용',
            '라벨 출력 데이터 전달 흐름 분석 및 관련 화면 수정 지원'
          ]
        }
      },
      {
        icon: 'recycle',
        category: 'MES & Operations',
        status: '구축·운영',
        name: '에너지머티리얼즈 MES 구축 및 유지보수',
        period: '2023.11 ~ 2024.08',
        stack: 'WEBUI 1.0, JavaScript, AUIGrid, MSSQL',
        summary: '그리드·리포트성 업무 화면을 개발하고 약 6개월간 운영 이슈를 대응했습니다.',
        detail: {
          overview: '배터리 재활용 MES 시스템 구축 프로젝트에서 프론트엔드 화면 개발과 운영 유지보수를 담당했습니다.',
          role: [
            '약 30개 데이터 관리 및 리포트성 화면 개발',
            '검색 조건, 콤보박스, 팝업, 버튼 이벤트 구현',
            '저장 전 필수값 및 데이터 유효성 검사 처리',
            'REST API 연동 및 MSSQL 데이터 확인'
          ],
          contribution: [
            '운영 중 발생한 UI 오류와 데이터 표시 문제 분석 및 수정',
            'AUIGrid 기반 조회, 동적 컬럼, 저장·수정·삭제 흐름 구현',
            '반복 화면 이슈의 원인을 분석하고 유사 화면에 공통 대응 방식 적용',
            '장기간 유지보수로 실제 사용자 요청 기반 운영 대응 경험 확보'
          ]
        }
      }
    ],
    experienceTitle: '프로젝트 참여 이력',
    awardLabel: 'Recognition',
    awardTitle: '2026년 상반기 우수사원',
    careerSummary: '6건의 구축·개발 프로젝트를 수행했으며, 사내 UI 프레임워크 운영과 차기 프로젝트 준비를 병행하고 있습니다.',
    experienceSubTitle: '업무 경험',
    experienceCountLabel: '프로젝트',
    experienceAction: '업무 보기',
    experienceCards: [
      {
        period: '2026.08 ~ 2026.11 예정',
        company: '대한항공 MES 프로젝트',
        role: '개발 / 주임',
        title: 'WEBUI 1.0 기반 JavaScript UI 개발 예정',
        summary: '항공 제조/운영 업무 흐름에 맞춘 MES 업무 화면 개발을 WEBUI 1.0 환경에서 수행할 예정입니다.',
        bullets: ['JavaScript 기반 업무 화면 개발', '그리드/폼/팝업/API 연동 화면 구현', '프로젝트 표준에 맞춘 UI 개발 대응']
      },
      {
        period: '2025.06.20 ~ 2025.10.31',
        company: 'LS Electric G2 MES 구축',
        role: '개발 / 주임',
        title: 'MES 업무 화면 개발 및 이슈 대응',
        summary: '공정 화면과 대량 데이터 입력 흐름을 포함한 약 40개 업무 화면을 개발했습니다.',
        bullets: ['동적 그리드와 엑셀 Copy & Paste 입력 구현', '바코드 연속 입력 누락 이슈 분석 및 처리 흐름 개선', 'LPS/ZPL 라벨 출력 연동 화면 지원']
      },
      {
        period: '2025.05.22 ~ 2025.07.30',
        company: '이녹스리튬 MES 구축',
        role: '개발 / 주임',
        title: '리튬 생산 MES 업무 화면 개발',
        summary: 'WEBUI 1.0 표준에 맞춰 데이터 조회, 입력, 저장 중심의 MES 화면을 구현했습니다.',
        bullets: ['JavaScript와 AUIGrid 기반 UI 개발', '그리드 CRUD, 폼 유효성 검사, API 연동', 'MSSQL 데이터 확인 및 프로젝트 이슈 대응']
      },
      {
        period: '2024.09.23 ~ 현재',
        company: 'WEBUI 2.0',
        role: '개발 / 주임',
        title: 'Vue 3 기반 사내 UI 프레임워크 개발 및 운영',
        summary: '차세대 UI 프레임워크, 공통 컴포넌트, 가이드, 정기 배포, Builder를 운영하고 있습니다.',
        bullets: ['UI 가이드 문서 90% 이상 작성', '매주 정기 배포 및 프로젝트 적용 이슈 대응', 'Electron.js Builder 관리와 개발자 교육 약 10회 진행']
      },
      {
        period: '2024.06.17 ~ 2024.12.12',
        company: '에너테크 MES 개발',
        role: '개발 / 사원',
        title: '배터리 MES 시스템 UI 개발',
        summary: '러시아 Kaliningrad·Moscow 사업장 대상 배터리 MES 업무 화면을 개발했습니다.',
        bullets: ['WEBUI 1.0과 JavaScript 기반 UI 개발', 'PostgreSQL 데이터 확인 및 API 연동', '그리드·폼·팝업 중심 업무 기능 구현']
      },
      {
        period: '2024.05.08 ~ 2024.06.05',
        company: '코마테크 MES 구축',
        role: '개발 / 사원',
        title: 'MES 업무 화면 개발 지원',
        summary: '단기 구축 일정에 맞춰 WEBUI 1.0 기반 MES 화면 개발과 기능 수정을 수행했습니다.',
        bullets: ['JavaScript 기반 UI 개발', 'Oracle 데이터 확인과 화면 연동', '프로젝트 표준에 맞춘 그리드·폼 기능 구현']
      },
      {
        period: '2023.11.15 ~ 2024.08.31',
        company: '에너지머티리얼즈 MES 구축',
        role: '개발 / 사원',
        title: '배터리 재활용 MES UI 개발',
        summary: '제조 현장 데이터 조회, 입력, 저장 흐름을 안정적인 업무 화면으로 구현했습니다.',
        bullets: ['WEBUI 1.0 기반 UI 개발 100%', '그리드 CRUD, 유효성 검사, 팝업 처리', '프로젝트 화면 이슈 및 변경 요청 대응']
      }
    ],
    tableHeads: ['프로젝트', '기간', '참여 형태', '주요 역할'],
    experience: [
      ['LS 티라유텍', '2023.11.01 ~ 현재', '주임', 'MES 개발, FrontEnd: JavaScript/Vue.js, DBMS: Oracle/MSSQL/PostgreSQL'],
      ['에너지머티리얼즈 MES 구축', '2023.11.15 ~ 2024.08.31', '개발 / 사원', 'WEBUI 1.0, JavaScript, MSSQL 기반 UI 개발 100%'],
      ['코마테크 MES 구축', '2024.05.08 ~ 2024.06.05', '개발 / 사원', 'WEBUI 1.0, JavaScript, Oracle 기반 UI 개발 100%'],
      ['에너테크 MES 개발', '2024.06.17 ~ 2024.12.12', '개발 / 사원', 'WEBUI 1.0, JavaScript, PostgreSQL 기반 UI 개발 100%'],
      ['WEBUI 2.0', '2024.09.23 ~ 현재', '개발 / 주임', 'Vue.js, MSSQL 기반 차세대 솔루션 UI 개발 100%'],
      ['이녹스리튬 MES 구축', '2025.05.22 ~ 2025.07.30', '개발 / 주임', 'WEBUI 1.0, JavaScript, MSSQL 기반 UI 개발 100%'],
      ['LS Electric G2 MES 구축', '2025.06.20 ~ 2025.10.31', '개발 / 주임', 'WEBUI 1.0, JavaScript, MSSQL 기반 UI 개발 100%'],
      ['대한항공 MES 프로젝트', '2026.08 ~ 2026.11 예정', '개발 / 주임', 'WEBUI 1.0, JavaScript 기반 UI 개발 예정']
    ],
    frameworkTitle: '사내 UI 프레임워크 경험',
    frameworkSubTitle: '공통 UI 개발 환경을 운영하고 개선했습니다',
    frameworkText:
      'Vue.js 기반 WEBUI 2.0 사내 UI 프레임워크 개발에 참여하고 있으며, MES 프로젝트에서 반복되는 그리드, 폼, 팝업, API 연동 화면 패턴을 공통화하고 내부 개발자가 일관된 방식으로 사용할 수 있도록 가이드, 배포, 빌더 관리, 교육, 이슈 대응을 수행하고 있습니다.',
    frameworkStats: [
      ['90%+', 'UI 가이드 문서 작성 기여도'],
      ['Weekly', '사내 프레임워크 정기 배포'],
      ['Electron', '컴포넌트 등록용 빌더 관리'],
      ['10회+', '사내/고객사 개발자 교육']
    ],
    frameworkItems: [
      'Vue.js 기반 WEBUI 2.0 화면 개발 및 사내 UI 프레임워크 개선',
      '그리드, 폼, 검색 조건, 팝업, API 연동 중심의 공통 화면 패턴 정리',
      'UI 개발 가이드 문서 90% 이상 작성 및 프로젝트 적용 문의 대응',
      '컴포넌트 등록용 Electron.js 빌더 관리 및 사용 흐름 개선',
      '매주 정기 배포, 프로젝트별 이슈/기능 요청 검토 및 반영',
      '사내 및 고객사 개발자 대상 프레임워크 교육 약 10회 진행'
    ],
    workflowTitle: 'AI를 초안 작성과 검증 보조 도구로 활용합니다',
    workflow: [
      '반복적인 CRUD 화면 구조와 유효성 검사 코드의 초안을 AI 개발 보조 도구로 빠르게 작성',
      '생성된 코드를 프로젝트 자체 UI 프레임워크 구조에 맞게 직접 수정',
      '그리드 이벤트, 저장/삭제 흐름, 예외 처리, 사용자 메시지를 직접 검증 후 반영',
      '중복 로직을 코드 리뷰 관점에서 정리하고 공통화 가능 여부 검토'
    ],
    aiToolsTitle: '실제 개발 흐름에 사용한 도구',
    aiTools: ['Cursor', 'Codex', 'Antigravity'],
    contactTitle: '업무 화면의 완성도를 함께 높이고 싶습니다',
    contactText:
      'B2B 업무 시스템, 사내 UI 프레임워크, 그리드 중심 화면 개발 경험을 바탕으로 요구사항을 안정적으로 화면에 반영하는 프론트엔드 개발자가 되겠습니다.',
    contactCards: [
      ['Email', profile.email],
      ['Phone', profile.phone],
      ['Company', profile.companyKo],
      ['Role', 'B2B Frontend / MES UI']
    ],
    contactCtaText: '프로젝트 화면 개발, 사내 UI 프레임워크, MES 업무 화면 관련 경험을 더 자세히 이야기할 수 있습니다.',
    contactMailLabel: '이메일 보내기'
  },
  en: {
    profileName: profile.nameEn,
    company: profile.companyEn,
    tenure: profile.tenureEn,
    heroEyebrow: 'MES · B2B Frontend',
    heroRole: 'B2B Frontend Developer',
    heroText:
      'I build grid, form, popup, and API-connected business screens for manufacturing MES projects while operating internal UI framework guides and training.',
    current: 'Current',
    tenureLabel: 'Tenure',
    emailLabel: 'Email',
    primaryAction: 'View Projects',
    secondaryAction: 'Contact',
    aboutTitle: 'A practical frontend developer',
    aboutKicker: 'Frontend Focus',
    aboutLead: 'Connecting requirements to reliable business screens',
    aboutText:
      'I focus on the flow and completeness of business screens used every day in B2B systems. Along with project screen development, I have improved shared UI development practices through internal framework operations, guides, and training.',
    aboutMetrics: [
      ['6+', 'Implementation and development projects'],
      ['90%+', 'Contribution to internal UI guides'],
      ['About 10', 'Internal and client training sessions']
    ],
    labels: {
      name: 'Name',
      phone: 'Phone',
      position: 'Position',
      department: 'Department',
      education: 'Education',
      techCategory: 'Technical Area',
      company: 'Company',
      tenure: 'Tenure'
    },
    strengths: [
      'Vue 3-based MES and B2B business system development',
      'Internal UI framework and common component operation',
      'AUIGrid-based data screens and dynamic grids',
      'UI Builder and metadata-driven UI improvement',
      'Developer guides, training, and project UI issue support'
    ],
    coreWorksTitle: 'Core Work',
    coreWorks: [
      {
        icon: 'UI',
        title: 'MES Business Screens',
        text: 'Grids, process screens, reports, barcode input UI'
      },
      {
        icon: 'FW',
        title: 'UI Framework',
        text: 'Common components and Core package operation'
      },
      {
        icon: 'BD',
        title: 'UI Builder',
        text: 'Metadata-driven screen builder maintenance'
      },
      {
        icon: 'GD',
        title: 'Guides & Training',
        text: 'VitePress guides, developer training, project support'
      }
    ],
    strengthKicker: 'Core Work',
    strengthTitle: 'Business Screen Development Strengths',
    snapshotTitle: 'Current Focus',
    snapshotName: 'WEBUI 2.0 Internal UI Framework',
    snapshotText:
      'I operate common components, Core packages, UI Builder, and development guides to improve a stable UI development environment across projects.',
    snapshotItems: [
      ['Screens', '90+ MES business screens'],
      ['Builder', '1 year of UI Builder maintenance'],
      ['Guide', 'VitePress development guides'],
      ['Award', '2026 first-half outstanding employee']
    ],
    skillsTitle: 'Tech Stack',
    skillGroups: [
      { title: 'Language', items: ['JavaScript', 'HTML', 'CSS', 'SCSS'] },
      { title: 'Framework', items: ['Vue.js', 'Vite', 'Pinia', 'Vue Router', 'jQuery'] },
      { title: 'UI / Chart', items: ['AUIGrid', 'Element Plus', 'ECharts'] },
      { title: 'Tool', items: ['Node.js', 'Electron.js', 'VitePress', 'Git', 'SVN', 'DBeaver', 'VSCode'] },
      {
        title: 'Database',
        note: 'Used for data checks and basic SELECT queries',
        items: ['MSSQL', 'Oracle', 'PostgreSQL']
      }
    ],
    projectsTitle: 'Representative Projects',
    projectLabels: ['Overview', 'Role', 'Contribution'],
    projectModalLabel: 'View Details',
    closeLabel: 'Close',
    projects: [
      {
        icon: 'framework',
        category: 'Internal Platform',
        status: 'Ongoing',
        name: 'WEBUI 2.0 Internal UI Framework and UI Builder',
        period: 'Sep 2024 ~ Present',
        stack: 'Vue 3, UI Framework, UI Builder, VitePress, Electron.js',
        summary: 'Operate and improve the internal UI framework and UI Builder used for B2B business systems.',
        detail: {
          overview: 'An internal Vue 3-based UI framework and UI Builder project used across B2B business systems.',
          role: [
            'Manage Core package and standard UI project separation',
            'Improve common components and fix framework issues',
            'Maintain UI Builder features and structure',
            'Write VitePress guides and train developers'
          ],
          contribution: [
            'Improved font-size, dark mode, and screen expansion features for large process monitors',
            'Applied keep-alive and menu state restore logic for stable screen transitions',
            'Converted project requirements into reusable framework features',
            'Maintained UI Builder features, tests, and project issue response for about one year'
          ]
        }
      },
      {
        icon: 'manufacturing',
        category: 'Manufacturing MES',
        status: 'Completed',
        name: 'G2 MES Implementation',
        period: 'Jun 2025 ~ Oct 2025',
        stack: 'WEBUI 1.0, JavaScript, AUIGrid, MSSQL, LPS/ZPL',
        summary: 'Built about 40 MES screens including process screens, dynamic grids, barcode input, and label printing integration.',
        detail: {
          overview: 'A manufacturing MES project focused on process screens and high-volume input workflows.',
          role: [
            'Developed about 40 MES business screens',
            'Built dynamic grids based on business conditions',
            'Handled Excel copy/paste bulk input',
            'Analyzed barcode scanning and LPS/ZPL label-printing flows'
          ],
          contribution: [
            'Analyzed missing data issues during rapid barcode input',
            'Improved timing between key events and callback processing',
            'Added loading UI to show processing state',
            'Supported label-printing data flow analysis and UI fixes'
          ]
        }
      },
      {
        icon: 'recycle',
        category: 'MES & Operations',
        status: 'Built & Maintained',
        name: 'Energy Materials MES Implementation and Maintenance',
        period: 'Nov 2023 ~ Aug 2024',
        stack: 'WEBUI 1.0, JavaScript, AUIGrid, MSSQL',
        summary: 'Developed about 30 grid/report screens and handled operational UI issues for about six months.',
        detail: {
          overview: 'A battery recycling MES project where I handled frontend screen development and maintenance.',
          role: [
            'Developed about 30 data management and report screens',
            'Implemented search conditions, combo boxes, popups, and button events',
            'Handled required-field and validation logic before save',
            'Integrated REST APIs and checked MSSQL data'
          ],
          contribution: [
            'Analyzed and fixed UI errors and data display issues during operation',
            'Built AUIGrid search, dynamic columns, save/update/delete flows',
            'Applied common fixes to similar repeated screen issues',
            'Gained hands-on maintenance experience from real user requests'
          ]
        }
      }
    ],
    experienceTitle: 'Project Experience',
    awardLabel: 'Recognition',
    awardTitle: 'Outstanding Employee, First Half of 2026',
    careerSummary:
      'I have contributed to six implementation and development projects while maintaining the internal UI framework and preparing for the next assignment.',
    experienceSubTitle: 'Work Experience',
    experienceCountLabel: 'Projects',
    experienceAction: 'View Work',
    experienceCards: [
      {
        period: 'Aug 2026 ~ Nov 2026 Scheduled',
        company: 'Korean Air MES Project',
        role: 'Developer / Assistant Manager',
        title: 'WEBUI 1.0 JavaScript UI development scheduled',
        summary: 'Scheduled to develop MES business screens in a WEBUI 1.0 environment for aviation manufacturing/operation workflows.',
        bullets: ['JavaScript-based business screen development', 'Grid/form/popup/API-connected UI implementation', 'UI development aligned with project standards']
      },
      {
        period: 'Jun 20, 2025 ~ Oct 31, 2025',
        company: 'LS Electric G2 MES Implementation',
        role: 'Developer / Assistant Manager',
        title: 'MES business screen development and issue resolution',
        summary: 'Delivered about 40 business screens, including process views and high-volume data-entry workflows.',
        bullets: ['Built dynamic grids and Excel copy-and-paste input', 'Analyzed rapid barcode input loss and improved the processing flow', 'Supported LPS/ZPL label-printing integrations']
      },
      {
        period: 'May 22, 2025 ~ Jul 30, 2025',
        company: 'Inox Lithium MES Implementation',
        role: 'Developer / Assistant Manager',
        title: 'Lithium production MES screen development',
        summary: 'Implemented MES screens for data search, entry, and save workflows using WEBUI 1.0 standards.',
        bullets: ['Developed UI with JavaScript and AUIGrid', 'Implemented grid CRUD, form validation, and API integration', 'Checked MSSQL data and resolved project UI issues']
      },
      {
        period: 'Sep 23, 2024 ~ Present',
        company: 'WEBUI 2.0',
        role: 'Developer / Assistant Manager',
        title: 'Vue 3 internal UI framework development and operation',
        summary: 'Maintain the next-generation UI framework, shared components, guides, weekly releases, and UI Builder.',
        bullets: ['Authored over 90% of the UI guide documentation', 'Manage weekly releases and project adoption issues', 'Maintain the Electron.js Builder and delivered about 10 developer training sessions']
      },
      {
        period: 'Jun 17, 2024 ~ Dec 12, 2024',
        company: 'Enertech MES Development',
        role: 'Developer / Staff',
        title: 'Battery MES system UI development',
        summary: 'Developed battery MES screens for the Kaliningrad and Moscow sites in Russia.',
        bullets: ['Developed UI with WEBUI 1.0 and JavaScript', 'Checked PostgreSQL data and integrated APIs', 'Implemented grid, form, and popup-based workflows']
      },
      {
        period: 'May 8, 2024 ~ Jun 5, 2024',
        company: 'Comatech MES Implementation',
        role: 'Developer / Staff',
        title: 'MES business screen development support',
        summary: 'Delivered WEBUI 1.0 screens and feature updates within a short implementation schedule.',
        bullets: ['Developed business UI with JavaScript', 'Checked Oracle data and screen integrations', 'Implemented grid and form features to project standards']
      },
      {
        period: 'Nov 15, 2023 ~ Aug 31, 2024',
        company: 'Energy Materials MES Implementation',
        role: 'Developer / Staff',
        title: 'Battery recycling MES UI development',
        summary: 'Built stable business screens for manufacturing data search, input, and save workflows.',
        bullets: ['100% UI development based on WEBUI 1.0', 'Grid CRUD, validation, and popup handling', 'UI issue and requirement change response']
      }
    ],
    tableHeads: ['Project', 'Period', 'Type', 'Main Role'],
    experience: [
      ['LS ThiraUtech', 'Nov 1, 2023 ~ Present', 'Assistant Manager', 'MES development, FrontEnd: JavaScript/Vue.js, DBMS: Oracle/MSSQL/PostgreSQL'],
      ['Energy Materials MES Implementation', 'Nov 15, 2023 ~ Aug 31, 2024', 'Developer / Staff', 'WEBUI 1.0, JavaScript, MSSQL UI development 100%'],
      ['Comatech MES Implementation', 'May 8, 2024 ~ Jun 5, 2024', 'Developer / Staff', 'WEBUI 1.0, JavaScript, Oracle UI development 100%'],
      ['Enertech MES Development', 'Jun 17, 2024 ~ Dec 12, 2024', 'Developer / Staff', 'WEBUI 1.0, JavaScript, PostgreSQL UI development 100%'],
      ['WEBUI 2.0', 'Sep 23, 2024 ~ Present', 'Developer / Assistant Manager', 'WEBUI 2.0, Vue.js, MSSQL UI development 100%'],
      ['Inox Lithium MES Implementation', 'May 22, 2025 ~ Jul 30, 2025', 'Developer / Assistant Manager', 'WEBUI 1.0, JavaScript, MSSQL UI development 100%'],
      ['LS Electric G2 MES Implementation', 'Jun 20, 2025 ~ Oct 31, 2025', 'Developer / Assistant Manager', 'WEBUI 1.0, JavaScript, MSSQL UI development 100%'],
      ['Korean Air MES Project', 'Aug 2026 ~ Nov 2026 Scheduled', 'Developer / Assistant Manager', 'WEBUI 1.0, JavaScript UI development scheduled']
    ],
    frameworkTitle: 'Internal UI Framework',
    frameworkSubTitle: 'Operating and improving a shared UI development environment',
    frameworkText:
      'I am participating in the development of the Vue.js-based WEBUI 2.0 internal UI framework, standardizing repeated MES screen patterns such as grids, forms, popups, and API integration while handling guides, releases, builder maintenance, training, and project issue response.',
    frameworkStats: [
      ['90%+', 'Contribution to UI guide documentation'],
      ['Weekly', 'Regular internal framework releases'],
      ['Electron', 'Component registration builder management'],
      ['10+', 'Internal/client developer training sessions']
    ],
    frameworkItems: [
      'Develop Vue.js-based WEBUI 2.0 screens and improve the internal UI framework',
      'Standardize common UI patterns around grids, forms, search conditions, popups, and API integration',
      'Create over 90% of UI guide documentation and respond to project adoption inquiries',
      'Manage the Electron.js-based component registration builder and improve usage flows',
      'Handle weekly regular releases and reflect project issues or feature requests',
      'Deliver about 10 internal/client developer training sessions'
    ],
    workflowTitle: 'Using AI as a drafting and verification assistant',
    workflow: [
      'Draft repetitive CRUD screen structures and validation logic with AI-assisted development tools',
      'Adapt generated code to the project-specific internal UI framework',
      'Verify grid events, save/delete flows, exception handling, and user messages directly',
      'Review duplicated logic and evaluate opportunities for commonization'
    ],
    aiToolsTitle: 'Tools used in development workflows',
    aiTools: ['Cursor', 'Codex', 'Antigravity'],
    contactTitle: 'I want to improve the completeness of business screens',
    contactText:
      'With experience in B2B systems, internal UI frameworks, and grid-centered screen development, I aim to reflect requirements reliably in frontend screens.',
    contactCards: [
      ['Email', profile.email],
      ['Phone', profile.phone],
      ['Company', profile.companyEn],
      ['Role', 'B2B Frontend / MES UI']
    ],
    contactCtaText:
      'I can share more detail about project UI development, internal UI frameworks, and MES business screen experience.',
    contactMailLabel: 'Send Email'
  }
}

const copy = computed(() => translations[language.value])

async function setLanguage(nextLanguage) {
  language.value = nextLanguage
  await nextTick()
  document.querySelectorAll('.reveal').forEach((target) => target.classList.add('is-visible'))
}

function updatePointer(event) {
  document.documentElement.style.setProperty('--pointer-x', `${event.clientX}px`)
  document.documentElement.style.setProperty('--pointer-y', `${event.clientY}px`)
}

onMounted(() => {
  window.addEventListener('pointermove', updatePointer)

  const revealTargets = document.querySelectorAll('.reveal')

  if (!window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add('is-visible')
            observer.unobserve(entry.target)
          }
        })
      },
      { threshold: 0.16, rootMargin: '0px 0px -40px 0px' }
    )

    revealTargets.forEach((target) => observer.observe(target))
    return
  }

  revealTargets.forEach((target) => target.classList.add('is-visible'))
})

onUnmounted(() => {
  window.removeEventListener('pointermove', updatePointer)
})
</script>

<template>
  <div class="site-shell" :class="`language-${language}`">
    <header class="site-header">
      <a class="brand" href="#top" aria-label="홈으로 이동">
        <span class="brand-mark">FE</span>
        <span>{{ copy.profileName }}</span>
      </a>
      <div class="header-actions">
        <nav class="nav" aria-label="주요 섹션">
          <a v-for="item in navItems" :key="item.id" :href="`#${item.id}`">
            {{ item.label }}
          </a>
        </nav>
        <div class="language-toggle" aria-label="언어 선택">
          <button :class="{ active: language === 'ko' }" type="button" @click="setLanguage('ko')">
            KO
          </button>
          <button :class="{ active: language === 'en' }" type="button" @click="setLanguage('en')">
            EN
          </button>
        </div>
      </div>
    </header>

    <main id="top">
      <section class="hero section-band mes-surface">
        <div class="hero-copy reveal">
          <p class="eyebrow">{{ copy.heroEyebrow }}</p>
          <h1 class="hero-title">
            <span class="hero-name">{{ copy.profileName }}</span>
            <span class="hero-role">{{ copy.heroRole }}</span>
          </h1>
          <p class="hero-text">{{ copy.heroText }}</p>
          <dl class="hero-profile" aria-label="프로필 요약">
            <div>
              <dt>{{ copy.current }}</dt>
              <dd>{{ copy.company }}</dd>
            </div>
            <div>
              <dt>{{ copy.tenureLabel }}</dt>
              <dd>{{ copy.tenure }}</dd>
            </div>
            <div>
              <dt>{{ copy.emailLabel }}</dt>
              <dd>{{ profile.email }}</dd>
            </div>
          </dl>
          <div class="hero-actions">
            <a class="primary-action" href="#projects">{{ copy.primaryAction }}</a>
            <a class="secondary-action" href="#contact">{{ copy.secondaryAction }}</a>
          </div>
        </div>
      </section>

      <section id="about" class="section">
        <div class="section-heading reveal">
          <p class="eyebrow">About</p>
          <h2>{{ copy.aboutTitle }}</h2>
        </div>
        <div class="about-intro reveal">
          <div class="about-lead-block">
            <span>{{ copy.aboutKicker }}</span>
            <strong>{{ copy.aboutLead }}</strong>
          </div>
          <div class="about-message">
            <p>{{ copy.aboutText }}</p>
          </div>
        </div>
        <div class="about-proof reveal" aria-label="About highlights">
          <div v-for="(item, index) in copy.aboutMetrics" :key="item[0]">
            <component :is="aboutMetricIcons[index]" :size="19" :stroke-width="1.8" aria-hidden="true" />
            <strong>{{ item[0] }}</strong>
            <span>{{ item[1] }}</span>
          </div>
        </div>
        <div class="core-work-section reveal">
          <div class="core-work-head">
            <span>{{ copy.strengthKicker }}</span>
            <strong>{{ copy.coreWorksTitle }}</strong>
          </div>
          <div class="core-work-grid">
            <article v-for="item in copy.coreWorks" :key="item.title" class="core-work-card">
              <span class="work-icon" aria-hidden="true">
                <component :is="workIcons[item.icon]" :size="24" :stroke-width="1.8" />
              </span>
              <h3>{{ item.title }}</h3>
              <p>{{ item.text }}</p>
            </article>
          </div>
        </div>
      </section>

      <section id="skills" class="section muted">
        <div class="section-heading reveal">
          <p class="eyebrow">Skills</p>
          <h2>{{ copy.skillsTitle }}</h2>
        </div>
        <div class="skill-grid">
          <article v-for="group in copy.skillGroups" :key="group.title" class="skill-card reveal">
            <div class="skill-card-head">
              <h3>{{ group.title }}</h3>
              <span>{{ group.items.length }}</span>
            </div>
            <p v-if="group.note" class="note">{{ group.note }}</p>
            <div class="tags">
              <span v-for="item in group.items" :key="item" class="stack-token">
                <img v-if="stackMeta(item).image" :src="stackMeta(item).image" alt="" loading="lazy" />
                <small v-else>{{ stackMeta(item).mark }}</small>
                <span>{{ item }}</span>
              </span>
            </div>
          </article>
        </div>
      </section>

      <section id="projects" class="section">
        <div class="section-heading reveal">
          <p class="eyebrow">Projects</p>
          <h2>{{ copy.projectsTitle }}</h2>
        </div>
        <div class="project-list">
          <article v-for="project in copy.projects" :key="project.name" class="project-card reveal">
            <div class="project-visual">
              <span class="project-icon" aria-hidden="true">
                <component :is="projectIcons[project.icon]" :size="28" :stroke-width="1.7" />
              </span>
              <div>
                <small>{{ project.category }}</small>
                <strong>{{ project.status }}</strong>
              </div>
            </div>
            <div class="project-top">
              <div>
                <h3>{{ project.name }}</h3>
                <p>{{ project.period }}</p>
              </div>
              <span>{{ project.stack }}</span>
            </div>
            <p class="project-summary">{{ project.summary }}</p>
            <button class="project-more" type="button" @click="selectedProject = project">
              <Eye :size="16" :stroke-width="2" aria-hidden="true" />
              {{ copy.projectModalLabel }}
            </button>
          </article>
        </div>
      </section>

      <section id="experience" class="section muted">
        <div class="section-heading reveal">
          <p class="eyebrow">Experience</p>
          <h2>{{ copy.experienceTitle }}</h2>
        </div>
        <div class="career-strip reveal">
          <div class="career-meta">
            <strong>{{ copy.company }}</strong>
            <span>{{ copy.tenure }}</span>
          </div>
          <p>{{ copy.careerSummary }}</p>
          <div class="career-award">
            <Award :size="24" :stroke-width="1.8" aria-hidden="true" />
            <span>
              <small>{{ copy.awardLabel }}</small>
              <strong>{{ copy.awardTitle }}</strong>
            </span>
          </div>
        </div>
        <div class="experience-board reveal">
          <div class="experience-board-head">
            <span>{{ copy.experienceSubTitle }}</span>
            <strong>{{ copy.experienceCards.length }} {{ copy.experienceCountLabel }}</strong>
          </div>
          <article v-for="item in copy.experienceCards" :key="`${item.company}-${item.period}`" class="experience-card reveal">
            <div class="experience-time">
              <span>{{ item.period }}</span>
              <small>{{ item.role }}</small>
            </div>
            <div class="experience-content">
              <p><Building2 :size="16" :stroke-width="1.9" aria-hidden="true" />{{ item.company }}</p>
              <h3>{{ item.title }}</h3>
              <span>{{ item.summary }}</span>
              <details>
                <summary>
                  <ListChecks :size="16" :stroke-width="2" aria-hidden="true" />
                  {{ copy.experienceAction }}
                </summary>
                <ul>
                  <li v-for="bullet in item.bullets" :key="bullet">{{ bullet }}</li>
                </ul>
              </details>
            </div>
          </article>
        </div>
      </section>

      <section id="framework-guide" class="section split-section">
        <div class="section-heading reveal">
          <p class="eyebrow">Framework & Guide</p>
          <h2>{{ copy.frameworkTitle }}</h2>
        </div>
        <div class="framework-stats reveal">
          <div v-for="(stat, index) in copy.frameworkStats" :key="stat[0]">
            <component :is="frameworkIcons[index]" :size="21" :stroke-width="1.8" aria-hidden="true" />
            <strong>{{ stat[0] }}</strong>
            <span>{{ stat[1] }}</span>
          </div>
        </div>
        <div class="feature-panel reveal">
          <div>
            <h3>{{ copy.frameworkSubTitle }}</h3>
            <p>{{ copy.frameworkText }}</p>
          </div>
          <ul class="check-list compact">
            <li v-for="item in copy.frameworkItems" :key="item">{{ item }}</li>
          </ul>
        </div>
      </section>

      <section id="ai-workflow" class="section muted">
        <div class="section-heading reveal">
          <p class="eyebrow">AI-assisted Workflow</p>
          <h2>{{ copy.workflowTitle }}</h2>
        </div>
        <div class="workflow-grid">
          <article v-for="(item, index) in copy.workflow" :key="item" class="workflow-item reveal">
            <span class="workflow-icon" aria-hidden="true">
              <component :is="workflowIcons[index]" :size="23" :stroke-width="1.8" />
            </span>
            <p>{{ item }}</p>
          </article>
        </div>
        <div class="ai-tool-panel reveal">
          <div>
            <span>AI Tools</span>
            <strong>{{ copy.aiToolsTitle }}</strong>
          </div>
          <div class="ai-tool-list">
            <span v-for="tool in copy.aiTools" :key="tool">{{ tool }}</span>
          </div>
        </div>
      </section>

      <section id="contact" class="section contact reveal">
        <div class="contact-layout">
          <div class="contact-copy">
            <p class="eyebrow">Contact</p>
            <h2 class="contact-title">{{ copy.contactTitle }}</h2>
            <p>{{ copy.contactText }}</p>
          </div>
          <div class="contact-panel">
            <div class="contact-grid" aria-label="Contact details">
              <div v-for="item in copy.contactCards" :key="item[0]">
                <span>{{ item[0] }}</span>
                <strong>{{ item[1] }}</strong>
              </div>
            </div>
            <div class="contact-cta">
              <p>{{ copy.contactCtaText }}</p>
              <a class="primary-action contact-mail" :href="`mailto:${profile.email}`">{{ copy.contactMailLabel }}</a>
            </div>
          </div>
        </div>
      </section>
    </main>

    <div
      v-if="selectedProject"
      class="project-modal"
      role="dialog"
      aria-modal="true"
      :aria-label="selectedProject.name"
      @click.self="selectedProject = null"
    >
      <article class="project-modal-card">
        <button class="modal-close" type="button" :aria-label="copy.closeLabel" @click="selectedProject = null">
          ×
        </button>
        <div class="project-modal-head">
          <span>{{ selectedProject.period }}</span>
          <h3>{{ selectedProject.name }}</h3>
          <p>{{ selectedProject.stack }}</p>
        </div>
        <div class="project-modal-body">
          <section>
            <strong>{{ copy.projectLabels[0] }}</strong>
            <p>{{ selectedProject.detail.overview }}</p>
          </section>
          <section>
            <strong>{{ copy.projectLabels[1] }}</strong>
            <ul>
              <li v-for="item in selectedProject.detail.role" :key="item">{{ item }}</li>
            </ul>
          </section>
          <section>
            <strong>{{ copy.projectLabels[2] }}</strong>
            <ul>
              <li v-for="item in selectedProject.detail.contribution" :key="item">{{ item }}</li>
            </ul>
          </section>
        </div>
      </article>
    </div>
  </div>
</template>
