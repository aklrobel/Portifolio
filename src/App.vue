<template>
  <div class="min-h-screen">
    <!-- Background decorative elements -->
    <div class="fixed inset-0 -z-10 overflow-hidden pointer-events-none">
      <div class="absolute top-20 right-10 w-96 h-96 bg-gruvbox-orange/10 rounded-full blur-3xl animate-float"></div>
      <div class="absolute top-1/3 left-10 w-64 h-64 bg-gruvbox-purple/10 rounded-full blur-3xl animate-float" style="animation-delay: 2s;"></div>
      <div class="absolute bottom-20 right-1/4 w-80 h-80 bg-gruvbox-aqua/10 rounded-full blur-3xl animate-float" style="animation-delay: 4s;"></div>
    </div>

    <!-- Sidebar -->
    <aside class="hidden lg:flex fixed left-0 top-0 h-screen w-80 bg-background border-r border-border z-50 flex-col">
      <!-- Header with Name -->
      <div class="p-12 pb-8">
        <h1 class="text-4xl font-bold text-foreground mb-2 leading-tight">
          Robel<br/>Aklilu
        </h1>
        <p class="text-gruvbox-blue font-semibold text-sm uppercase tracking-wider mb-6">
          Full stack Developer
        </p>
        <p class="text-muted-foreground text-sm leading-relaxed">
          Building elegant solutions with clean code and thoughtful design.
        </p>
      </div>

      <div class="border-t border-gruvbox-orange/30 mx-12"></div>

      <!-- Navigation Links -->
      <nav class="flex-1 px-12 py-8 space-y-1">
        <a v-for="link in navLinks" :key="link.id"
           :href="link.href"
           @click="activeSection = link.id"
           :class="['group flex items-center gap-4 py-3 transition-all duration-300 relative',
                    activeSection === link.id 
                      ? 'text-gruvbox-orange scale-110' 
                      : 'text-muted-foreground hover:text-foreground hover:scale-105']">
          <div :class="['w-12 h-0.5 transition-all duration-300',
                        activeSection === link.id 
                          ? 'bg-gruvbox-orange w-16' 
                          : 'bg-border group-hover:bg-muted-foreground group-hover:w-14']"></div>
          <span :class="['font-medium uppercase tracking-widest transition-all duration-300',
                         activeSection === link.id ? 'text-sm font-bold' : 'text-xs']">{{ link.label }}</span>
          <div v-if="activeSection === link.id" 
               class="absolute left-0 top-0 bottom-0 w-1 bg-gruvbox-orange rounded-r"></div>
        </a>
      </nav>

      <!-- Dark Mode Toggle -->
      <div class="px-12 pb-8 flex justify-center">
        <button @click="toggleDarkMode" 
                class="px-6 py-2.5 bg-foreground text-background rounded-lg font-medium text-sm hover:opacity-90 transition-opacity flex items-center justify-center gap-2">
          <svg v-if="!isDark" class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
          </svg>
          <svg v-else class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
          </svg>
          <span>{{ isDark ? '' : '' }}</span>
        </button>
      </div>

      <div class="border-t border-gruvbox-orange/30 mx-12"></div>

      <!-- Social Links -->
      <div class="px-12 py-8 flex gap-6">
        <a href="https://github.com/RobelAK" target="_blank" 
           class="text-muted-foreground hover:text-foreground transition-colors"
           title="GitHub">
          <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
            <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
          </svg>
        </a>
        
        <a href="https://t.me/robelakl" target="_blank"
           class="text-muted-foreground hover:text-foreground transition-colors"
           title="Telegram">
          <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
            <path d="M11.944 0A12 12 0 0 0 0 12a12 12 0 0 0 12 12 12 12 0 0 0 12-12A12 12 0 0 0 12 0a12 12 0 0 0-.056 0zm4.962 7.224c.1-.002.321.023.465.14a.506.506 0 0 1 .171.325c.016.093.036.306.02.472-.18 1.898-.962 6.502-1.36 8.627-.168.9-.499 1.201-.82 1.23-.696.065-1.225-.46-1.9-.902-1.056-.693-1.653-1.124-2.678-1.8-1.185-.78-.417-1.21.258-1.91.177-.184 3.247-2.977 3.307-3.23.007-.032.014-.15-.056-.212s-.174-.041-.249-.024c-.106.024-1.793 1.14-5.061 3.345-.48.33-.913.49-1.302.48-.428-.008-1.252-.241-1.865-.44-.752-.245-1.349-.374-1.297-.789.027-.216.325-.437.893-.663 3.498-1.524 5.83-2.529 6.998-3.014 3.332-1.386 4.025-1.627 4.476-1.635z"/>
          </svg>
        </a>
        
      </div>
    </aside>

    <!-- Main Content with offset for sidebar -->
    <div class="lg:ml-80">

    <!-- Hero Section -->
    <section id="hero" class="min-h-screen flex items-center justify-center px-6">
      <div class="max-w-4xl mx-auto text-center">
        
        <h1 class="text-6xl lg:text-8xl font-bold mb-6 tracking-tight">
          <span class="text-gruvbox-orange">Robel Aklilu</span>
          <br />
          <span class="text-gruvbox-blue min-h-[1.2em] inline-block">{{ displayedTitle }}<span class="animate-pulse">|</span></span>
        </h1>
        
        <p class="text-xl lg:text-2xl text-muted-foreground mb-12 leading-relaxed max-w-2xl mx-auto">
          Building elegant solutions with clean code and thoughtful design
        </p>
        
        <div class="flex items-center justify-center gap-4 flex-wrap">
          <a href="#projects" class="px-8 py-4 bg-gruvbox-orange text-background rounded-xl font-semibold hover:scale-105 hover:shadow-xl transition-all duration-300">
            View Projects
          </a>
          <a href="#contact" class="px-8 py-4 border-2 border-gruvbox-orange text-gruvbox-orange rounded-xl font-semibold hover:bg-gruvbox-orange hover:text-background transition-all duration-300">
            Get in Touch
          </a>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="min-h-screen flex items-center py-24 px-6">
      <div class="max-w-4xl mx-auto">
        <h2 class="text-4xl lg:text-5xl font-bold mb-12">
          About <span class="text-gruvbox-orange">Me</span>
        </h2>
        
        <div class="bg-card border border-border rounded-2xl p-8 shadow-lg hover:border-gruvbox-orange hover:shadow-2xl transition-all duration-300 hover:scale-[1.02]">
          <p class="text-lg leading-relaxed text-muted-foreground mb-6">
            <span class="text-5xl text-gruvbox-orange font-bold float-left mr-3 mt-1 leading-none">I</span>
            am a results-oriented Full-Stack Developer with strong expertise in the Microsoft ecosystem, including C#, .NET, and SQL Server, and hands-on experience building scalable web and mobile applications.
          </p>

          <p class="text-lg leading-relaxed text-muted-foreground mb-6">
            I also work with modern JavaScript and TypeScript frameworks such as Angular and React, and have cross-platform mobile development experience using Flutter. Additionally, I apply DevOps practices to streamline development workflows.
          </p>

          <p class="text-lg leading-relaxed text-muted-foreground">
            I work with tools such as Jenkins, CI/CD pipelines, version control, containerization, and automated deployments to ensure reliability and efficiency across projects. I hold a degree in Information Systems from Wolkite University and bring a strong academic foundation, practical problem-solving skills, effective communication, and a commitment to continuous learning and professional growth.
          </p>

        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="min-h-screen flex items-center py-24 px-6 bg-muted/30">
      <div class="max-w-4xl mx-auto">
        <h2 class="text-4xl lg:text-5xl font-bold mb-12">
          Work <span class="text-gruvbox-orange">Experience</span>
        </h2>
        
        <div class="space-y-8">
          <div class="bg-card border-l-4 border-gruvbox-orange rounded-r-xl p-6 shadow-lg hover:shadow-2xl hover:scale-[1.02] transition-all duration-300 cursor-pointer">
            <div class="flex flex-wrap items-start justify-between mb-3">
              <div>
                <h3 class="text-2xl font-bold text-foreground">Software Enginner</h3>
                <p class="text-gruvbox-blue font-semibold">XOKA IT Solutions</p>
              </div>
              <span class="text-sm text-muted-foreground">December 2024 - Present</span>
            </div>
            <p class="text-muted-foreground leading-relaxed">
              Developed responsive front-end interfaces using Angular and TypeScript. Built and maintained RESTful APIs 
              with ASP.NET Core and C#. Designed and optimized SQL Server databases to support government service workflows. 
              Implemented secure authentication and role-based access control (RBAC). Ensured cross-browser compatibility, 
              mobile responsiveness, and collaborated with teams to deliver secure, reliable end-to-end solutions.
            </p>

          </div>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="min-h-screen flex items-center py-24 px-6 bg-muted/30">
      <div class="max-w-7xl mx-auto">
        <h2 class="text-4xl lg:text-5xl font-bold mb-4 text-center">
          Featured <span class="text-gruvbox-orange">Projects</span>
        </h2>
        <p class="text-center text-muted-foreground mb-16 text-lg">Some of my recent involvments</p>
        
        <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-8">
          <div v-for="project in projects" :key="project.id" 
               class="group bg-card border-2 border-border rounded-2xl overflow-hidden hover:border-gruvbox-orange hover:shadow-2xl transition-all duration-500 hover:-translate-y-3 hover:scale-[1.02] cursor-pointer">
            <div class="h-48 overflow-hidden relative" :class="project.image ? '' : 'bg-gradient-to-br ' + project.gradient">
              <img v-if="project.image" :src="project.image" :alt="project.title" class="w-full h-full object-cover" />
            </div>
            
            <div class="p-6">
              <h3 class="text-2xl font-bold mb-3 group-hover:text-gruvbox-orange transition-colors">
                {{ project.title }}
              </h3>
              <p class="text-muted-foreground mb-4 leading-relaxed">
                {{ project.description }}
              </p>
              
              <div class="flex flex-wrap gap-2 mb-4">
                <span v-for="tech in project.tech" :key="tech" 
                      class="px-3 py-1 bg-gruvbox-orange/10 border border-gruvbox-orange/30 rounded-full text-xs font-medium text-gruvbox-orange">
                  {{ tech }}
                </span>
              </div>
              
              <div class="flex gap-3 opacity-0 group-hover:opacity-100 transition-opacity duration-300">
                <a :href="project.github" target="_blank" 
                   class="flex-1 text-center px-4 py-2 bg-gruvbox-orange/10 border border-gruvbox-orange/30 rounded-lg text-sm font-medium text-gruvbox-orange hover:bg-gruvbox-orange hover:text-background transition-all duration-300 flex items-center justify-center gap-2">
                  <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
                  </svg>
                  Code
                </a>
                <a v-if="project.demo" :href="project.demo" target="_blank"
                   class="flex-1 text-center px-4 py-2 bg-gruvbox-blue/10 border border-gruvbox-blue/30 rounded-lg text-sm font-medium text-gruvbox-blue hover:bg-gruvbox-blue hover:text-background transition-all duration-300 flex items-center justify-center gap-2">
                  Live Demo
                </a>
                <span v-else
                      class="flex-1 text-center px-4 py-2 bg-muted border border-border rounded-lg text-sm font-medium text-muted-foreground cursor-not-allowed flex items-center justify-center gap-2">
                  <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                  </svg>
                  Coming Soon
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Education Section -->
    <section id="education" class="min-h-screen flex items-center py-24 px-6">
      <div class="max-w-4xl mx-auto">
        <h2 class="text-4xl lg:text-5xl font-bold mb-12">
          <span class="text-gruvbox-orange">Education</span>
        </h2>
        
        <div class="space-y-8">
          <div class="bg-card border-l-4 border-gruvbox-purple rounded-r-xl p-6 shadow-lg hover:shadow-2xl hover:scale-[1.02] transition-all duration-300 cursor-pointer">
            <div class="flex flex-wrap items-start justify-between mb-3">
              <div>
                <h3 class="text-2xl font-bold text-foreground">Bachelor's Degree</h3>
                <p class="text-gruvbox-blue font-semibold">Wolkite University - School of Computer Science and Technology</p>
              </div>
              <span class="text-sm text-muted-foreground">2021 - 2024</span>
            </div>
            <p class="text-muted-foreground leading-relaxed">
              Focused on software engineering, full-stack development, and DevOps practices. 
              Gained comprehensive knowledge in database design, web technologies, and cloud infrastructure.
            </p>
          </div>

        </div>
      </div>
    </section>

    <!-- Skills Section -->
<section id="skills" class="min-h-screen flex items-center py-24 px-6 bg-muted/30">
  <div class="max-w-6xl mx-auto">
    <h2 class="text-4xl lg:text-5xl font-bold mb-3">
      <span class="text-gruvbox-orange">Skills</span>
    </h2>
    <div class="w-20 h-1 bg-gradient-to-r from-gruvbox-orange to-gruvbox-red mb-12"></div>
    
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
      <!-- Left Column -->
      <div class="space-y-12">
        <!-- Programming & Frameworks -->
        <div>
          <div class="flex items-center gap-3 mb-6">
            <svg class="w-5 h-5 text-gruvbox-blue" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4" />
            </svg>
            <h3 class="text-xl font-bold text-gruvbox-blue">Programming & Frameworks</h3>
          </div>
          <div class="flex flex-wrap gap-3">
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-blue hover:text-gruvbox-blue transition-all duration-300 cursor-pointer">React</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-blue hover:text-gruvbox-blue transition-all duration-300 cursor-pointer">ASP.NET</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-blue hover:text-gruvbox-blue transition-all duration-300 cursor-pointer">Angular</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-blue hover:text-gruvbox-blue transition-all duration-300 cursor-pointer">TypeScript</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-blue hover:text-gruvbox-blue transition-all duration-300 cursor-pointer">Node.js</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-blue hover:text-gruvbox-blue transition-all duration-300 cursor-pointer">Flutter</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-blue hover:text-gruvbox-blue transition-all duration-300 cursor-pointer">C#</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-blue hover:text-gruvbox-blue transition-all duration-300 cursor-pointer">Express.js</span>
          </div>
        </div>

        <!-- Database Technologies -->
        <div>
          <div class="flex items-center gap-3 mb-6">
            <svg class="w-5 h-5 text-gruvbox-green" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 7v10c0 2.21 3.582 4 8 4s8-1.79 8-4V7M4 7c0 2.21 3.582 4 8 4s8-1.79 8-4M4 7c0-2.21 3.582-4 8-4s8 1.79 8 4m0 5c0 2.21-3.582 4-8 4s-8-1.79-8-4" />
            </svg>
            <h3 class="text-xl font-bold text-gruvbox-green">Database Technologies</h3>
          </div>
          <div class="flex flex-wrap gap-3">
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-green hover:text-gruvbox-green transition-all duration-300 cursor-pointer">SQL Server</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-green hover:text-gruvbox-green transition-all duration-300 cursor-pointer">PostgreSQL</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-green hover:text-gruvbox-green transition-all duration-300 cursor-pointer">Database Design</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-green hover:text-gruvbox-green transition-all duration-300 cursor-pointer">SQL</span>
          </div>
        </div>

        <!-- Tools & Platforms -->
        <div>
          <div class="flex items-center gap-3 mb-6">
            <svg class="w-5 h-5 text-gruvbox-orange" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
            </svg>
            <h3 class="text-xl font-bold text-gruvbox-orange">Tools & Platforms</h3>
          </div>
          <div class="flex flex-wrap gap-3">
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-orange hover:text-gruvbox-orange transition-all duration-300 cursor-pointer">Docker/Podman</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-orange hover:text-gruvbox-orange transition-all duration-300 cursor-pointer">Visual Studio Code</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-orange hover:text-gruvbox-orange transition-all duration-300 cursor-pointer">Postman</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-orange hover:text-gruvbox-orange transition-all duration-300 cursor-pointer">Visual Studio</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-orange hover:text-gruvbox-orange transition-all duration-300 cursor-pointer">GitHub</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-orange hover:text-gruvbox-orange transition-all duration-300 cursor-pointer">Jenkins</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-orange hover:text-gruvbox-orange transition-all duration-300 cursor-pointer">Git</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-orange hover:text-gruvbox-orange transition-all duration-300 cursor-pointer">IIS</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-orange hover:text-gruvbox-orange transition-all duration-300 cursor-pointer">GitHub Actions</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-orange hover:text-gruvbox-orange transition-all duration-300 cursor-pointer">Terraform</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-orange hover:text-gruvbox-orange transition-all duration-300 cursor-pointer">Ansible</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-orange hover:text-gruvbox-orange transition-all duration-300 cursor-pointer">Prometheus</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-orange hover:text-gruvbox-orange transition-all duration-300 cursor-pointer">Grafana</span>
          </div>
        </div>
      </div>

      <!-- Right Column -->
      <div class="space-y-12">
        <!-- DevOps & Cloud -->
        <div>
          <div class="flex items-center gap-3 mb-6">
            <svg class="w-5 h-5 text-gruvbox-yellow" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 15a4 4 0 004 4h9a5 5 0 10-.1-9.999 5.002 5.002 0 10-9.78 2.096A4.001 4.001 0 003 15z" />
            </svg>
            <h3 class="text-xl font-bold text-gruvbox-yellow">DevOps & Cloud</h3>
          </div>
          <div class="flex flex-wrap gap-3">
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-yellow hover:text-gruvbox-yellow transition-all duration-300 cursor-pointer">Docker</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-yellow hover:text-gruvbox-yellow transition-all duration-300 cursor-pointer">Kubernetes</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-yellow hover:text-gruvbox-yellow transition-all duration-300 cursor-pointer">CI/CD Pipelines</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-yellow hover:text-gruvbox-yellow transition-all duration-300 cursor-pointer">Infrastructure as Code</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-yellow hover:text-gruvbox-yellow transition-all duration-300 cursor-pointer">Containerization</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-yellow hover:text-gruvbox-yellow transition-all duration-300 cursor-pointer">Cloud Platforms</span>
          </div>
        </div>

        <!-- Soft Skills -->
        <div>
          <div class="flex items-center gap-3 mb-6">
            <svg class="w-5 h-5 text-gruvbox-purple" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197m13.5 5.197a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z" />
            </svg>
            <h3 class="text-xl font-bold text-gruvbox-purple">Soft Skills</h3>
          </div>
          <div class="flex flex-wrap gap-3">
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-purple hover:text-gruvbox-purple transition-all duration-300 cursor-pointer">Adaptability</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-purple hover:text-gruvbox-purple transition-all duration-300 cursor-pointer">Continuous Learning</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-purple hover:text-gruvbox-purple transition-all duration-300 cursor-pointer">Communication</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-purple hover:text-gruvbox-purple transition-all duration-300 cursor-pointer">Time Management</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-purple hover:text-gruvbox-purple transition-all duration-300 cursor-pointer">Problem Solving</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-purple hover:text-gruvbox-purple transition-all duration-300 cursor-pointer">Team Collaboration</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-purple hover:text-gruvbox-purple transition-all duration-300 cursor-pointer">Authentication</span>
            <span class="px-4 py-2 bg-card border border-border rounded-lg text-sm font-medium hover:border-gruvbox-purple hover:text-gruvbox-purple transition-all duration-300 cursor-pointer">Security</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

    <!-- Contact Section -->
    <section id="contact" class="min-h-screen flex items-center py-24 px-6">
      <div class="max-w-4xl mx-auto">
        <h2 class="text-4xl lg:text-5xl font-bold mb-3">
          Get In <span class="text-gruvbox-orange">Touch</span>
        </h2>
        <div class="w-20 h-1 bg-gradient-to-r from-gruvbox-orange to-gruvbox-purple mb-8"></div>
        
        <p class="text-lg text-muted-foreground mb-12 leading-relaxed max-w-2xl">
          I'm always open to new opportunities, collaborations, and interesting projects. 
          Whether you have a question or just want to say hi, feel free to reach out!
        </p>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-12">
          <!-- Email Card -->
          <div class="bg-card border border-border rounded-2xl p-6 hover:border-gruvbox-orange hover:shadow-xl transition-all duration-300 hover:-translate-y-1 group">
            <div class="w-12 h-12 bg-gruvbox-red/10 rounded-lg flex items-center justify-center mb-4 group-hover:bg-gruvbox-red/20 transition-colors">
              <svg class="w-6 h-6 text-gruvbox-red" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
              </svg>
            </div>
            <h3 class="text-lg font-bold mb-2">Email</h3>
            <a href="mailto:robelaklilu100@gmail.com" class="text-sm text-muted-foreground hover:text-gruvbox-orange transition-colors break-all">
              robelaklilu100@gmail.com
            </a>
          </div>

          <!-- Phone Card -->
          <div class="bg-card border border-border rounded-2xl p-6 hover:border-gruvbox-green hover:shadow-xl transition-all duration-300 hover:-translate-y-1 group">
            <div class="w-12 h-12 bg-gruvbox-green/10 rounded-lg flex items-center justify-center mb-4 group-hover:bg-gruvbox-green/20 transition-colors">
              <svg class="w-6 h-6 text-gruvbox-green" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
              </svg>
            </div>
            <h3 class="text-lg font-bold mb-2">Phone</h3>
            <a href="tel:+251953244493" class="text-sm text-muted-foreground hover:text-gruvbox-orange transition-colors">
              +251 95 324 4493
            </a>
          </div>

          <!-- Location Card -->
          <div class="bg-card border border-border rounded-2xl p-6 hover:border-gruvbox-blue hover:shadow-xl transition-all duration-300 hover:-translate-y-1 group">
            <div class="w-12 h-12 bg-gruvbox-blue/10 rounded-lg flex items-center justify-center mb-4 group-hover:bg-gruvbox-blue/20 transition-colors">
              <svg class="w-6 h-6 text-gruvbox-blue" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
              </svg>
            </div>
            <h3 class="text-lg font-bold mb-2">Location</h3>
            <p class="text-sm text-muted-foreground">
              Addis Ababa, Ethiopia
            </p>
          </div>
        </div>

        <!-- Action Buttons -->
        <div class="flex flex-wrap gap-4 mt-8">
          <a href="https://mail.google.com/mail/?view=cm&fs=1&to=robelaklilu100@gmail.com" 
             target="_blank"
             class="px-8 py-4 bg-gruvbox-orange text-background rounded-xl font-semibold hover:scale-105 hover:shadow-xl transition-all duration-300 flex items-center gap-2">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
            </svg>
            Get In Touch
          </a>
          <a href="/assets/Robel_Aklilu_CV.pdf" target="_blank"
             class="px-8 py-4 border-2 border-gruvbox-blue text-gruvbox-blue rounded-xl font-semibold hover:bg-gruvbox-blue hover:text-background transition-all duration-300 flex items-center gap-2">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
            </svg>
            View Resume
          </a>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="py-8 px-6 border-t border-border">
      <div class="max-w-7xl mx-auto text-center text-muted-foreground">
        <p>&copy; 2025 Portfolio. Built with Vue.js & Tailwind CSS</p>
      </div>
    </footer>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, h } from 'vue'

const isDark = ref(false)
const activeSection = ref('hero')
const displayedTitle = ref('')
const titles = ['Full Stack Developer', 'DevOps Engineer']
let titleIndex = 0
let charIndex = 0
let isDeleting = false

// Navigation icon components
const HomeIcon = () => h('svg', { fill: 'none', stroke: 'currentColor', viewBox: '0 0 24 24' }, [
  h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', 'stroke-width': '2', d: 'M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6' })
])

const UserIcon = () => h('svg', { fill: 'none', stroke: 'currentColor', viewBox: '0 0 24 24' }, [
  h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', 'stroke-width': '2', d: 'M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z' })
])

const BriefcaseIcon = () => h('svg', { fill: 'none', stroke: 'currentColor', viewBox: '0 0 24 24' }, [
  h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', 'stroke-width': '2', d: 'M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z' })
])

const CodeIcon = () => h('svg', { fill: 'none', stroke: 'currentColor', viewBox: '0 0 24 24' }, [
  h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', 'stroke-width': '2', d: 'M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4' })
])

const MailIcon = () => h('svg', { fill: 'none', stroke: 'currentColor', viewBox: '0 0 24 24' }, [
  h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', 'stroke-width': '2', d: 'M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z' })
])

const navLinks = [
  { id: 'hero', label: 'Home', href: '#hero' },
  { id: 'about', label: 'About', href: '#about' },
  { id: 'experience', label: 'Experience', href: '#experience' },
  { id: 'projects', label: 'Projects', href: '#projects' },
  { id: 'education', label: 'Education', href: '#education' },
  { id: 'skills', label: 'Skills', href: '#skills' },
  { id: 'contact', label: 'Contact', href: '#contact' },
]

const projects = [
  {
    id: 1,
    title: 'Digital Art Store',
    description: 'E-commerce platform for digital art marketplace with seller management, payment processing, and branch operations. Features admin dashboard, artist profiles, and secure payment integration.',
    tech: ['React', 'Node.js', 'Express', 'MongoDB'],
    image: '/images/art_store.png',
    gradient: 'from-gruvbox-red/20 via-gruvbox-orange/20 to-gruvbox-yellow/20',
    github: null,
    demo: 'https://thedigitalartstore.netlify.app',
    isPrivate: false
  },
  {
    id: 2,
    title: 'Ministry of Water and Energy',
    description: 'A centralized web-based system used to collect, manage, and analyze data related to river basins across Ethiopia, supporting informed decision-making and sustainable water resource management.',
    tech: ['Angular', '.NET', 'Microsoft SQL Server'],
    gradient: 'from-gruvbox-aqua/20 via-gruvbox-blue/20 to-gruvbox-purple/20',
    github: null,
    demo: 'http://water.gov.et/',
    isPrivate: true
  },
  {
    id: 3,
    title: 'Petroleum and Energy',
    description: 'An enterprise-level information management system designed to support petroleum and energy sector operations, enabling efficient data collection, monitoring, and reporting for regulatory compliance and strategic planning.',
    tech: ['Angular', '.NET', 'Microsoft SQL Server'],
    gradient: 'from-gruvbox-orange/20 via-gruvbox-red/20 to-gruvbox-yellow/20',
    github: null,
    demo: 'https://ews.pea.gov.et/',
    isPrivate: true
  },
]

const skills = [
  { name: 'Node.js', icon: '🟢', category: 'Backend' },
  { name: 'Next.js', icon: '▲', category: 'Frontend' },
  { name: 'React', icon: '⚛️', category: 'Frontend' },
  { name: 'PostgreSQL', icon: '🐘', category: 'Database' },
  { name: 'MySQL', icon: '🐬', category: 'Database' },
  { name: 'SQLite', icon: '💾', category: 'Database' },
  { name: 'Docker', icon: '🐳', category: 'DevOps' },
  { name: 'Kubernetes', icon: '☸️', category: 'DevOps' },
  { name: 'GitHub Actions', icon: '⚙️', category: 'CI/CD' },
  { name: 'Prometheus', icon: '📊', category: 'Monitoring' },
  { name: 'Grafana', icon: '📈', category: 'Monitoring' },
  { name: 'Terraform', icon: '🏗️', category: 'IaC' },
  { name: 'Ansible', icon: '🔧', category: 'Automation' },
  { name: 'Git', icon: '📦', category: 'Version Control' },
  { name: 'Jest', icon: '🃏', category: 'Testing' },
  { name: 'Playwright', icon: '🎭', category: 'Testing' }
]

const toggleDarkMode = () => {
  isDark.value = !isDark.value
  document.documentElement.classList.toggle('dark')
  localStorage.setItem('theme', isDark.value ? 'dark' : 'light')
}

// Typing effect function
const typeEffect = () => {
  const currentText = titles[titleIndex]
  
  if (!isDeleting && charIndex <= currentText.length) {
    displayedTitle.value = currentText.substring(0, charIndex)
    charIndex++
    setTimeout(typeEffect, 100)
  } else if (!isDeleting && charIndex > currentText.length) {
    // Pause at the end before deleting
    setTimeout(() => {
      isDeleting = true
      typeEffect()
    }, 2000)
  } else if (isDeleting && charIndex > 0) {
    displayedTitle.value = currentText.substring(0, charIndex - 1)
    charIndex--
    setTimeout(typeEffect, 50)
  } else if (isDeleting && charIndex === 0) {
    isDeleting = false
    titleIndex = (titleIndex + 1) % titles.length
    setTimeout(typeEffect, 500)
  }
}

onMounted(() => {
  const savedTheme = localStorage.getItem('theme')
  if (savedTheme === 'dark' || (!savedTheme && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
    isDark.value = true
    document.documentElement.classList.add('dark')
  }

  // Start typing effect
  typeEffect()

  // Intersection Observer for active section tracking
  const sections = document.querySelectorAll('section[id]')
  const observerOptions = {
    root: null,
    rootMargin: '-50% 0px -50% 0px',
    threshold: 0
  }

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        activeSection.value = entry.target.id
      }
    })
  }, observerOptions)

  sections.forEach(section => observer.observe(section))
})
</script>
