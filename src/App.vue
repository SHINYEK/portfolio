<script setup>
import { computed, nextTick, onMounted, onUnmounted, ref } from 'vue'

const language = ref('ko')

const profile = {
  nameKo: '김신예',
  nameEn: 'Shinye Kim',
  birth: '1996.12.24',
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

const translations = {
  ko: {
    profileName: profile.nameKo,
    company: profile.companyKo,
    tenure: profile.tenureKo,
    heroEyebrow: 'B2B 업무 화면과 MES 프로젝트 경험',
    heroRole: '실무형 B2B 프론트엔드 개발자',
    heroText:
      'MES, POP 등 제조업 중심 프로젝트에서 그리드, 폼, 팝업, 콤보박스, API 연동 기반의 업무 화면을 개발했습니다. 화려함보다 요구사항을 정확하게 화면에 반영하고, 이슈를 끝까지 추적하는 개발 경험을 강점으로 합니다.',
    current: 'Current',
    tenureLabel: 'Tenure',
    emailLabel: 'Email',
    primaryAction: '대표 프로젝트 보기',
    secondaryAction: '연락하기',
    aboutTitle: '프레임워크 환경에 맞춰 업무 화면을 완성하는 개발자',
    aboutText:
      'Vue.js와 JavaScript 기반의 B2B 업무 시스템 프론트엔드 개발 경험을 보유하고 있습니다. 제조업 중심 프로젝트에서 데이터 조회, 저장, 삭제, 유효성 검사, 팝업, 콤보박스, API 연동 흐름을 구현해 왔습니다.',
    labels: {
      name: '이름',
      birth: '생년월일',
      phone: '연락처',
      position: '직위',
      department: '부서',
      education: '최종학력',
      techCategory: '기술구분',
      company: '재직 회사',
      tenure: '재직 기간'
    },
    strengths: [
      'Vue.js / JavaScript 기반 업무 화면 개발',
      'MES, POP 등 제조업 중심 B2B 시스템 경험',
      '그리드 중심 CRUD, 유효성 검사, 팝업, 콤보박스 처리',
      '자체 UI 프레임워크 구조에 맞춘 화면 개발',
      '프로젝트 이슈 대응 및 기능 개선'
    ],
    skillsTitle: '업무 화면 개발에 필요한 기술을 목적별로 사용합니다',
    skillGroups: [
      { title: 'Frontend', items: ['HTML', 'CSS', 'JavaScript', 'jQuery', 'Vue.js'] },
      {
        title: 'UI Library / Component',
        items: ['AUIGrid', 'Element Plus', 'Tabulator', 'ECharts', 'jqxSplitter', 'jqxComboBox']
      },
      { title: 'Runtime / Tool', items: ['Node.js', 'Electron.js', '사내 npm 패키지 관리'] },
      {
        title: 'Database',
        note: '데이터 확인 및 기본 조회 쿼리 작성 용도',
        items: ['MSSQL', 'Oracle', 'PostgreSQL']
      },
      {
        title: 'Currently Learning',
        items: ['TypeScript', 'Flutter', 'Java / Spring', 'API / HTTP 기본 구조']
      },
      {
        title: 'Certification',
        items: ['SQLD (2023.04.14)', '컴퓨터활용능력 1급 (2022.05.13)', '정보처리기사 (2026.09.11 취득 예정)']
      }
    ],
    projectsTitle: '문제, 역할, 해결, 성과 중심의 대표 프로젝트',
    projectLabels: ['문제', '역할', '해결', '성과'],
    projects: [
      {
        name: '에너지머티리얼즈 MES 구축',
        period: '2023.11.15 ~ 2024.08.31',
        stack: 'WEBUI 1.0, JavaScript, MSSQL, Git, DBeaver, VSCode',
        problem: '배터리 재활용 MES 구축 과정에서 현장 데이터 조회, 입력, 저장 흐름을 안정적인 업무 화면으로 구현해야 했습니다.',
        role: '개발 / 사원으로 참여해 UI 개발을 100% 담당했습니다.',
        solution: 'WEBUI 1.0 기반으로 그리드, 폼, 팝업, 검색 조건, 저장 전 유효성 검사, API 연동 화면을 구현했습니다.',
        result: '제조 현장 업무 흐름에 맞는 MES 화면을 구축하고, 프로젝트 기간 동안 화면 이슈와 변경 요청에 대응했습니다.'
      },
      {
        name: 'LS Electric G2 MES 구축',
        period: '2025.06.20 ~ 2025.10.31',
        stack: 'WEBUI 1.0, JavaScript, MSSQL, Git, DBeaver, VSCode',
        problem: 'LS Electric G2 MES 구축에서 프로젝트 표준과 업무 요구사항을 동시에 만족하는 화면 개발이 필요했습니다.',
        role: '개발 / 주임으로 참여해 UI 개발을 100% 담당했습니다.',
        solution: '조회 조건, 그리드, 폼, 사용자 메시지, API 연동 흐름을 WEBUI 1.0 기준에 맞춰 구현했습니다.',
        result: 'MES 업무 화면의 일관된 개발 패턴을 유지하면서 기능 수정과 화면 개선 요청에 대응했습니다.'
      },
      {
        name: 'WEBUI 2.0 사내 UI 프레임워크 개발',
        period: '2024.09.23 ~ 현재',
        stack: 'WEBUI 2.0, Vue.js, MSSQL, Git, VSCode',
        problem: '프로젝트별로 반복되는 MES 화면 개발 패턴을 표준화하고, 내부 개발자가 일관된 방식으로 화면을 구현할 수 있는 차세대 UI 프레임워크가 필요했습니다.',
        role: '개발 / 주임으로 참여해 Vue.js 기반 사내 UI 프레임워크 화면 개발, 공통 컴포넌트 사용 흐름 정리, 개발 가이드 및 문의 대응을 수행하고 있습니다.',
        solution: '그리드, 폼, 검색 조건, 팝업, API 연동 등 B2B 업무 화면에서 반복되는 UI 패턴을 프레임워크 구조에 맞게 정리하고, 프로젝트 적용 시 발생하는 이슈와 개선 요청을 반영했습니다.',
        result: '실제 MES 프로젝트 경험을 바탕으로 사내 UI 프레임워크의 사용성과 화면 개발 생산성을 높이는 데 기여하고 있으며, 현재도 최신 업무로 지속 수행 중입니다.'
      }
    ],
    experienceTitle: '프로젝트 참여 이력',
    careerSummary: 'B2B 업무 시스템 화면 개발과 사내 UI 프레임워크 운영, 가이드, 교육 지원을 함께 수행하고 있습니다.',
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
    frameworkTitle: '사내 UI 프레임워크 운영과 교육 경험',
    frameworkSubTitle: '공통된 개발 방식을 만드는 경험',
    frameworkText:
      'Vue.js 기반 WEBUI 2.0 사내 UI 프레임워크 개발에 참여하고 있으며, MES 프로젝트에서 반복되는 그리드, 폼, 팝업, API 연동 화면 패턴을 공통화하고 내부 개발자가 일관된 방식으로 사용할 수 있도록 가이드와 이슈 대응을 수행하고 있습니다.',
    frameworkItems: [
      'Vue.js 기반 WEBUI 2.0 화면 개발 및 사내 UI 프레임워크 개선',
      '그리드, 폼, 검색 조건, 팝업, API 연동 중심의 공통 화면 패턴 정리',
      'UI 개발 가이드 문서 작성 및 프로젝트 적용 문의 대응',
      '컴포넌트 사용 흐름, 등록 구조, 반복 개발 패턴 개선',
      '프로젝트별 이슈, 추가 기능 요청, 프레임워크 개선 사항 검토 및 반영'
    ],
    workflowTitle: 'AI를 초안 작성과 검증 보조 도구로 활용합니다',
    workflow: [
      '반복적인 CRUD 화면 구조와 유효성 검사 코드의 초안을 AI 개발 보조 도구로 빠르게 작성',
      '생성된 코드를 프로젝트 자체 UI 프레임워크 구조에 맞게 직접 수정',
      '그리드 이벤트, 저장/삭제 흐름, 예외 처리, 사용자 메시지를 직접 검증 후 반영',
      '중복 로직을 코드 리뷰 관점에서 정리하고 공통화 가능 여부 검토'
    ],
    contactTitle: '업무 화면의 완성도를 함께 높이고 싶습니다',
    contactText:
      'B2B 업무 시스템, 사내 UI 프레임워크, 그리드 중심 화면 개발 경험을 바탕으로 요구사항을 안정적으로 화면에 반영하는 프론트엔드 개발자가 되겠습니다.'
  },
  en: {
    profileName: profile.nameEn,
    company: profile.companyEn,
    tenure: profile.tenureEn,
    heroEyebrow: 'B2B Business Screens and MES Project Experience',
    heroRole: 'Practical B2B Frontend Developer',
    heroText:
      'I build enterprise work screens for manufacturing-centered MES and POP projects, focusing on grids, forms, popups, combo boxes, validation, and API integration. My strength is translating requirements into stable UI behavior within real project constraints.',
    current: 'Current',
    tenureLabel: 'Tenure',
    emailLabel: 'Email',
    primaryAction: 'View Projects',
    secondaryAction: 'Contact',
    aboutTitle: 'A developer who completes business screens within framework constraints',
    aboutText:
      'I have frontend development experience with Vue.js and JavaScript for B2B enterprise systems. In manufacturing projects, I implemented data search, save, delete, validation, popup, combo box, and API integration workflows.',
    labels: {
      name: 'Name',
      birth: 'Birth Date',
      phone: 'Phone',
      position: 'Position',
      department: 'Department',
      education: 'Education',
      techCategory: 'Technical Area',
      company: 'Company',
      tenure: 'Tenure'
    },
    strengths: [
      'Business screen development with Vue.js / JavaScript',
      'MES, POP, and manufacturing-centered B2B system experience',
      'Grid-based CRUD, validation, popup, and combo box handling',
      'Screen development aligned with an internal UI framework',
      'Project issue response and feature improvement'
    ],
    skillsTitle: 'I use technologies by purpose for enterprise UI development',
    skillGroups: [
      { title: 'Frontend', items: ['HTML', 'CSS', 'JavaScript', 'jQuery', 'Vue.js'] },
      {
        title: 'UI Library / Component',
        items: ['AUIGrid', 'Element Plus', 'Tabulator', 'ECharts', 'jqxSplitter', 'jqxComboBox']
      },
      { title: 'Runtime / Tool', items: ['Node.js', 'Electron.js', 'Internal npm package management'] },
      {
        title: 'Database',
        note: 'Used for data checks and basic SELECT queries',
        items: ['MSSQL', 'Oracle', 'PostgreSQL']
      },
      {
        title: 'Currently Learning',
        items: ['TypeScript', 'Flutter', 'Java / Spring', 'API / HTTP basics']
      },
      {
        title: 'Certification',
        items: ['SQLD (Apr 14, 2023)', 'Computer Specialist in Spreadsheet & Database Level 1 (May 13, 2022)', 'Engineer Information Processing (Expected Sep 11, 2026)']
      }
    ],
    projectsTitle: 'Selected projects structured by problem, role, solution, and impact',
    projectLabels: ['Problem', 'Role', 'Solution', 'Impact'],
    projects: [
      {
        name: 'Energy Materials MES Implementation',
        period: 'Nov 15, 2023 ~ Aug 31, 2024',
        stack: 'WEBUI 1.0, JavaScript, MSSQL, Git, DBeaver, VSCode',
        problem: 'The battery recycling MES project required stable UI screens for manufacturing data search, input, and save workflows.',
        role: 'Participated as developer / staff and handled 100% of UI development.',
        solution: 'Implemented grids, forms, popups, search conditions, pre-save validation, and API-connected screens based on WEBUI 1.0.',
        result: 'Delivered MES screens aligned with manufacturing workflows and responded to UI issues and requirement changes during the project.'
      },
      {
        name: 'LS Electric G2 MES Implementation',
        period: 'Jun 20, 2025 ~ Oct 31, 2025',
        stack: 'WEBUI 1.0, JavaScript, MSSQL, Git, DBeaver, VSCode',
        problem: 'The LS Electric G2 MES project required UI screens that satisfied both project standards and business requirements.',
        role: 'Participated as developer / assistant manager and handled 100% of UI development.',
        solution: 'Implemented search conditions, grids, forms, user messages, and API integration flows according to WEBUI 1.0 standards.',
        result: 'Maintained consistent MES screen development patterns while responding to feature changes and screen improvement requests.'
      },
      {
        name: 'WEBUI 2.0 Internal UI Framework',
        period: 'Sep 23, 2024 ~ Present',
        stack: 'WEBUI 2.0, Vue.js, MSSQL, Git, VSCode',
        problem: 'Repeated MES screen development patterns needed to be standardized so internal developers could build screens consistently across projects.',
        role: 'Participating as developer / assistant manager, working on Vue.js-based internal UI framework screens, common component usage flows, development guides, and project inquiries.',
        solution: 'Structured repeated B2B UI patterns such as grids, forms, search conditions, popups, and API integration around the framework architecture, then reflected project issues and improvement requests.',
        result: 'Contributing to better usability and productivity of the internal UI framework based on real MES project experience. This is the latest ongoing work.'
      }
    ],
    experienceTitle: 'Project Experience',
    careerSummary:
      'I work on B2B business system screens while supporting internal UI framework operation, guides, and developer training.',
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
    frameworkTitle: 'Internal UI Framework, Guide, and Training',
    frameworkSubTitle: 'Creating a shared way to build screens',
    frameworkText:
      'I am participating in the development of the Vue.js-based WEBUI 2.0 internal UI framework, standardizing repeated MES screen patterns such as grids, forms, popups, and API integration so internal developers can use them consistently across projects.',
    frameworkItems: [
      'Develop Vue.js-based WEBUI 2.0 screens and improve the internal UI framework',
      'Standardize common UI patterns around grids, forms, search conditions, popups, and API integration',
      'Write UI development guides and respond to project application inquiries',
      'Improve component usage flows, registration structure, and repeated screen development patterns',
      'Review and reflect project issues, feature requests, and framework improvement items'
    ],
    workflowTitle: 'Using AI as a drafting and verification assistant',
    workflow: [
      'Draft repetitive CRUD screen structures and validation logic with AI-assisted development tools',
      'Adapt generated code to the project-specific internal UI framework',
      'Verify grid events, save/delete flows, exception handling, and user messages directly',
      'Review duplicated logic and evaluate opportunities for commonization'
    ],
    contactTitle: 'I want to improve the completeness of business screens',
    contactText:
      'With experience in B2B systems, internal UI frameworks, and grid-centered screen development, I aim to reflect requirements reliably in frontend screens.'
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
          <div class="mes-status-board" aria-label="MES process status">
            <span>MES</span>
            <span>LOT TRACKING</span>
            <span>GRID CRUD</span>
            <span>API SYNC</span>
          </div>
          <div class="hero-actions">
            <a class="primary-action" href="#projects">{{ copy.primaryAction }}</a>
            <a class="secondary-action" href="#contact">{{ copy.secondaryAction }}</a>
          </div>
        </div>
        <figure class="hero-visual reveal">
          <img src="/b2b-dashboard-hero.png" alt="B2B 업무 시스템 대시보드 목업" />
        </figure>
      </section>

      <section id="about" class="section">
        <div class="section-heading reveal">
          <p class="eyebrow">About</p>
          <h2>{{ copy.aboutTitle }}</h2>
        </div>
        <div class="about-layout">
          <div class="about-copy reveal">
            <p>{{ copy.aboutText }}</p>
            <dl class="profile-list">
              <div><dt>{{ copy.labels.name }}</dt><dd>{{ copy.profileName }}</dd></div>
              <div><dt>{{ copy.labels.birth }}</dt><dd>{{ profile.birth }}</dd></div>
              <div><dt>{{ copy.labels.phone }}</dt><dd>{{ profile.phone }}</dd></div>
              <div><dt>{{ copy.labels.position }}</dt><dd>{{ language === 'ko' ? profile.positionKo : profile.positionEn }}</dd></div>
              <div><dt>{{ copy.labels.department }}</dt><dd>{{ language === 'ko' ? profile.departmentKo : profile.departmentEn }}</dd></div>
              <div><dt>{{ copy.labels.education }}</dt><dd>{{ language === 'ko' ? profile.educationKo : profile.educationEn }}</dd></div>
              <div><dt>{{ copy.labels.techCategory }}</dt><dd>{{ language === 'ko' ? profile.techCategoryKo : profile.techCategoryEn }}</dd></div>
              <div><dt>{{ copy.labels.company }}</dt><dd>{{ copy.company }}</dd></div>
              <div><dt>{{ copy.labels.tenure }}</dt><dd>{{ copy.tenure }}</dd></div>
            </dl>
          </div>
          <figure class="about-portrait reveal">
            <div class="portrait-frame">
              <img src="/about-developer-placeholder.png" :alt="`${copy.profileName} developer placeholder`" />
            </div>
            <figcaption class="portrait-meta">
              <strong>{{ copy.profileName }}</strong>
              <span>Frontend Developer</span>
              <small>MES · B2B System · Vue.js</small>
            </figcaption>
          </figure>
        </div>
        <div class="strength-panel reveal">
          <div class="strength-panel-head">
            <span>Core Work Patterns</span>
            <strong>업무 화면 개발 강점</strong>
          </div>
          <ul class="check-list strength-list">
            <li v-for="(item, index) in copy.strengths" :key="item" class="reveal">
              <span class="strength-index">{{ String(index + 1).padStart(2, '0') }}</span>
              <span>{{ item }}</span>
            </li>
          </ul>
        </div>
      </section>

      <section id="skills" class="section muted">
        <div class="section-heading reveal">
          <p class="eyebrow">Skills</p>
          <h2>{{ copy.skillsTitle }}</h2>
        </div>
        <div class="skill-grid">
          <article v-for="group in copy.skillGroups" :key="group.title" class="skill-card reveal">
            <h3>{{ group.title }}</h3>
            <p v-if="group.note" class="note">{{ group.note }}</p>
            <div class="tags">
              <span v-for="item in group.items" :key="item">{{ item }}</span>
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
            <div class="project-top">
              <div>
                <h3>{{ project.name }}</h3>
                <p>{{ project.period }}</p>
              </div>
              <span>{{ project.stack }}</span>
            </div>
            <div class="project-detail">
              <div><strong>{{ copy.projectLabels[0] }}</strong><p>{{ project.problem }}</p></div>
              <div><strong>{{ copy.projectLabels[1] }}</strong><p>{{ project.role }}</p></div>
              <div><strong>{{ copy.projectLabels[2] }}</strong><p>{{ project.solution }}</p></div>
              <div><strong>{{ copy.projectLabels[3] }}</strong><p>{{ project.result }}</p></div>
            </div>
          </article>
        </div>
      </section>

      <section id="experience" class="section muted">
        <div class="section-heading reveal">
          <p class="eyebrow">Experience</p>
          <h2>{{ copy.experienceTitle }}</h2>
        </div>
        <div class="career-strip reveal">
          <strong>{{ copy.company }}</strong>
          <span>{{ copy.tenure }}</span>
          <p>{{ copy.careerSummary }}</p>
        </div>
        <div class="table-wrap reveal" role="region" aria-label="프로젝트 참여 이력 표">
          <table>
            <thead>
              <tr>
                <th v-for="head in copy.tableHeads" :key="head">{{ head }}</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="row in copy.experience" :key="row[0]">
                <td v-for="cell in row" :key="cell">{{ cell }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </section>

      <section id="framework-guide" class="section split-section">
        <div class="section-heading reveal">
          <p class="eyebrow">Framework & Guide</p>
          <h2>{{ copy.frameworkTitle }}</h2>
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
            <span>{{ String(index + 1).padStart(2, '0') }}</span>
            <p>{{ item }}</p>
          </article>
        </div>
      </section>

      <section id="contact" class="section contact reveal">
        <div class="section-heading">
          <p class="eyebrow">Contact</p>
          <h2 class="contact-title">{{ copy.contactTitle }}</h2>
        </div>
        <p>{{ copy.contactText }}</p>
        <a class="primary-action" :href="`mailto:${profile.email}`">{{ profile.email }}</a>
      </section>
    </main>
  </div>
</template>
