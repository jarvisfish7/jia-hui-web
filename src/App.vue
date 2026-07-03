<script setup>
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'

const lang = ref('zh')
const activeSlide = ref(0)

const copy = {
  zh: {
    nav: ['首页', '业务', '痛点', '案例', '流程', '联系'],
    cta: '发起合作',
    heroEyebrow: 'GUANGZHOU JIA HUI ENTERPRISE MANAGEMENT CO., LTD.',
    heroTitle: ['灵活用工', '现场服务解决方案'],
    heroText:
      '为物业、安保、餐饮、活动和短期项目提供批量招聘、岗位外包、现场派遣与合规结算支持。',
    heroPrimary: '立即咨询',
    heroSecondary: '获取服务方案',
    heroStats: [
      { value: '按需', label: '增减人员' },
      { value: '批量', label: '快速补位' },
      { value: '合规', label: '服务结算' },
    ],
    heroCapabilities: ['劳务派遣', '岗位外包', '批量招聘', '现场管理', '服务费发票'],
    heroFlow: ['需求沟通', '岗位匹配', '人员到岗', '现场跟进'],
    floatCardTitle: '项目协同',
    floatCardText: '从用工配置到现场落地，保持交付稳定与响应速度。',
    heroImage: '/images/hero-impact.png',
    servicesTitle: '核心业务能力',
    servicesText: '以管理、人才与执行三条线，形成更完整的服务链路。',
    services: [
      {
        id: '01',
        icon: '企',
        tag: '管理支持',
        title: '企业管理咨询',
        desc: '组织运营、财税协同、礼仪会展与企业形象支持。',
        action: '了解服务',
      },
      {
        id: '02',
        icon: '招',
        tag: '快速补位',
        title: '人力资源服务',
        desc: '招聘配置、项目补位、劳务服务与职业中介协同。',
        action: '了解服务',
      },
      {
        id: '03',
        icon: '派',
        tag: '现场执行',
        title: '劳务派遣外包',
        desc: '保安、服务员、保洁员等多岗位全国范围输出。',
        action: '了解服务',
      },
    ],
    painTitle: '解决痛点',
    painText: '从编制、招聘、现场到结算逐项拆解企业用工压力，给出可落地的服务方案。',
    pains: [
      {
        id: '01',
        problem: '用工编制、人员名额受限',
        solution: '灵活用工与岗位外包',
        text: '派遣不占用本单位编制，快速补充人手。',
      },
      {
        id: '02',
        problem: '季节性、阶段性用工波动',
        solution: '按项目周期增减人员',
        text: '演唱会、电商大促、展会、项目短期攻坚、生产线旺季，可按需增减人员。',
      },
      {
        id: '03',
        problem: '招聘周期长、人员流动大',
        solution: '标准化招聘与储备机制',
        text: '快速批量招人，缩短招聘周期，解决紧急缺人。',
      },
      {
        id: '04',
        problem: '社保、工伤、劳动纠纷压力',
        solution: '劳动关系与合同规范管理',
        text: '企业只负责岗位管理和工作安排，降低合规监管压力。',
      },
      {
        id: '05',
        problem: '人力成本高、财务结构不灵活',
        solution: '人力成本结构优化',
        text: '费用可统一开具服务费发票，财务入账更灵活。',
      },
    ],
    quickTitle: '把临时用工压力转化为可控交付',
    quickWins: [
      '批量招聘与岗位储备同步推进，提升紧急补位效率。',
      '按项目周期灵活配置人员，淡旺季和短期任务都能收放有序。',
      '规范劳动关系、合同和服务流程，降低合规管理压力。',
      '不增加正式编制负担，匹配企业阶段性人力预算。',
      '统一服务结算与票据管理，让人力成本更清晰可控。',
    ],
    showcaseTitle: '专业能力',
    showcaseText: '以真实服务场景呈现佳汇在招聘组织、岗位派驻、现场管理与合规结算上的交付能力。',
    slides: [
      {
        tag: '批量招人',
        title: '快速补齐项目现场的人手缺口',
        text: '适配演唱会、展会、电商大促、生产旺季等短周期集中用工。',
        bullets: ['快速补位', '按需增减', '缩短周期'],
        metrics: [
          { value: '批量', label: '岗位补位' },
          { value: '短期', label: '项目承接' },
          { value: '按需', label: '人员增减' },
        ],
        image:
          '/images/hero-enterprise.png',
      },
      {
        tag: '现场服务',
        title: '保安、服务员、保洁员等岗位外派',
        text: '围绕物业、餐饮、安保、后勤场景组织人员到岗和现场管理。',
        bullets: ['岗位外派', '班次调度', '现场跟进'],
        metrics: [
          { value: '多岗', label: '现场派驻' },
          { value: '班次', label: '协同排班' },
          { value: '跟进', label: '现场管理' },
        ],
        image:
          '/images/service-hospitality.png',
      },
      {
        tag: '合规协同',
        title: '从招聘到结算的一体化服务协同',
        text: '协助企业降低人事流程、劳动合规、财务结算和长期编制压力。',
        bullets: ['合规支持', '服务费发票', '成本优化'],
        metrics: [
          { value: '合规', label: '流程支持' },
          { value: '发票', label: '统一结算' },
          { value: '减负', label: '行政支出' },
        ],
        image:
          '/images/service-property.png',
      },
    ],
    galleryTitle: '服务能力展示',
    galleryText: '围绕企业用工全过程，清晰呈现招聘配置、现场派驻、物业后勤与结算支持能力。',
    gallery: [
      {
        title: '批量招聘',
        text: '短时间组织岗位筛选、面试、到岗与补位。',
        image:
          '/images/gallery-recruitment.png',
      },
      {
        title: '现场派遣',
        text: '保安、服务员、保洁员等岗位按项目节奏派驻。',
        image:
          '/images/hero-minimal.png',
      },
      {
        title: '物业后勤',
        text: '覆盖园区、商业、餐饮、物业类场景的日常支撑。',
        image:
          '/images/gallery-property-support.png',
      },
      {
        title: '合规结算',
        text: '统一服务费发票，减少企业人事行政配套支出。',
        image:
          '/images/gallery-compliance.png',
      },
    ],
    processTitle: '服务流程',
    processText: '从需求到结算拆成清晰节点，让短期项目和长期外包都能稳妥推进。',
    processSteps: [
      { id: '01', title: '需求诊断', text: '确认岗位、人数、班次、到岗时间和现场管理边界。' },
      { id: '02', title: '招聘匹配', text: '按岗位画像组织筛选、面试、储备和替补机制。' },
      { id: '03', title: '派驻执行', text: '人员到岗、班次调度、现场反馈和异常补位同步推进。' },
      { id: '04', title: '合规结算', text: '服务过程留痕，统一服务费发票，便于财务入账。' },
    ],
    partnersTitle: '合作单位',
    partners: ['广州珠江物业', '深圳新大正物业', '北京京城保安', '广州摩打食堂'],
    partnersText: '覆盖物业、安保、餐饮与现场服务客户，适合高频、阶段性和批量岗位需求。',
    partnerBadge: '合作客户',
    contactTitle: '联系方式',
    contactText: 'Kevin 18033390585',
    contactButton: '立即联系 Kevin',
  },
  en: {
    nav: ['Home', 'Services', 'Pain Points', 'Cases', 'Process', 'Contact'],
    cta: 'Get a Plan',
    heroEyebrow: 'GUANGZHOU JIA HUI ENTERPRISE MANAGEMENT CO., LTD.',
    heroTitle: ['Flexible staffing', 'and field service solutions'],
    heroText:
      'Bulk recruitment, role outsourcing, on-site dispatch and compliant settlement for property, security, catering, events and short-term projects.',
    heroPrimary: 'Talk to Kevin',
    heroSecondary: 'Get Service Plan',
    heroStats: [
      { value: 'On-demand', label: 'Headcount' },
      { value: 'Bulk', label: 'Fast fill' },
      { value: 'Compliant', label: 'Settlement' },
    ],
    heroCapabilities: ['Labor dispatch', 'Role outsourcing', 'Bulk hiring', 'Field management', 'Service invoice'],
    heroFlow: ['Brief', 'Match', 'Deploy', 'Follow-up'],
    floatCardTitle: 'Delivery Rhythm',
    floatCardText: 'From workforce setup to on-site execution, focused on speed and stability.',
    heroImage: '/images/hero-impact.png',
    servicesTitle: 'Core Capabilities',
    servicesText: 'Management, staffing and field execution combined into one service chain.',
    services: [
      {
        id: '01',
        icon: '企',
        tag: 'Management',
        title: 'Enterprise Consulting',
        desc: 'Operations, finance coordination, events and corporate image support.',
        action: 'Learn more',
      },
      {
        id: '02',
        icon: '招',
        tag: 'Fast fill',
        title: 'HR Services',
        desc: 'Recruitment, flexible staffing, labor services and talent coordination.',
        action: 'Learn more',
      },
      {
        id: '03',
        icon: '派',
        tag: 'Field delivery',
        title: 'Dispatch & Outsourcing',
        desc: 'Security, waitstaff and cleaning teams deployed at national scale.',
        action: 'Learn more',
      },
    ],
    painTitle: 'Pain Points Solved',
    painText: 'Workforce pressure is broken down across headcount, hiring, field delivery and settlement, then matched with practical service responses.',
    pains: [
      {
        id: '01',
        problem: 'Headcount and staffing limits',
        solution: 'Flexible staffing and role outsourcing',
        text: 'Dispatched workers do not occupy internal headcount and can fill gaps quickly.',
      },
      {
        id: '02',
        problem: 'Seasonal and project-based workforce swings',
        solution: 'Scale teams by project cycle',
        text: 'Concerts, ecommerce campaigns, expos, project sprints and production peaks can scale up or down on demand.',
      },
      {
        id: '03',
        problem: 'Long hiring cycles and staff turnover',
        solution: 'Standardized recruiting and reserve pool',
        text: 'Bulk hiring shortens recruitment cycles and helps solve urgent vacancies.',
      },
      {
        id: '04',
        problem: 'Social insurance, injury and labor dispute pressure',
        solution: 'Standard labor relationship and contract management',
        text: 'Businesses manage roles and work arrangements while service support reduces compliance pressure.',
      },
      {
        id: '05',
        problem: 'High labor cost and rigid finance structure',
        solution: 'Workforce cost structure optimization',
        text: 'Service fees can be invoiced uniformly for more flexible accounting.',
      },
    ],
    quickTitle: 'Turn temporary staffing pressure into controlled delivery',
    quickWins: [
      'Run bulk recruitment and reserve pools together for faster urgent fill.',
      'Scale teams by project cycle so peaks and short-term tasks stay controlled.',
      'Standardize labor relationships, contracts and service workflows to reduce compliance pressure.',
      'Support staged workforce budgets without expanding permanent headcount.',
      'Unify service settlement and invoices so labor costs stay visible.',
    ],
    showcaseTitle: 'Professional Capabilities',
    showcaseText: 'Real service scenes highlight delivery strength across recruiting, deployment, field management and compliant settlement.',
    slides: [
      {
        tag: 'Bulk Hiring',
        title: 'Quickly close on-site workforce gaps',
        text: 'Built for concerts, expos, ecommerce campaigns, production peaks and short-cycle staffing spikes.',
        bullets: ['Fast fill', 'Scale on demand', 'Shorter cycles'],
        metrics: [
          { value: 'Bulk', label: 'Role fill' },
          { value: 'Short', label: 'Project cycle' },
          { value: 'Agile', label: 'Headcount' },
        ],
        image:
          '/images/hero-enterprise.png',
      },
      {
        tag: 'Field Service',
        title: 'On-site dispatch for security, service and cleaning roles',
        text: 'Staffing support for property, catering, security and backend service scenes.',
        bullets: ['Role dispatch', 'Shift scheduling', 'Field follow-up'],
        metrics: [
          { value: 'Multi-role', label: 'Deployment' },
          { value: 'Shift', label: 'Scheduling' },
          { value: 'On-site', label: 'Follow-up' },
        ],
        image:
          '/images/service-hospitality.png',
      },
      {
        tag: 'Compliance',
        title: 'Integrated support from hiring to settlement',
        text: 'Helps reduce HR workflow, labor compliance, financial settlement and permanent headcount pressure.',
        bullets: ['Compliance', 'Service invoice', 'Cost control'],
        metrics: [
          { value: 'Comply', label: 'Process' },
          { value: 'Invoice', label: 'Settlement' },
          { value: 'Relief', label: 'Admin cost' },
        ],
        image:
          '/images/service-property.png',
      },
    ],
    galleryTitle: 'Service Capability Display',
    galleryText: 'A clear view of recruitment, dispatch, property support and settlement capabilities across the workforce lifecycle.',
    gallery: [
      {
        title: 'Bulk Recruitment',
        text: 'Screening, interviews, onboarding and replacement at speed.',
        image:
          '/images/gallery-recruitment.png',
      },
      {
        title: 'On-site Dispatch',
        text: 'Security, waitstaff and cleaning roles deployed by project rhythm.',
        image:
          '/images/hero-minimal.png',
      },
      {
        title: 'Property Support',
        text: 'Everyday support for parks, business sites, catering and property scenes.',
        image:
          '/images/gallery-property-support.png',
      },
      {
        title: 'Compliant Settlement',
        text: 'Unified service-fee invoicing reduces HR and admin support spend.',
        image:
          '/images/gallery-compliance.png',
      },
    ],
    processTitle: 'Service Process',
    processText: 'A clear path from requirement diagnosis to compliant settlement keeps short-term and long-term work predictable.',
    processSteps: [
      { id: '01', title: 'Diagnose', text: 'Confirm roles, headcount, shifts, arrival time and field-management boundary.' },
      { id: '02', title: 'Match', text: 'Recruit, screen, interview and prepare backup staff by role profile.' },
      { id: '03', title: 'Deploy', text: 'Coordinate arrival, shifts, feedback and replacement in the field.' },
      { id: '04', title: 'Settle', text: 'Keep service records and issue service-fee invoices for accounting.' },
    ],
    partnersTitle: 'Selected Partners',
    partners: ['Guangzhou Pearl River Property', 'Shenzhen Xindazheng Property', 'Beijing Jingcheng Security', 'Guangzhou Moda Canteen'],
    partnersText: 'Trusted across property, security, catering and field-service scenarios with high-frequency and short-cycle workforce needs.',
    partnerBadge: 'Verified partner',
    contactTitle: 'Contact',
    contactText: 'Kevin 18033390585',
    contactButton: 'Call Kevin',
  },
}

const current = computed(() => copy[lang.value])
const partnerLoop = computed(() => [...current.value.partners, ...current.value.partners])

const heroBackgroundStyle = computed(() => ({
  '--hero-image': `url(${current.value.heroImage})`,
}))

const trackStyle = computed(() => ({
  transform: `translateX(-${activeSlide.value * 100}%)`,
}))

let timer

const startAutoplay = () => {
  stopAutoplay()
  timer = window.setInterval(() => {
    activeSlide.value = (activeSlide.value + 1) % current.value.slides.length
  }, 4200)
}

const stopAutoplay = () => {
  if (timer) {
    window.clearInterval(timer)
    timer = null
  }
}

const setLang = (nextLang) => {
  lang.value = nextLang
  activeSlide.value = 0
  startAutoplay()
}

const goToSlide = (index) => {
  activeSlide.value = index
  startAutoplay()
}

const nextSlide = () => {
  activeSlide.value = (activeSlide.value + 1) % current.value.slides.length
  startAutoplay()
}

onMounted(() => {
  startAutoplay()
})

onBeforeUnmount(() => {
  stopAutoplay()
})
</script>

<template>
  <div class="page-shell">
    <div class="texture-layer"></div>
    <div class="glow glow-a"></div>
    <div class="glow glow-b"></div>

    <header class="site-header">
      <a class="brand" href="#top">
        <span class="brand-badge"></span>
        <div>
          <strong>佳汇企业管理</strong>
          <span>JIA HUI</span>
        </div>
      </a>

      <nav class="top-nav">
        <a href="#top">{{ current.nav[0] }}</a>
        <a href="#services">{{ current.nav[1] }}</a>
        <a href="#pain-points">{{ current.nav[2] }}</a>
        <a href="#showcase">{{ current.nav[3] }}</a>
        <a href="#process">{{ current.nav[4] }}</a>
        <a href="#contact">{{ current.nav[5] }}</a>
      </nav>

      <div class="header-actions">
        <div class="lang-switch">
          <button :class="{ active: lang === 'zh' }" @click="setLang('zh')">中</button>
          <button :class="{ active: lang === 'en' }" @click="setLang('en')">EN</button>
        </div>
        <a class="header-cta" href="#contact">{{ current.cta }}</a>
      </div>
    </header>

    <main id="top">
      <section class="hero-section" :style="heroBackgroundStyle">
        <div class="hero-copy">
          <p class="eyebrow">{{ current.heroEyebrow }}</p>
          <h1>
            <span>{{ current.heroTitle[0] }}</span>
            {{ current.heroTitle[1] }}
          </h1>
          <p class="hero-text">{{ current.heroText }}</p>

          <div class="hero-actions">
            <a class="primary-action" href="#contact">{{ current.heroPrimary }}</a>
            <a class="secondary-action" href="#services">{{ current.heroSecondary }}</a>
          </div>

          <div class="stats-row">
            <article v-for="item in current.heroStats" :key="item.label">
              <strong>{{ item.value }}</strong>
              <span>{{ item.label }}</span>
            </article>
          </div>

          <div class="hero-capability-panel">
            <div class="hero-tags">
              <span v-for="item in current.heroCapabilities" :key="item">{{ item }}</span>
            </div>
            <div class="hero-flow">
              <i v-for="(item, index) in current.heroFlow" :key="item">
                <b>{{ String(index + 1).padStart(2, '0') }}</b>
                {{ item }}
              </i>
            </div>
          </div>
        </div>

        <div class="hero-signal">
          <p>{{ current.slides[activeSlide].tag }}</p>
          <strong>{{ current.slides[activeSlide].title }}</strong>
          <span>{{ current.floatCardText }}</span>
        </div>
      </section>

      <section id="services" class="services-section">
        <div class="section-head">
          <p>Services</p>
          <div>
            <h2>{{ current.servicesTitle }}</h2>
            <span>{{ current.servicesText }}</span>
          </div>
        </div>

        <div class="service-grid">
          <article v-for="item in current.services" :key="item.id" class="service-card">
            <div class="service-card-top">
              <i>{{ item.icon }}</i>
              <span>{{ item.id }}</span>
            </div>
            <em>{{ item.tag }}</em>
            <h3>{{ item.title }}</h3>
            <p>{{ item.desc }}</p>
            <a href="#contact">{{ item.action }} →</a>
          </article>
        </div>
      </section>

      <section id="pain-points" class="pain-section">
        <div class="section-head">
          <p>Pain Points</p>
          <div>
            <h2>{{ current.painTitle }}</h2>
            <span>{{ current.painText }}</span>
          </div>
        </div>

        <div class="pain-layout">
          <div class="pain-stack">
            <article v-for="item in current.pains" :key="item.id" class="pain-card">
              <span>{{ item.id }}</span>
              <div class="pain-problem">
                <small>企业常见痛点</small>
                <h3>{{ item.problem }}</h3>
                <p>{{ item.text }}</p>
              </div>
              <div class="pain-solution">
                <small>对应解决方案</small>
                <strong>{{ item.solution }}</strong>
              </div>
            </article>
          </div>

          <aside class="quick-panel">
            <p>{{ current.quickTitle }}</p>
            <ul>
              <li v-for="item in current.quickWins" :key="item">{{ item }}</li>
            </ul>
          </aside>
        </div>
      </section>

      <section id="showcase" class="showcase-section">
        <div class="section-head">
          <p>Showcase</p>
          <div>
            <h2>{{ current.showcaseTitle }}</h2>
            <span>{{ current.showcaseText }}</span>
          </div>
        </div>

        <div class="showcase-shell">
          <div class="slides-track" :style="trackStyle">
            <article v-for="slide in current.slides" :key="slide.title" class="slide">
              <div class="slide-copy">
                <p>{{ slide.tag }}</p>
                <h3>{{ slide.title }}</h3>
                <span>{{ slide.text }}</span>
                <div class="slide-tags">
                  <i v-for="bullet in slide.bullets" :key="bullet">{{ bullet }}</i>
                </div>
                <div class="slide-metrics">
                  <article v-for="metric in slide.metrics" :key="metric.label">
                    <strong>{{ metric.value }}</strong>
                    <span>{{ metric.label }}</span>
                  </article>
                </div>
              </div>

              <div class="slide-art" :style="{ backgroundImage: `linear-gradient(180deg, rgba(10,10,10,0.02), rgba(10,10,10,0.22)), url(${slide.image})` }">
                <div class="art-orb orb-a"></div>
                <div class="art-orb orb-b"></div>
                <div class="art-stack">
                  <div class="art-panel large"></div>
                  <div class="art-panel small"></div>
                  <div class="art-panel slim"></div>
                </div>
              </div>
            </article>
          </div>

          <div class="carousel-controls">
            <div class="dots">
              <button
                v-for="(_, index) in current.slides"
                :key="index"
                :class="{ active: index === activeSlide }"
                @click="goToSlide(index)"
              ></button>
            </div>
            <button class="next-button" @click="nextSlide">NEXT</button>
          </div>
        </div>
      </section>

      <section id="gallery" class="gallery-section">
        <div class="section-head">
          <p>Gallery</p>
          <div>
            <h2>{{ current.galleryTitle }}</h2>
            <span>{{ current.galleryText }}</span>
          </div>
        </div>

        <div class="gallery-grid">
          <article
            v-for="item in current.gallery"
            :key="item.title"
            class="gallery-card"
            :style="{ backgroundImage: `linear-gradient(180deg, rgba(12,12,12,0.06), rgba(12,12,12,0.58)), url(${item.image})` }"
          >
            <span>{{ item.title }}</span>
            <p>{{ item.text }}</p>
          </article>
        </div>
      </section>

      <section id="process" class="process-section">
        <div class="section-head">
          <p>Process</p>
          <div>
            <h2>{{ current.processTitle }}</h2>
            <span>{{ current.processText }}</span>
          </div>
        </div>

        <div class="process-grid">
          <article v-for="item in current.processSteps" :key="item.id">
            <span>{{ item.id }}</span>
            <h3>{{ item.title }}</h3>
            <p>{{ item.text }}</p>
          </article>
        </div>
      </section>

      <section id="partners" class="partners-section">
        <div class="section-head">
          <p>Partners</p>
          <div>
            <h2>{{ current.partnersTitle }}</h2>
            <span>{{ current.partnersText }}</span>
          </div>
        </div>

        <div class="partner-carousel" aria-label="合作单位循环展示">
          <div class="partner-track">
            <article v-for="(item, index) in partnerLoop" :key="`${item}-${index}`">
              <strong>{{ item }}</strong>
              <span>{{ current.partnerBadge }}</span>
            </article>
          </div>
        </div>
      </section>

      <section id="contact" class="contact-section">
        <div class="contact-copy">
          <p>Contact</p>
          <h2>{{ current.contactTitle }}</h2>
          <span>{{ current.contactText }}</span>
        </div>

        <div class="contact-card">
          <strong>广州佳汇企业管理有限公司</strong>
          <p>Kevin 18033390585</p>
          <a href="tel:18033390585">{{ current.contactButton }}</a>
        </div>
      </section>
    </main>
  </div>
</template>
