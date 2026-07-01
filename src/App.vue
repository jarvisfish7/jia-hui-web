<script setup>
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'

const lang = ref('zh')
const activeSlide = ref(0)

const copy = {
  zh: {
    nav: ['首页', '业务', '案例场景', '合作单位', '联系'],
    cta: '发起合作',
    heroEyebrow: 'GUANGZHOU JIA HUI ENTERPRISE MANAGEMENT CO., LTD.',
    heroTitle: ['为企业配置', '稳定的人才与现场服务系统'],
    heroText:
      '企业管理、人力资源服务、劳务派遣与综合外包协同，面向广州、深圳及全国项目提供响应支持。',
    heroPrimary: '立即洽谈',
    heroSecondary: '查看服务能力',
    heroStats: [
      { value: '2022', label: '成立时间' },
      { value: '全国', label: '服务范围' },
      { value: '30+', label: '经营方向' },
    ],
    floatCardTitle: '项目协同',
    floatCardText: '从用工配置到现场落地，保持交付稳定与响应速度。',
    heroImage: '/images/hero-minimal.png',
    servicesTitle: '核心业务能力',
    servicesText: '以管理、人才与执行三条线，形成更完整的服务链路。',
    services: [
      {
        id: '01',
        title: '企业管理咨询',
        desc: '组织运营、财税协同、礼仪会展与企业形象支持。',
      },
      {
        id: '02',
        title: '人力资源服务',
        desc: '招聘配置、项目补位、劳务服务与职业中介协同。',
      },
      {
        id: '03',
        title: '劳务派遣外包',
        desc: '保安、服务员、保洁员等多岗位全国范围输出。',
      },
    ],
    showcaseTitle: '服务场景轮播',
    showcaseText: '更像案例呈现，而不是普通公司简介。',
    slides: [
      {
        tag: '人力配置',
        title: '大体量用工项目的快速组织能力',
        text: '适配活动、园区、酒店与物业类项目的阶段性集中用工。',
        bullets: ['劳务派遣', '代招支持', '全国协同'],
        image:
          '/images/hero-enterprise.png',
      },
      {
        tag: '现场服务',
        title: '保安、服务员、保洁员等岗位的外派执行',
        text: '深圳分公司已建设完成，适合高频、持续型现场岗位需求。',
        bullets: ['岗位外派', '班次调度', '执行跟进'],
        image:
          '/images/service-hospitality.png',
      },
      {
        tag: '综合管理',
        title: '从咨询到执行的一体化企业服务组合',
        text: '覆盖企业管理、供应链协调、物业管理与后勤清洁等场景。',
        bullets: ['企业咨询', '供应链服务', '物业与保洁'],
        image:
          '/images/service-property.png',
      },
    ],
    galleryTitle: '精选服务画面',
    galleryText: '用更直观的方式表达项目组织、现场协同与企业支持能力。',
    gallery: [
      {
        title: '企业管理协同',
        image:
          '/images/hero-enterprise.png',
      },
      {
        title: '会议与项目执行',
        image:
          '/images/service-hospitality.png',
      },
      {
        title: '空间与后勤支持',
        image:
          '/images/service-property.png',
      },
    ],
    partnersTitle: '合作单位',
    partners: ['珠海长隆', '广东省人大', '广州市政府', '珠江物业'],
    contactTitle: '默认中文，可切换英文',
    contactText: '目前未提供公开电话与邮箱，正式上线前可补充真实联系方式。',
    contactButton: '补充联系方式',
  },
  en: {
    nav: ['Home', 'Services', 'Showcase', 'Partners', 'Contact'],
    cta: 'Start a Project',
    heroEyebrow: 'GUANGZHOU JIA HUI ENTERPRISE MANAGEMENT CO., LTD.',
    heroTitle: ['Reliable workforce', 'and on-site service systems for enterprises'],
    heroText:
      'Enterprise management, HR services, labor dispatch and outsourcing support for projects across Guangzhou, Shenzhen and nationwide.',
    heroPrimary: 'Talk to Us',
    heroSecondary: 'Explore Services',
    heroStats: [
      { value: '2022', label: 'Founded' },
      { value: 'Nationwide', label: 'Coverage' },
      { value: '30+', label: 'Service Areas' },
    ],
    floatCardTitle: 'Delivery Rhythm',
    floatCardText: 'From workforce setup to on-site execution, focused on speed and stability.',
    heroImage: '/images/hero-minimal.png',
    servicesTitle: 'Core Capabilities',
    servicesText: 'Management, staffing and field execution combined into one service chain.',
    services: [
      {
        id: '01',
        title: 'Enterprise Consulting',
        desc: 'Operations, finance coordination, events and corporate image support.',
      },
      {
        id: '02',
        title: 'HR Services',
        desc: 'Recruitment, flexible staffing, labor services and talent coordination.',
      },
      {
        id: '03',
        title: 'Dispatch & Outsourcing',
        desc: 'Security, waitstaff and cleaning teams deployed at national scale.',
      },
    ],
    showcaseTitle: 'Service Showcase',
    showcaseText: 'Presented more like selected scenarios than a plain company profile.',
    slides: [
      {
        tag: 'Workforce',
        title: 'Fast coordination for large-scale staffing needs',
        text: 'Suitable for events, parks, hotels and property-related workforce peaks.',
        bullets: ['Labor dispatch', 'Recruitment support', 'Nationwide response'],
        image:
          '/images/hero-enterprise.png',
      },
      {
        tag: 'Field Service',
        title: 'On-site dispatch for security, service and cleaning roles',
        text: 'Our Shenzhen branch supports recurring, high-frequency field staffing.',
        bullets: ['Role dispatch', 'Shift scheduling', 'Execution follow-up'],
        image:
          '/images/service-hospitality.png',
      },
      {
        tag: 'Integrated Support',
        title: 'A combined model from consulting to execution',
        text: 'Covers management advisory, supply-chain support, property and cleaning services.',
        bullets: ['Consulting', 'Supply chain', 'Property support'],
        image:
          '/images/service-property.png',
      },
    ],
    galleryTitle: 'Selected Scenes',
    galleryText: 'A more visual way to express coordination, staffing and enterprise support.',
    gallery: [
      {
        title: 'Management Coordination',
        image:
          '/images/hero-enterprise.png',
      },
      {
        title: 'Project Execution',
        image:
          '/images/service-hospitality.png',
      },
      {
        title: 'Facilities Support',
        image:
          '/images/service-property.png',
      },
    ],
    partnersTitle: 'Selected Partners',
    partners: ['Zhuhai Chimelong', 'Guangdong People’s Congress', 'Guangzhou Government', 'Pearl River Property'],
    contactTitle: 'Chinese by default, English available',
    contactText: 'Public phone and email were not provided yet and can be added before launch.',
    contactButton: 'Add Contact Info',
  },
}

const current = computed(() => copy[lang.value])

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
        <a href="#showcase">{{ current.nav[2] }}</a>
        <a href="#partners">{{ current.nav[3] }}</a>
        <a href="#contact">{{ current.nav[4] }}</a>
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
            <span>{{ item.id }}</span>
            <h3>{{ item.title }}</h3>
            <p>{{ item.desc }}</p>
          </article>
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
              </div>

              <div class="slide-art" :style="{ backgroundImage: `linear-gradient(180deg, rgba(10,10,10,0.08), rgba(10,10,10,0.42)), url(${slide.image})` }">
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

      <section class="gallery-section">
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
          </article>
        </div>
      </section>

      <section id="partners" class="partners-section">
        <div class="section-head">
          <p>Partners</p>
          <div>
            <h2>{{ current.partnersTitle }}</h2>
          </div>
        </div>

        <div class="marquee">
          <div class="marquee-track">
            <span v-for="(item, index) in [...current.partners, ...current.partners]" :key="`${lang}-${item}-${index}`">
              {{ item }}
            </span>
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
          <p>Guangzhou / Shenzhen / Nationwide</p>
          <a href="#top">{{ current.contactButton }}</a>
        </div>
      </section>
    </main>
  </div>
</template>
