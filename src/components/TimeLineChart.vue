<template>
  <div>
    <nav>
      <!--Shows our position on the timeline-->
      <div class="marker"></div>

      <div class="nav__track" data-draggable>
        <ul class="nav__list">
          <li v-for="section in sections" :key="section.id">
            <a :href="'#' + section.id" class="nav__link" data-link>
              <i>{{ section.year }}</i>
              <span style="padding-top: 4px">{{ section.month }}</span>
            </a>
          </li>
        </ul>
      </div>
    </nav>

    <main>
      <section v-for="(section, index) in sections" :id="section.id" :style="{ '--i': index }" :key="section.id">
        <div class="container">
          <h2 class="section__heading">
            <span>{{ section.year }} - {{ section.month }}</span>
            <span>{{ section.title }}</span>
          </h2>
          <div class="section__tasks">
            <ul>
              <li v-for="(item, index) in section.tasks" :key="index">
                <p style="font-weight: bolder">{{ item.task }}
                  <span v-if="item.status?.length>0">[{{ item.status }}]</span>
                </p>
                <p v-html="item.narrative"></p>
                <p v-if="item.reason?.length>0">Reason: {{ item.reason }}</p>
                <i v-if="item.tags?.length>0">Projects:&nbsp;</i>
                <span v-for="tag in item.tags" :key="tag" style="font-style: italic">
                  {{ tag }}
                </span>
              </li>
            </ul>
            <template v-if="section.ps_note?.length>0">
              <span style="font-style: italic;font-weight: bolder;margin-top: 1000px" v-for="note in section.ps_note" :key="note">PS: {{ note }}</span>
            </template>
          </div>
          <!--          <div class="section__image">-->
          <!--            <img :src="section.image" width="1200" height="1200" />-->
          <!--          </div>-->
        </div>
      </section>
    </main>
  </div>
</template>

<script setup>
import { gsap } from 'gsap'
import Draggable from 'gsap/Draggable'
import ScrollTrigger from 'gsap/ScrollTrigger'
import { onMounted, ref } from 'vue'

const sections = ref(
  [
    {
      'id': 'section_1',
      'year': '2022',
      'month': 'October',
      'title': 'Beginning of the Journey',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Create optimized container for local development',
          'narrative': 'An optimized container was created to make local development faster and easier to set up.'
        },
        {
          'task': 'Laravel Mix to Vite migration',
          'tags': ['JoBins'],
          'status': 'Hold',
          'reason': 'The team was not confident in the solution. It was later implemented in CRM.',
          'narrative': 'The build process was transitioned from Laravel Mix to Vite, which improved build times and the development experience.'
        }
      ]
    },
    {
      'id': 'section_2',
      'year': '2022',
      'month': 'November',
      'title': 'Improving Development Processes',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'ps_note': ['PHPUnit was already implemented but not maintained anymore.'],
      'tasks': [
        {
          'task': 'Streamline PHP tests with Pest and PHPUnit',
          'tags': ['JoBins'],
          'narrative': 'Pest and PHPUnit were integrated into the PHP testing framework, simplifying the testing process and improving efficiency. PHPUnit was initially selected for testing.'
        },
        {
          'task': 'Use Vite for build tool for CRM',
          'tags': ['CRM'],
          'narrative': 'Vite was adopted as the primary build tool, enhancing the speed and performance of the build process.'
        },
        {
          'task': 'Test case writing for JoBins',
          'narrative': 'Test cases for JoBins were developed and documented using the PHPUnitGen package, ensuring comprehensive test coverage and reliability with semi-automation.'
        },
        {
          'task': 'Implement Sentry for application-level logging',
          'narrative': 'Sentry was set up for application-level logging under supervision, which improved error tracking and debugging capabilities.',
          'tags': ['JoBins']
        }
      ]
    },
    {
      'id': 'section_3',
      'year': '2022',
      'month': 'December',
      'title': 'Enhancing CRM Features',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Consider other URLs as valid in memo',
          'narrative': 'The memo feature was enhanced to recognize and validate more types of URLs, including those with or without HTTP and HTTPS protocols.',
          'tags': ['CRM']
        },
        {
          'task': 'Start of Agent Pool Beta version',
          'narrative': 'The beta version of the Agent Pool was initiated, creating a system to collect data from agents and candidates efficiently.',
          'tags': ['Agent Pool']
        },
        {
          'task': 'Include Laravel Pint and Test suite run in Bitbucket pipeline',
          'narrative': 'Laravel Pint and the test suite were integrated into the Bitbucket pipeline, ensuring consistent code quality and automated testing.',
          'tags': ['Agent Pool']
        },
        {
          'task': 'Create sophisticated analytics tool for Agent Pool Beta',
          'narrative': 'An advanced analytics tool for the Agent Pool Beta was developed, providing detailed insights and performance metrics.',
          'tags': ['Agent Pool']
        },
        {
          'task': 'Address missing migration from live to local',
          'narrative': 'The missing migration from the live environment to the local setup was addressed, ensuring consistency and reliability.',
          'tags': ['JoBins']
        }
      ]
    },
    {
      'id': 'section_4',
      'year': '2023',
      'month': 'January',
      'title': 'Developing Solo Features',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'ps_note': ['Pint would introduce drastic changes in the codebase, so later two types of configurations were released: strict and weak formatting.'],
      'tasks': [
        {
          'task': 'Started first solo feature IP management',
          'tags': ['JoBins'],
          'narrative': 'The IP management feature was developed, allowing agents and clients to control access via IP addresses within the application.'
        },
        {
          'task': 'Improve Webpack build time for local development',
          'tags': ['JoBins'],
          'narrative': 'During the development of IP management, the Webpack configuration was optimized by filtering unnecessary compiling of folders, significantly reducing build times and enhancing the developer experience.'
        },
        {
          'task': 'Automate Linting with Pint and ESLint',
          'tags': ['JoBins'],
          'narrative': 'The linting process was automated using Pint and ESLint, ensuring code quality and consistency across the project.'
        }
      ]
    },
    {
      'id': 'section_5',
      'year': '2023',
      'month': 'February',
      'title': 'Pipeline and Testing Optimization',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Improve Bitbucket pipeline execution time',
          'duration': '30 min to 10 mins',
          'tags': ['JoBins'],
          'narrative': 'The Bitbucket pipeline execution time was reduced from 30 minutes to 15 minutes by separating frontend compiling, improving overall deployment efficiency.'
        },
        {
          'task': 'Setup Cypress for E2E frontend testing',
          'status': 'Hold',
          'tags': ['JoBins'],
          'narrative': 'Cypress was set up for end-to-end frontend testing, ensuring comprehensive test coverage for the application.',
          'reason': 'Halted due to no available resources to continue writing test cases.'
        },
        {
          'task': 'Laravel 9x and 10x upgrade',
          'tags': ['JoBins'],
          'narrative': 'The application upgrade to Laravel 9x was continued, taking advantage of the latest features and improvements.',
          'status': 'Hold',
          'reason': 'No confidence that the upgrade would not break features.'
        },
        {
          'task': 'PHP 8.0 to 8.1 upgrade, deprecated code upgrade',
          'tags': ['JoBins'],
          'narrative': 'The PHP version was upgraded from 8.0 to 8.1, and deprecated code was updated to ensure compatibility and performance improvements.',
          'status': 'Hold',
          'reason': 'Introduced drastic changes to the codebase, which did not guarantee that no features were broken.'
        },
        {
          'task': 'Parallel testing',
          'tags': ['JoBins'],
          'narrative': 'Parallel testing was tried, allowing tests to run concurrently and reducing overall testing time.',
          'status': 'Hold',
          'reason': 'Test code was not written to support parallel testing.'
        },
        {
          'task': 'Install Laravel Horizon for queue',
          'tags': ['JoBins'],
          'narrative': 'Laravel Horizon was installed to manage queues, improving job processing and monitoring capabilities.',
          'status': 'Hold',
          'reason': 'No confidence that Redis would not break the database queues.'
        }
      ]
    },
    {
      'id': 'section_6',
      'year': '2023',
      'month': 'March',
      'title': 'Debugging and Feature Development',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Install Inspector for debugging',
          'narrative': 'Inspector was installed to enhance the debugging process, making it easier to identify and track slow functions and resolve issues quickly.',
          'status': 'Degraded',
          'reason': 'Deployed on test environment but not tracked properly.',
          'tags': ['JoBins', 'CRM']
        },
        {
          'task': 'Create Netmaker for VPN',
          'tags': ['Infra'],
          'narrative': 'Netmaker for VPN was introduced, providing a secure and reliable virtual private network solution. The demo was presented and eventually rolled out.'
        },
        {
          'task': 'Deploy Teleport',
          'tags': ['Infra'],
          'narrative': 'Teleport was deployed for a demo, showcasing its capabilities and potential uses. The demo was presented and eventually rolled out.'
        },
        {
          'task': 'Beginning of review and rating feature',
          'tags': ['JoBins'],
          'narrative': 'The development of the review and rating feature was led, allowing users to provide feedback and ratings.'
        },
        {
          'task': 'Database design and documentation in Confluence',
          'tags': ['JoBins'],
          'narrative': 'The database schema was designed and documented in Confluence, ensuring clear and accessible documentation for the team.'
        },
        {
          'task': 'Folder structure and list of technologies for feature',
          'tags': ['JoBins'],
          'narrative': 'The folder structure and technologies used for the feature were organized, providing a clear development roadmap.'
        }
      ]
    },
    {
      'id': 'section_7',
      'year': '2023',
      'month': 'April',
      'title': 'Pipeline Enhancements and AI Integration',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Run PHPUnit test suite in Bitbucket pipeline on PR event',
          'tags': ['JoBins'],
          'narrative': 'The pipeline was configured to run PHPUnit tests automatically on PR pushes, ensuring code quality is maintained and reducing deployment.'
        },
        {
          'task': 'AI Job Description form fill up',
          'narrative': 'A simple AI chatbot based on OpenAI was developed to automatically fill up job description forms, streamlining the recruitment process.',
          'tags': ['JoBins'],
          'status': 'Hold'
        },
        {
          'task': 'CV parsing using OpenAPI ChatGPT and ChatGPT wrapper',
          'tags': ['JoBins'],
          'narrative': 'OpenAPI ChatGPT and a ChatGPT wrapper were used to parse CVs, improving the efficiency of the recruitment process.',
          'status': 'Hold',
          'reason': 'Not efficient to parse handwritten CVs.'
        }
      ]
    },
    {
      'id': 'section_8',
      'year': '2023',
      'month': 'May',
      'title': 'Research and Documentation',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Research trends in agent ratings',
          'tags': ['JoBins'],
          'narrative': 'Research on current trends in agent ratings was conducted, providing valuable insights for future feature development.'
        },
        {
          'task': 'Incremental average case study for rating',
          'tags': ['JoBins'],
          'narrative': 'A case study on incremental averages for ratings was conducted, offering data-driven insights for improving the rating system.'
        },
        {
          'task': 'Feature documentation in Confluence',
          'tags': ['JoBins'],
          'narrative': 'Features were documented in Confluence, ensuring comprehensive and accessible documentation for the team.'
        }
      ]
    },
    {
      'id': 'section_9',
      'year': '2023',
      'month': 'June',
      'title': 'Tool Development and Enhancements',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Created URL tracking for JoBins',
          'narrative': 'A simple and comprehensive URL tracking tool for JoBins was developed, improving the ability to track and analyze URLs.'
        },
        {
          'task': 'Created JoBins task generator',
          'narrative': 'A generator for JoBins was created that scaffolded tasks, making it easier to set up and manage tasks efficiently.'
        }
      ]
    },
    {
      'id': 'section_10',
      'year': '2023',
      'month': 'July',
      'title': 'DevOps and Pipeline Improvements',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Start of JoBins direct scout management',
          'tags': ['JoBins'],
          'narrative': 'The direct scout management feature for JoBins was started, enhancing the recruitment and management processes.'
        },
        {
          'task': 'Focus on DevOps',
          'narrative': 'Focus returned to DevOps, improving infrastructure and deployment processes. ' +
            '<br> 1. Faster pipeline deployment with intelligent execution ' +
            '<br>2. Automate OSWAP testing from GitHub ' +
            '<br>3. Automated OS updates ' +
            '<br>4. Set up OS vulnerability scanning and reporting'
        },
        {
          'task': 'Create Ansible playbook for managing changes and GitOps',
          'narrative': 'An Ansible playbook was created to manage all changes and implement GitOps, improving infrastructure management.'
        },
        {
          'task': 'Implement Laravel Health package for system health monitoring',
          'narrative': 'The Laravel Health package was implemented to monitor system health, ensuring the application\'s reliability and performance.'
        }
      ]
    },
    {
      'id': 'section_11',
      'year': '2023',
      'month': 'August',
      'title': 'Performance and Security Enhancements',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Optimize Webpack configuration for faster compile',
          'tags': ['JoBins'],
          'narrative': 'Webpack configuration and caching were optimized, reducing compile times and improving overall performance.'
        },
        {
          'task': 'Research and implement PHPStan to PR comments',
          'narrative': 'PHPStan was researched and implemented to PR comments, enhancing code review processes.'
        },
        {
          'task': 'Conduct JMeter load testing',
          'narrative': 'Load testing was conducted using JMeter, identifying and addressing performance bottlenecks.'
        },
        {
          'task': 'Integrate SonarQube into CRM, JoBins and other projects',
          'narrative': 'SonarQube was integrated into the CRM, JoBins and other projects improving code quality and security analysis.'
        }
      ]
    },
    {
      'id': 'section_12',
      'year': '2023',
      'month': 'September',
      'title': 'DevOps Research and Implementations',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Analyze PHPStan on commit for JoBins',
          'narrative': 'PHPStan was analyzed on commit for JoBins, ensuring code quality and compliance.'
        },
        {
          'task': 'DevOps Research and Implementations',
          'narrative': '1. Tenable Nessus' +
            '<br>Tenable Nessus was researched and implemented, enhancing security vulnerability assessments.' +
            '<br><br>2. Nginx ModSecurity' +
            '<br>Nginx ModSecurity usage was researched, improving the security of the web server' +
            '<br><br>3. AWS CloudFront demo' +
            '<br>4. Bun for JoBins project'
        },
        {
          'task': 'Implement selective supervisor reload after deploy for JoBins',
          'narrative': 'A selective supervisor reload after deploy for JoBins was implemented, improving deployment efficiency.'
        },
        {
          'task': 'Update corporate \'Privacy Policy\' and add \'Basic Policy of Information Security\'',
          'narrative': 'The corporate \'Privacy Policy\' was updated, and a new page for the \'Basic Policy of Information Security\' was added, enhancing policy clarity and compliance.'
        }
      ]
    },
    {
      'id': 'section_13',
      'year': '2023',
      'month': 'October',
      'title': 'Session Management Improvements',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Develop load balancer roadmap',
          'narrative': 'A roadmap for the load balancer was developed, outlining steps for implementation and optimization.'
        },
        {
          'task': 'Research and document file session to Redis and Database migration',
          'narrative': 'The process of migrating session management from file-based to Redis and Database was researched and documented, improving performance and reliability.'
        },
        {
          'task': 'Move CRM DNS name to agent CRM',
          'tags': ['CRM'],
          'narrative': 'The DNS name of the CRM was migrated to agent CRM, ensuring seamless access, backward compatibility of old URL and improved performance.'
        }
      ]
    },
    {
      'id': 'section_14',
      'year': '2023',
      'month': 'November',
      'title': 'Automation and Scheduling',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Prepare PHPStan issue list in Excel and assign',
          'tags': ['JoBins'],
          'narrative': 'Develop command to convert PHPStan Neon to XLSX Excel, making it easier to track and assign tasks for resolution.' +
            '<br><br> Run PHPStan on only changed PHP files'
        },
       {
          'task': 'Show uploaded recruitment documents in-browser PDF viewer',
          'narrative': 'A feature was implemented to show uploaded recruitment documents in an in-browser PDF viewer, enhancing usability.'
        },
        {
          'task': 'Schedule pipeline for periodic agent list fetch',
          'narrative': 'A pipeline was scheduled to periodically fetch the agent list, ensuring data is always up-to-date.'
        },
        {
          'task': 'Conduct database upgrade check and document process',
          'narrative': 'A database upgrade check was conducted and the process documented, ensuring a smooth transition and minimal disruption.'
        },
        {
          'task': 'Research Jira automation and document process in Excel',
          'narrative': 'Research on Jira automation was conducted and the process documented in Excel, enhancing project tracking and management.'
        }
      ]
    },
    {
      'id': 'section_15',
      'year': '2023',
      'month': 'December',
      'title': 'Compatibility Testing and Release Management',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Upgrade test-server database to MySQL 8.0',
          'narrative': 'The test-server database was upgraded to MySQL 8.0 to start compatibility testing and start compatibility testing of MySQL 8 with codebase.'
        },
        {
          'task': 'Begin release deployment',
          'narrative': 'The process of deploying new releases was started, ensuring smooth transitions and minimal downtime.' +
            '<br><br> Develop system to create new databases for releases dynamically' +
            '<br><br>Implement release branch manager to track and deletion of release page. '
        },
        {
          'task': 'Conduct short KSS on WireGuard and its usage for JoBins',
          'narrative': 'A short Knowledge Sharing Session (KSS) on WireGuard and its usage for JoBins was conducted, enhancing team knowledge.'
        },
        {
          'task': 'Configure Nginx for VPN-only access',
          'narrative': 'Nginx was configured to restrict access to VPN-only connections, enhancing security.'
        }
      ]
    },
    {
      'id': 'section_16',
      'year': '2024',
      'month': 'January',
      'title': 'Redis Integration and SES Usage',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'ps_note': ['Sazn has become the only developer in JoBins who writes correct code with formatting. [Pun intended]'],
      'tasks': [
        {
          'task': 'In-depth study of SES and AWS S3 usage',
          'narrative': 'An in-depth study on SES and AWS S3 usage was conducted, identifying best practices and potential improvements.'
        },
        {
          'task': 'Automate Pint and push process from pipeline',
          'narrative': 'The Pint and push process was automated from the pipeline with Git commits, streamlining code updates and deployments.'
        }
      ]
    },
    {
      'id': 'section_17',
      'year': '2024',
      'month': 'February',
      'title': 'Database Configurations and Project Setup',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Configure separate databases for read and write operations',
          'narrative': 'Separate databases for read and write operations were configured, improving performance and data management.',
          'status': 'Hold',
          'reason': 'No real data of sync between master and slave database.'
        },
        {
          'task': 'Release PHPMyAdmin for better database management',
          'narrative': 'PHPMyAdmin was released for better database management and a user-friendly interface for accessing release databases.'
        },
        {
          'task': 'Migrate test-server to new internal server',
          'narrative': 'The test-server was migrated to a new internal server, ensuring better performance and resource management.'
        }
      ]
    },
    {
      'id': 'section_18',
      'year': '2024',
      'month': 'March',
      'title': 'Upgrades and Research',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Collaborate on MySQL 8 staging upgrade',
          'narrative': 'Collaboration on upgrading the MySQL 8 staging environment was carried out, ensuring compatibility and performance improvements.'
        },
        {
          'task': 'Research on FIFO queue via Redis',
          'narrative': 'Research on implementing FIFO queues via Redis was conducted, exploring potential benefits and use cases.'
        },
        {
          'task': 'Format entire codebase with Pint',
          'narrative': 'The entire codebase was formatted using Pint, ensuring consistent code style and quality.'
        },
        {
          'task': 'Address high CPU usage by changing queue mode',
          'narrative': 'High CPU usage issues were addressed by changing the queue mode from listen to work, improving efficiency on the QA server.'
        }
      ]
    },
    {
      'id': 'section_19',
      'year': '2024',
      'month': 'April',
      'title': 'Optimization and Feature Planning',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Start development of JoBins mobile app',
          'narrative': 'Development of the JoBins mobile app was started, expanding the application\'s reach and functionality. Collaboration and planning sessions with the team were initiated, setting the foundation for upcoming projects.'
        },
        {
          'task': 'Discuss API architecture with teams',
          'narrative': 'Discussions on API architecture with the teams were led, aligning on design and implementation strategies.'
        },
        {
          'task': 'Conduct research on Domain-Driven Design (DDD) and collect resources',
          'narrative': 'Research on Domain-Driven Design (DDD) was conducted, and a collection of resources for the team was curated.'
        },
        {
          'task': 'Optimize animations on JoBins front page',
          'narrative': 'Animations on the JoBins front page were optimized, improving user experience and performance.'
        },
        {
          'task': 'Implement Elastic MQ as SQS FIFO queue for Laravel',
          'narrative': 'Elastic MQ was implemented as an SQS FIFO queue for Laravel, enhancing the messaging system.'
        },
        {
          'task': 'Use Redis as the queue driver',
          'narrative': 'Redis was implemented as the queue driver, improving performance and reliability of the queue system.'
        }
      ]
    },
    {
      'id': 'section_20',
      'year': '2024',
      'month': 'May',
      'title': 'Collaborations and Fixes',
      'image': 'https://assets.codepen.io/85648/radiohead_pablo-honey.jpg',
      'tasks': [
        {
          'task': 'Collaborate on Magika Rust build',
          'narrative': 'Collaboration on the Magika Rust build project was carried out, combining expertise to achieve project goals.'
        },
        {
          'task': 'Address various PHPStan issues',
          'narrative': 'Various PHPStan issues were addressed, ensuring code quality and compliance with standards.'
        },
        {
          'task': 'Create PR Diff Splitter Script',
          'narrative': 'A PR Diff Splitter Script was developed, making it easier to review pull requests by splitting large diffs into manageable parts.'
        }
      ]
    }
  ]
)

onMounted(() => {
  initAnimations()
})

const initAnimations = () => {
  gsap.registerPlugin(ScrollTrigger, Draggable)
  const sections = gsap.utils.toArray('section')
  const track = document.querySelector('[data-draggable]')
  const navLinks = gsap.utils.toArray('[data-link]')
  const marker = document.querySelector('.marker')
  const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)')

  const lastItemWidth = () => navLinks[navLinks.length - 1].offsetWidth
  const getUseableHeight = () => document.documentElement.offsetHeight - window.innerHeight

  const getDraggableWidth = () => {
    return ((track.offsetWidth * 0.5) - lastItemWidth())
  }

  const updatePosition = () => {
    const left = track.getBoundingClientRect().left * -1
    const width = getDraggableWidth()
    const useableHeight = getUseableHeight()
    const y = gsap.utils.mapRange(0, width, 0, useableHeight, left)

    st.scroll(y)
  }

  const tl = gsap.timeline()
                 .to(track, {
                   x: () => getDraggableWidth() * -1,
                   ease: 'none'
                 })

  const st = ScrollTrigger.create({
    animation: tl,
    scrub: 0
  })

  Draggable.create(track, {
    type: 'x',
    inertia: true,
    bounds: {
      minX: 0,
      maxX: getDraggableWidth() * -1
    },
    edgeResistance: 1,
    onDragStart: () => st.disable(),
    onDragEnd: () => st.enable(),
    onDrag: updatePosition,
    onThrowUpdate: updatePosition
  })

  const initSectionAnimation = () => {
    /* Do nothing if user prefers reduced motion */
    if (prefersReducedMotion.matches) return

    sections.forEach((section, index) => {
      const heading = section.querySelector('h2')
      const tasks = section.querySelector('.section__tasks')
      const image = section.querySelector('.section__image')

      /* Set animation start state */
      gsap.set(heading, {
        opacity: 0,
        y: 50
      })
      gsap.set(tasks, {
        opacity: 0,
        y: 50
      })
      gsap.set(image, {
        opacity: 0,
        rotateY: 0
      })

      /* Create the timeline */
      const sectionTl = gsap.timeline({
        scrollTrigger: {
          trigger: section,
          start: () => 'top center',
          end: () => `+=${window.innerHeight}`,
          toggleActions: 'play reverse play reverse'
          // toggleClass: 'is-active',
          // markers: true,
        }
      })

      /* Add tweens to the timeline */
      sectionTl.to(image, {
                 opacity: 1,
                 rotateY: -5,
                 duration: 6,
                 ease: 'elastic'
               })
               .to(heading, {
                 opacity: 1,
                 y: 0,
                 duration: 2
               }, 0.5)
               .to(tasks, {
                 opacity: 1,
                 y: 0,
                 duration: 3
               }, 0.5)

      /* Create a new timeline to add an active class to the nav link for the current section */
      gsap.timeline({
        scrollTrigger: {
          trigger: section,
          start: 'top 20px',
          end: () => `bottom top`,
          toggleActions: 'play none play reverse',
          onToggle: ({ isActive }) => {
            const sectionLink = navLinks[index]

            if (isActive) {
              sectionLink.classList.add('is-active')
              const linkRect = sectionLink.getBoundingClientRect()
              const linkLeft = linkRect.left + window.scrollX
              const linkCenter = linkLeft + linkRect.width / 2
              const markerLeft = linkCenter - marker.offsetWidth / 2

              gsap.to(marker, {
                left: markerLeft > 0 ? markerLeft : linkRect.width,
                duration: 0.5,
                ease: 'power2.out'
              })
            } else {
              sectionLink.classList.remove('is-active')
            }
          }
        }
      })
    })
  }

  initSectionAnimation()

  /* Allow navigation via keyboard */
  track.addEventListener('keyup', (e) => {
    const id = e.target.getAttribute('href')
    if (!id || e.key !== 'Tab') return

    const section = document.querySelector(id)
    const y = section.getBoundingClientRect().top + window.scrollY

    st.scroll(y)
  })
}
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

html {
  overscroll-behavior: contain;
}

@media (prefers-reduced-motion: no-preference) {
  html {
    scroll-behavior: smooth;
  }
}

body {
  --activeColor: rgb(240, 240, 240);
  --navBgColor: rgb(37, 38, 41);
  --navTextColor: rgb(144, 144, 150);
  --mainBg: rgb(20, 20, 23);
  font-family: 'Syncopate', sans-serif;
  min-height: 100vh;
  margin: 0;
  color: rgb(20, 20, 23);
  background: var(--mainBg);
}

img {
  display: block;
  width: 100%;
  height: auto;
  max-width: 100%;
}

section {
  --h: calc(var(--i) * 30);

  min-height: 100vh;
  padding: 8rem 0 max(5vh, 2rem);
  display: flex;
  justify-content: center;
  //align-items: center;
  background-color: hsl(var(--h, 0) 75% 60%);
}


.container {
  width: 100%;
  //max-width: 80rem;
  padding: 0 max(5vw, 1rem);
  transform-style: preserve-3d;
  perspective: 900px;
}

@media (min-width: 32em) {
  .container {
    display: grid;
    grid-template-columns: repeat(7, minmax(0, 1fr));
    gap: 1rem;
  }
}

nav {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background: var(--navBgColor);
  color: var(--navTextColor);
  z-index: 2;
  height: 7rem;
}

nav::after {
  content: '';
  position: absolute;
  top: 1.7rem;
  left: 0;
  width: 100%;
  height: 0.25rem;
  background: currentColor;
  pointer-events: none;
}

.marker {
  position: fixed;
  top: 1.75rem;
  left: 4rem;
  width: 1rem;
  height: 1rem;
  transform: translate3d(-50%, -50%, 0);
  background: var(--activeColor);
  border-radius: 100%;
  z-index: 2000;

  &::before {
    content: '';
    position: absolute;
    top: calc(50% - 0.2rem);
    right: 100%;
    width: 400rem;
    height: 0.4rem;
    background-color: var(--activeColor);
  }
}


.nav__track {
  position: relative;
  min-width: max(200rem, 200%);
  padding: 1.5rem max(100rem, 100%) 0 0;
  height: 6rem;
}

.nav__list {
  list-style: none;
  display: flex;
  justify-content: space-between;
  margin: 0;
  padding: 0;
}

.nav__link {
  position: relative;
  display: block;
  min-width: 8rem;
  padding: 2.25rem 1rem 0.5rem;
  text-align: center;
  color: inherit;
  text-decoration: none;
  z-index: 1;
  transition: color 150ms;
}

.nav__link:hover,
.nav__link:focus {
  color: var(--activeColor);
  text-decoration: underline;
}

.nav__link::after {
  content: '';
  position: absolute;
  top: 0;
  left: 50%;
  width: 0.65rem;
  height: 0.65rem;
  background-color: currentColor;
  border-radius: 50%;
  transform: translate3d(-50%, 0, 0);
  transform-origin: center center;
}

.nav__link span {
  display: block;
  transition: transform 200ms;
}

.nav__link.is-active span {
  transform: scale(1.4);
  color: var(--activeColor);
}

.nav__link.is-active::after {
  display: none;
}

.section__heading {
  font-size: clamp(2rem, 12vmin, 3rem);
  line-height: 1;
  letter-spacing: -0.06em;
  margin: 0 0 1rem;
  grid-row: 1;
  grid-column: 1 / span 4;
  align-self: start;
  position: relative;
  z-index: 1;
}

.section__tasks {
  grid-row: 2;
  grid-column: 1 / span 4;
}

.section__tasks p {
  font-size: 20px;
}

.section__heading span {
  display: block;
}

.section__heading span:first-child {
  font-size: clamp(1rem, 10vmin, 5rem);
}

.section__heading span:nth-child(2) {
  word-break: break-word;
}

.section__image {
  grid-row: 2;
  grid-column: 5 / span 3;
  position: relative;
  box-shadow: 0.45rem 0.45rem 8rem rgb(0 0 0 / 0.3);
  align-self: center;
}

.section__image::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: hsl(var(--h, 0) 50% 50%);
  mix-blend-mode: screen;
}

.section__image img {
  filter: brightness(0.5) grayscale(100%);
}
</style>
