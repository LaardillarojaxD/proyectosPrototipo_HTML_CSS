<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dan Sánchez(Software Developer y IoT Specialist)</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;600&family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            black: '#08090d',
                            darkCard: '#11131c',
                            cardBorder: '#1e2235',
                            cyan: '#00f0ff',
                            cyanGlow: 'rgba(0, 240, 255, 0.25)',
                            red: '#ff2a5f',
                            redGlow: 'rgba(255, 42, 95, 0.25)',
                            orangeError: '#ff7700',
                            orangeBg: 'rgba(255, 119, 0, 0.15)',
                            textLight: '#e2e8f0',
                            textMuted: '#94a3b8'
                        }
                    },
                    fontFamily: {
                        sans: ['Plus Jakarta Sans', 'sans-serif'],
                        mono: ['Fira Code', 'monospace']
                    }
                }
            }
        }
        
    </script>

    <style>
        body {
            background-color: #212125;
            color: #e2e8f0;
            overflow-x: hidden;
        }

        /* Dynamic Canvas Styling */
        #bgCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: 0;
            pointer-events: none;
        }

        /* Custom Glows */
        .cyan-glow {
            box-shadow: 0 0 25px rgba(47, 22, 189, 0.2);
        }
        .red-glow {
            box-shadow: 0 0 25px rgba(255, 42, 95, 0.2);
        }
        .cyan-border-glow:focus {
            outline: none;
            border-color: #00f0ff;
            box-shadow: 0 0 15px rgba(0, 240, 255, 0.4);
        }
        
        /* Error state border */
        .input-error {
            border-color: #eb110a !important;
            background-color: rgba(255, 119, 0, 0.08) !important;
            box-shadow: 0 0 15px rgba(255, 5, 5, 0.884) !important;
        }

        .gradient-text-cyan-red {
            background: linear-gradient(135deg, #00f0ff 0%, #ff2a5f 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        /* Glassmorphism */
        .glass-panel {
            background: rgba(17, 19, 28, 0.85);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.07);
        }

        /* Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #08090d;
        }
        ::-webkit-scrollbar-thumb {
            background: #1e2235;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #00f0ff;
        }

        
    </style>
</head> 

<body class="font-sans antialiased relative selection:bg-brand-cyan selection:text-black">

        <!-- Fondo de Canvas Interactivo y Dinámico de mi página -->
    <canvas id="bgCanvas"></canvas>

    <!-- El famoso encabezado de navegación -->
    <header class="sticky top-0 z-50 glass-panel border-b border-brand-cardBorder/50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <a href="#" class="flex items-center gap-3 group">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-brand-cyan to-brand-red p-[2px] transition-transform group-hover:scale-105">
                    <div class="w-full h-full bg-brand-black rounded-[10px] flex items-center justify-center font-mono font-bold text-brand-cyan">
                        DS
                    </div>
                </div>
                <div>
                    <span class="font-bold text-lg text-white tracking-wide block">DAN SÁNCHEZ</span>
                    <span class="text-xs font-mono text-brand-cyan block">DEV // IOT // FUTURO DESARROLLADOR</span>
                </div>
            </a>

            <!-- Desktop Nav -->
            <nav class="hidden md:flex items-center gap-8 font-medium text-sm">
                <a href="#about" class="text-brand-textMuted hover:text-brand-cyan transition-colors">Trayectoria</a>
                <a href="#projects" class="text-brand-textMuted hover:text-brand-cyan transition-colors">Proyectos</a>
                <a href="#recommendations" class="text-brand-textMuted hover:text-brand-cyan transition-colors">Recomendaciones</a>
                <a href="#scrum" class="text-brand-textMuted hover:text-brand-red transition-colors flex items-center gap-1">
                    <i class="fa-solid fa-layer-group text-xs text-brand-red"></i> Scrum y Arch
                </a>
                <a href="#contact" class="px-5 py-2.5 rounded-xl bg-gradient-to-r from-brand-cyan to-blue-600 text-black font-bold hover:opacity-90 transition-all cyan-glow">
                    Contacto
                </a>
            </nav>

            <!-- Mobile Menu Button -->
            <button id="mobileMenuBtn" class="md:hidden text-2xl text-brand-textLight focus:outline-none">
                <i class="fa-solid fa-bars"></i>
            </button>
        </div>

        <!-- Mobile Nav Drawer móviles para visualización -->
        <div id="mobileNav" class="hidden md:hidden glass-panel border-b border-brand-cardBorder px-6 py-4 flex-col gap-4">
            <a href="#about" class="text-brand-textMuted hover:text-brand-cyan">Trayectoria</a>
            <a href="#projects" class="text-brand-textMuted hover:text-brand-cyan">Proyectos</a>
            <a href="#recommendations" class="text-brand-textMuted hover:text-brand-cyan">Recomendaciones</a>
            <a href="#scrum" class="text-brand-textMuted hover:text-brand-red">Scrum & Arquitectura</a>
            <a href="#contact" class="px-5 py-2.5 rounded-xl bg-brand-cyan text-black font-bold text-center">Contacto</a>
        </div>
    </header>

    <!-- conetenedor principal -->
    <main class="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 space-y-28 py-12">

        <!-- sección principal (hero) -->
        <section id="hero" class="pt-6 grid lg:grid-cols-12 gap-12 items-center">
            <div class="lg:col-span-7 space-y-6">
                <div class="inline-flex items-center gap-2 px-3.5 py-1.5 rounded-full glass-panel border border-brand-cyan/30 text-brand-cyan text-xs font-mono">
                    <span class="w-2 h-2 rounded-full bg-brand-cyan animate-ping"></span>
                    DISPONIBLE PARA PRÁCTICAS Y PROYECTOS DE SOFTWARE
                </div>

                <h1 class="text-4xl sm:text-6xl font-extrabold tracking-tight leading-tight">
                    Construyendo software con visión de <span class="gradient-text-cyan-red">Product Owner y metodología</span>.
                </h1>

                <p class="text-lg text-brand-textMuted leading-relaxed max-w-2xl">
                    Hola, me llamo <strong class="text-white">Dan (Daniel Abraham Sánchez Bravo)

                    </strong>. Desarrollador en formación continua (último año de Ingeniería en Software), especialista en soluciones Back Office, integración IoT y arquitectura de datos con Spring Boot y MongoDB. Como MYSQL Workbench y SQL Server, así como Paquetería Office.
                </p>

                <div class="p-4 rounded-2xl glass-panel border-l-4 border-l-brand-red bg-brand-darkCard/60 space-y-2">
                    <div class="text-xs font-mono text-brand-red uppercase tracking-wider font-semibold">
                        <i class="fa-solid fa-bullseye mr-1"></i> Mi Misión
                    </div>
                    <p class="text-sm text-slate-300 italic">
                        "Construir la comunicación para generar la confianza de mis colaboradores y de esta forma poder desarrollar sus habilidades a nivel profesional, fomentando el desarrollo del proyecto y la mejora continua."
                    </p>
                </div> 
                
                <div class="p-4 rounded-2xl glass-panel border-l-4 border-l-brand-red bg-brand-darkCard/60 space-y-2">
                    <div class="text-xs font-mono text-brand-red uppercase tracking-wider font-semibold">
                        <i class="fa-solid fa-bullseye mr-1"></i> Mi Visión
                    </div>
                    <p class="text-sm text-slate-300 italic">
                        "Ser un desarrollador de software con visión de Product Owner, capaz de liderar equipos y proyectos, fomentando la innovación y la mejora continua en el desarrollo de soluciones tecnológicas."
                    </p>

                </div>

                <div class="flex flex-wrap gap-4 pt-2">
                    <a href="#contact" class="px-6 py-3.5 rounded-xl bg-brand-cyan text-black font-bold flex items-center gap-2 hover:bg-cyan-300 transition-all cyan-glow">
                        <i class="fa-solid fa-paper-plane"></i> Aquí pueden dejar sus datos :D
                    </a>
                    <a href="#scrum" class="px-6 py-3.5 rounded-xl glass-panel text-white font-semibold flex items-center gap-2 hover:border-brand-red transition-all hover:text-brand-red">
                        <i class="fa-solid fa-diagram-project"></i> Plan Scrum & API
                    </a>
                </div>

                <!-- Fast Stack Tech Badges -->
                <div class="pt-4 flex flex-wrap items-center gap-3 text-xs font-mono text-brand-textMuted">
                    <span>Tecnologías que domino:</span>
                    <span class="px-2.5 py-1 rounded-md bg-brand-darkCard border border-brand-cardBorder text-brand-cyan">Java Spring Boot</span>
                    <span class="px-2.5 py-1 rounded-md bg-brand-darkCard border border-brand-cardBorder text-green-400">MongoDB</span>
                    <span class="px-2.5 py-1 rounded-md bg-brand-darkCard border border-brand-cardBorder text-yellow-400">Python</span>
                    <span class="px-2.5 py-1 rounded-md bg-brand-darkCard border border-brand-cardBorder text-blue-400">SQL Server & MySQL</span>
                    <span class="px-2.5 py-1 rounded-md bg-brand-darkCard border border-brand-cardBorder text-brand-red">Git / GitLab</span>
                    <span class="px-2.5 py-1 rounded-md bg-brand-darkCard border border-brand-cardBorder text-purple-400">Office Microsoft</span>
                    <span class="px-2.5 py-1 rounded-md bg-brand-darkCard border border-brand-cardBorder text-brand-cyan">Cisco CNNA</span>
                    <span class="px-2.5 py-1 rounded-md bg-brand-darkCard border border-brand-cardBorder text-brand-cyan">IoT y Telemetría como monitoreo</span>
                    <span class="px-2.5 py-1 rounded-md bg-brand-darkCard border border-brand-cardBorder text-brand-cyan">Desarrollo Web</span>
                    <span class="px-2.5 py-1 rounded-md bg-brand-darkCard border border-brand-cardBorder text-brand-cyan">CRM como salesforce y SAP</span>
                    <SPAN class="px-2.5 py-1 rounded-md bg-brand-darkCard border border-brand-cardBorder text-brand-cyan">Scrum y Metodologías Ágiles y de empresas</SPAN>
                    <span class="px-2.5 py-1 rounded-md bg-brand-darkCard border border-brand-cardBorder text-brand-cyan">Actualmente aprendiendo Android...</span>
                </div>
            </div>

            <!-- Profile / IoT Tech Display Card -->
            <div class="lg:col-span-5">
                <div class="relative group">
                    <div class="absolute -inset-1 bg-gradient-to-r from-brand-cyan to-brand-red rounded-3xl blur opacity-30 group-hover:opacity-60 transition duration-1000"></div>
                    <div class="relative glass-panel rounded-3xl p-6 space-y-6">
                        <div class="flex items-center justify-between border-b border-brand-cardBorder pb-4">
                            <div class="flex items-center gap-3">
                                 <div class="w-12 h-12 rounded-full bg-gradient-to-tr from-brand-cyan to-brand-red flex items-center justify-center text-xl text-black font-bold overflow-hidden">
                                    <img id="profilePhotoDisplay" src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='%2300f0ff'%3E%3Cpath d='M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z'/%3E%3C/svg%3E" alt="Foto de perfil" class="w-full h-full object-cover">
                                </div>
                                <!-- Carga de foto de perfil -->
                        <div class="space-y-3 pt-4 border-t border-brand-cardBorder">
                            <label class="block text-xs font-mono text-brand-textMuted mb-2">
                                <i class="fa-solid fa-camera mr-1"></i> SUBIR FOTO DE PERFIL
                            </label>
                            <input type="file" id="profilePhotoInput" accept="image/*" class="w-full px-3 py-2 rounded-lg bg-brand-black/80 border border-brand-cardBorder text-white text-xs file:mr-3 file:py-1.5 file:px-3 file:rounded file:border-0 file:text-xs file:font-semibold file:bg-brand-cyan file:text-black hover:file:opacity-90 cursor-pointer">
                            <small class="text-[10px] text-brand-cyan block">JPG, PNG o GIF (máx 2MB)</small>
                        </div>
                                <div>
                                    <h3 class="font-bold text-white">Dan Sánchez</h3>
                                    <p class="text-xs text-brand-cyan font-mono">Ingeniería en Desarrollo de Software</p>
                                </div>
                            </div>
                            <span class="px-3 py-1 text-xs font-mono rounded-full bg-emerald-950 text-emerald-400 border border-emerald-800">
                                B2 Inglés
                            </span>
                        </div>

                        <!-- Mini Stats / Key Specs -->
                        <div class="grid grid-cols-2 gap-4">
                            <div class="p-3 rounded-xl bg-brand-black/60 border border-brand-cardBorder">
                                <span class="text-xs text-brand-textMuted block">Enfoque Actual</span>
                                <span class="font-semibold text-sm text-brand-cyan">IoT y Back Office</span>
                            </div>
                            <div class="p-3 rounded-xl bg-brand-black/60 border border-brand-cardBorder">
                                <span class="text-xs text-brand-textMuted block">Especialización</span>
                                <span class="font-semibold text-sm text-brand-red">Java y Spring Boot</span>
                            </div>
                            <div class="p-3 rounded-xl bg-brand-black/60 border border-brand-cardBorder">
                                <span class="text-xs text-brand-textMuted block">Base de Datos</span>
                                <span class="font-semibold text-sm text-green-400">MongoDB / SQL</span>
                            </div>
                            <div class="p-3 rounded-xl bg-brand-black/60 border border-brand-cardBorder">
                                <span class="text-xs text-brand-textMuted block">Meta Profesional</span>
                                <span class="font-semibold text-sm text-purple-400">Product Owner</span>
                            </div>
                        </div>

                        <div class="p-4 rounded-xl bg-brand-black/80 font-mono text-xs text-slate-300 space-y-1 border border-brand-cardBorder">
                            <div class="text-brand-cyan">Contacto Directo(De preferencia por medio de whats, para saber que me están buscando)</div>
                            <div>Email: <a href="mailto:dasanchezb@powerfleet.com" class="text-white underline">dasanchezb@powerfleet.com</a></div>
                            <div>Email: <a href="mailto:daniosion@outlook.es" class="text-white underline">daniosion@outlook.es</a></div>
                            <div>WhatsApp: <a href="https://wa.me/525629130682" target="_blank" class="text-emerald-400">5629130682</a></div>
                            <div>Mi personal WhatsApp: <a href="https://wa.me/525629130682" target="_blank" class="text-emerald-400">5629130682</a></div>
                            <div>Ubicación: <span class="text-slate-400">Ciudad de México, CDMX</span></div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- CAREER TRAJECTORY & EXPERIENCE SECTION -->
        <section id="about" class="space-y-10">
            <div class="border-l-4 border-brand-cyan pl-4">
                <h2 class="text-3xl font-extrabold text-white">Trayectoria y Experiencia</h2>
                <p class="text-brand-textMuted text-sm">Evolución profesional combinando soporte operativo, análisis de datos y desarrollo de software.</p>
            </div>

            <div class="relative border-l-2 border-brand-cardBorder ml-4 space-y-12">

                <!-- Job 1 -->
                <div class="relative pl-8 group">
                    <div class="absolute -left-[9px] top-1.5 w-4 h-4 rounded-full bg-brand-cyan group-hover:scale-125 transition-transform cyan-glow"></div>
                    <div class="glass-panel p-6 rounded-2xl space-y-3 hover:border-brand-cyan/50 transition-colors">
                        <div class="flex flex-wrap items-center justify-between gap-2">
                            <div>
                                <h3 class="text-xl font-bold text-white">Administrativo Soporte Técnico & IoT Back Office</h3>
                                <span class="text-brand-cyan font-mono text-sm">PowerFleet — Ciudad de México</span>
                            </div>
                            <span class="px-3 py-1 rounded-full bg-brand-cyan/10 text-brand-cyan text-xs font-mono border border-brand-cyan/30">
                                Abril 2025 – Presente
                            </span>
                        </div>
                        <p class="text-sm text-slate-300 leading-relaxed">
                            Apoyo especializado a técnicos en la configuración de equipos GPS, actualización de protocolos de firmware y verificación continua para monitoreo 24/7. Instalación y validación de hardware especializado (cámaras, sensores, jammers y tracking). Gestión de datos con SQL Workbench y Server.
                        </p>
                        <div class="flex flex-wrap gap-2 pt-2">
                            <span class="px-2.5 py-1 rounded bg-brand-black text-xs font-mono text-slate-400 border border-brand-cardBorder">Dispositivos IoT</span>
                            <span class="px-2.5 py-1 rounded bg-brand-black text-xs font-mono text-slate-400 border border-brand-cardBorder">MySQL / SQL Server</span>
                            <span class="px-2.5 py-1 rounded bg-brand-black text-xs font-mono text-slate-400 border border-brand-cardBorder">Protocolos de Monitoreo</span>
                        </div>
                    </div>
                </div>

                <!-- Job 2 -->
                <div class="relative pl-8 group">
                    <div class="absolute -left-[9px] top-1.5 w-4 h-4 rounded-full bg-brand-red group-hover:scale-125 transition-transform red-glow"></div>
                    <div class="glass-panel p-6 rounded-2xl space-y-3 hover:border-brand-red/50 transition-colors">
                        <div class="flex flex-wrap items-center justify-between gap-2">
                            <div>
                                <h3 class="text-xl font-bold text-white">Analista Back Office (Tienda en Línea Samsung)</h3>
                                <span class="text-brand-red font-mono text-sm">Samsung / Atento — Insurgentes, CDMX</span>
                            </div>
                            <span class="px-3 py-1 rounded-full bg-brand-red/10 text-brand-red text-xs font-mono border border-brand-red/30">
                                Septiembre 2023 – Febrero 2025
                            </span>
                        </div>
                        <p class="gradient-text-cyan-red">
                            Análisis y pronósticos mediante cruce de datos complejos y tablas dinámicas en Excel avanzado. Generación de reportes de resolución para e-Commerce, atención de casos de estudio críticos y soporte directo a mesas de ayuda de compras.
                        </p>
                        <div class="flex flex-wrap gap-2 pt-2">
                            <span class="px-2.5 py-1 rounded bg-brand-black text-xs font-mono text-slate-400 border border-brand-cardBorder">Excel Avanzado</span>
                            <span class="px-2.5 py-1 rounded bg-brand-black text-xs font-mono text-slate-400 border border-brand-cardBorder">Cruces de Datos</span>
                            <span class="px-2.5 py-1 rounded bg-brand-black text-xs font-mono text-slate-400 border border-brand-cardBorder">Casos de Estudio</span>
                        </div>
                    </div>
                </div>

                <!-- Job 3 -->
                <div class="relative pl-8 group">
                    <div class="absolute -left-[9px] top-1.5 w-4 h-4 rounded-full bg-slate-600 group-hover:scale-125 transition-transform"></div>
                    <div class="glass-panel p-6 rounded-2xl space-y-3 hover:border-slate-500 transition-colors">
                        <div class="flex flex-wrap items-center justify-between gap-2">
                            <div>
                                <h3 class="text-xl font-bold text-white">Asesor Telefónico / CHAT — Mesa de Ayuda</h3>
                                <span class="text-slate-400 font-mono text-sm">MAPFRE — Ciudad de México</span>
                            </div>
                            <span class="px-3 py-1 rounded-full bg-slate-800 text-slate-300 text-xs font-mono border border-slate-700">
                                Noviembre 2021 – Mayo 2023
                            </span>
                        </div>
                        <p class="text-sm text-slate-300 leading-relaxed">
                            Atención al cliente técnica y administrativa. Procesamiento de endosos, seguimiento a ajustes de deducibles como coasegurador y gestión de reembolsos proporcionales de pólizas.
                        </p>
                    </div>
                </div> 
                <div class="relative pl-8 group">
                    <div class="absolute -left-[10px] top-1.5 w-4 h-4 rounded-full bg-slate-600 group-hover:scale-125 transition-transform"></div>
                    <div class="glass-panel p-6 rounded-2xl space-y-3 hover:border-slate-500 transition-colors">
                        <div class="flex flex-wrap items-center justify-between gap-2">
                            <div>
                                <h3 class="text-xl font-bold text-white">Asesor Telefónico / CHAT — Mesa de Ayuda TKM(ITalika)</h3>
                                <span class="text-slate-400 font-mono text-sm">TKM — Ciudad de México</span>
                            </div>
                            <span class="px-3 py-1 rounded-full bg-slate-800 text-slate-300 text-xs font-mono border border-slate-700">
                                 Septiembre 2018 – septiembre 2021
                            </span>
                        </div>
                        <p class="gradient-text-cyan-red">
                        Atención chat y administrativa. Ventas de unidades, contizaciones, seguimientos de refacciones como de entrega de motocicletas
                        
                    </p>
                 </div>
                 <div>
                    <h2>
                    <div class="flex flex-wrap gap-8 pt-2">
                    <a href="#contact" class="px-6 py-3.5 rounded-xl bg-brand-cyan text-black font-bold flex items-center gap-2 hover:bg-cyan-300 transition-all cyan-glow">
                        <i class="fa-solid fa-paper-plane"></i> Si desean conocer más de mi vida profesional y lo que me gusta como fotos
                    </a>
                </div>
                    </h2>
                 </div>
                    
                </div>



                <!-- Education -->
                <div class="relative pl-8 group">
                    <div class="absolute -left-[9px] top-1.5 w-4 h-4 rounded-full bg-purple-500 group-hover:scale-125 transition-transform"></div>
                    <div class="glass-panel p-6 rounded-2xl space-y-3 border-purple-900/50">
                        <div class="flex flex-wrap items-center justify-between gap-2">
                            <div>
                                <h3 class="text-xl font-bold text-white">Ingeniería en Desarrollo de Software</h3>
                                <span class="text-purple-400 font-mono text-sm">Universidad virtual del Estado de Guanajuato (UvEG)</span>
                            </div>
                            <span class="px-3 py-1 rounded-full bg-purple-950 text-purple-300 text-xs font-mono border border-purple-800">
                                En Curso — Último Año
                            </span>
                        </div>
                        <p class="text-sm text-slate-300">
                            Formación integral en programación orientada a objetos, bases de datos no relacionales, análisis de requerimientos y metodologías ágiles.
                        </p>
                    </div>
                </div>

            </div>
        </section>

        <!-- PROJECTS GALLERY SECTION -->
        <section id="projects" class="space-y-10">
            <div class="flex flex-wrap items-end justify-between gap-4 border-l-4 border-brand-red pl-4">
                <div>
                    <h2 class="text-3xl font-extrabold text-white">Proyectos Destacados</h2>
                    <p class="text-brand-textMuted text-sm">Desarrollo de software, automatización e integración con bases de datos.</p>
                </div>
                <div class="font-mono text-xs text-brand-cyan">
                    // FILTRAR POR STACK: ALL / JAVA / MONGO
                </div>
            </div>

            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">

                <!-- Project Card 1 -->
                <div class="glass-panel rounded-2xl overflow-hidden group hover:border-brand-cyan transition-all flex flex-col justify-between">
                    <div>
                        <div class="h-48 bg-gradient-to-br from-slate-900 via-brand-darkCard to-cyan-950 p-6 flex flex-col justify-between relative overflow-hidden border-b border-brand-cardBorder">
                            <div class="absolute top-0 right-0 w-32 h-32 bg-brand-cyan/10 rounded-full blur-2xl"></div>
                            <span class="px-3 py-1 rounded-full bg-black/60 text-brand-cyan text-xs font-mono w-fit border border-brand-cyan/30">
                                Ciberseguridad & POO
                            </span>
                            <i class="fa-solid fa-shield-halved text-5xl text-brand-cyan/40 group-hover:text-brand-cyan transition-colors"></i>
                        </div>
                        <div class="p-6 space-y-3">
                            <h3 class="text-xl font-bold text-white group-hover:text-brand-cyan transition-colors">ANALIA Assistant</h3>
                            <p class="text-xs text-brand-textMuted leading-relaxed">
                                Arquitectura y desarrollo en Java para un asistente orientado a ciberseguridad, privacidad de datos y protección de credenciales aplicando principios avanzados de POO.
                            </p>
                        </div>
                    </div>
                    <div class="p-6 pt-0 flex items-center gap-2 text-xs font-mono text-slate-400">
                        <span class="px-2 py-1 rounded bg-brand-black border border-brand-cardBorder">Java</span>
                        <span class="px-2 py-1 rounded bg-brand-black border border-brand-cardBorder">POO</span>
                        <span class="px-2 py-1 rounded bg-brand-black border border-brand-cardBorder">Security</span>
                    </div>
                </div>

                <!-- Project Card 2 -->
                <div class="glass-panel rounded-2xl overflow-hidden group hover:border-brand-red transition-all flex flex-col justify-between">
                    <div>
                        <div class="h-48 bg-gradient-to-br from-slate-900 via-brand-darkCard to-red-950 p-6 flex flex-col justify-between relative overflow-hidden border-b border-brand-cardBorder">
                            <div class="absolute top-0 right-0 w-32 h-32 bg-brand-red/10 rounded-full blur-2xl"></div>
                            <span class="px-3 py-1 rounded-full bg-black/60 text-brand-red text-xs font-mono w-fit border border-brand-red/30">
                                IoT & Monitoreo
                            </span>
                            <i class="fa-solid fa-satellite-dish text-5xl text-brand-red/40 group-hover:text-brand-red transition-colors"></i>
                        </div>
                        <div class="p-6 space-y-3">
                            <h3 class="text-xl font-bold text-white group-hover:text-brand-red transition-colors">IoT Fleet Telemetry Monitor</h3>
                            <p class="text-xs text-brand-textMuted leading-relaxed">
                                Plataforma de simulación de telemetría para rastreo vehicular, ingesta de eventos de sensores (jammers, cámaras) y persistencia en documentos MongoDB.
                            </p>
                        </div>
                    </div>
                    <div class="p-6 pt-0 flex items-center gap-2 text-xs font-mono text-slate-400">
                        <span class="px-2 py-1 rounded bg-brand-black border border-brand-cardBorder">MongoDB</span>
                        <span class="px-2 py-1 rounded bg-brand-black border border-brand-cardBorder">IoT</span>
                        <span class="px-2 py-1 rounded bg-brand-black border border-brand-cardBorder">Spring Boot</span>
                    </div>
                </div>

                <!-- Project Card 3 -->
                <div class="glass-panel rounded-2xl overflow-hidden group hover:border-emerald-500 transition-all flex flex-col justify-between">
                    <div>
                        <div class="h-48 bg-gradient-to-br from-slate-900 via-brand-darkCard to-emerald-950 p-6 flex flex-col justify-between relative overflow-hidden border-b border-brand-cardBorder">
                            <div class="absolute top-0 right-0 w-32 h-32 bg-emerald-500/10 rounded-full blur-2xl"></div>
                            <span class="px-3 py-1 rounded-full bg-black/60 text-emerald-400 text-xs font-mono w-fit border border-emerald-800">
                                Fullstack Portfolio
                            </span>
                            <i class="fa-solid fa-database text-5xl text-emerald-500/40 group-hover:text-emerald-400 transition-colors"></i>
                        </div>
                        <div class="p-6 space-y-3">
                            <h3 class="text-xl font-bold text-white group-hover:text-emerald-400 transition-colors">Recruiter Mongo Engine</h3>
                            <p class="text-xs text-brand-textMuted leading-relaxed">
                                Aplicación web responsiva con formulario de comentarios para reclutadores, integración REST API en Java Spring Boot y almacenamiento en MongoDB.
                            </p>
                        </div>
                    </div>
                    <div class="p-6 pt-0 flex items-center gap-2 text-xs font-mono text-slate-400">
                        <span class="px-2 py-1 rounded bg-brand-black border border-brand-cardBorder">Spring Data Mongo</span>
                        <span class="px-2 py-1 rounded bg-brand-black border border-brand-cardBorder">AJAX</span>
                    </div>
                </div>

            </div>
        </section>

        <!-- RECOMMENDATIONS & ENDORSEMENTS SECTION -->
        <section id="recommendations" class="space-y-10">
            <div class="border-l-4 border-brand-cyan pl-4">
                <h2 class="text-3xl font-extrabold text-white">Recomendaciones e Impacto</h2>
                <p class="text-brand-textMuted text-sm">Comentarios sobre liderazgo empático, trabajo en equipo y resolución técnica.</p>
            </div>

            <div class="grid md:grid-cols-2 gap-6" id="recommendationsContainer">
                <!-- Static Recommendation 1 -->
                <div class="glass-panel p-6 rounded-2xl space-y-4 border-brand-cardBorder relative">
                    <i class="fa-solid fa-quote-right absolute top-6 right-6 text-3xl text-slate-800"></i>
                    <p class="text-sm text-slate-300 italic">
                        "Dan demuestra un alto compromiso con la calidad operativa y la comunicación clara. Su capacidad para traducir requerimientos complejos de Back Office a soluciones ordenadas inspira mucha confianza."
                    </p>
                    <div class="flex items-center gap-3 pt-2">
                        <div class="w-10 h-10 rounded-full bg-brand-cyan/20 border border-brand-cyan flex items-center justify-center font-bold text-brand-cyan text-sm">
                            LR
                        </div>
                        <div>
                            <div class="font-bold text-sm text-white">Líder de Operaciones IoT</div>
                            <div class="text-xs text-brand-textMuted">Sector Telemetría & GPS</div>
                        </div>
                    </div>
                </div>

                <!-- Static Recommendation 2 -->
                <div class="glass-panel p-6 rounded-2xl space-y-4 border-brand-cardBorder relative">
                    <i class="fa-solid fa-quote-right absolute top-6 right-6 text-3xl text-slate-800"></i>
                    <p class="text-sm text-slate-300 italic">
                        "Poseo un liderazgo empático natural. En el análisis de datos y seguimiento de casos críticos, su dinamismo y autoconciencia destacan en cada entrega."
                    </p>
                    <div class="flex items-center gap-3 pt-2">
                        <div class="w-10 h-10 rounded-full bg-brand-red/20 border border-brand-red flex items-center justify-center font-bold text-brand-red text-sm">
                            CS
                        </div>
                        <div>
                            <div class="font-bold text-sm text-white">Coordinador Back Office</div>
                            <div class="text-xs text-brand-textMuted">E-Commerce & Support</div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- RECRUITER CONTACT FORM SECTION (CONNECTED TO MONGO DATA MODEL) -->
        <section id="contact" class="space-y-8">
            <div class="border-l-4 border-brand-red pl-4">
                <h2 class="text-3xl font-extrabold text-white">Contacto para Reclutadores y Comentarios</h2>
                <p class="text-brand-textMuted text-sm">Ingresa tus datos de contacto para coordinar entrevistas o vacantes de software / prácticas.</p>
            </div>

            <div class="grid lg:grid-cols-12 gap-8 items-start">
                
                <!-- Form Box -->
                <div class="lg:col-span-7 glass-panel p-8 rounded-3xl space-y-6 relative border-brand-cardBorder">
                    
                    <!-- Notification Alert Box (Error state: ORANGE / Success: GREEN) -->
                    <div id="formAlert" class="hidden p-4 rounded-xl text-sm font-medium transition-all duration-300"></div>

                    <form id="recruiterForm" class="space-y-5" onsubmit="handleFormSubmit(event)" novalidate>
                        <div class="grid sm:grid-cols-2 gap-5">
                            <div>
                                <label class="block text-xs font-mono text-brand-textMuted mb-2">NOMBRE COMPLETO *</label>
                                <input type="text" id="recruiterName" class="w-full px-4 py-3 rounded-xl bg-brand-black/80 border border-brand-cardBorder text-white text-sm cyan-border-glow transition-all" placeholder="Ej. Ana Martínez">
                            </div>
                            <div>
                                <label class="block text-xs font-mono text-brand-textMuted mb-2">EMPRESA / EMPLEADOR *</label>
                                <input type="text" id="companyName" class="w-full px-4 py-3 rounded-xl bg-brand-black/80 border border-brand-cardBorder text-white text-sm cyan-border-glow transition-all" placeholder="Ej. Tech Solutions">
                            </div>
                        </div>

                        <div class="grid sm:grid-cols-2 gap-5">
                            <div>
                                <label class="block text-xs font-mono text-brand-textMuted mb-2">CORREO ELECTRÓNICO *</label>
                                <input type="email" id="recruiterEmail" class="w-full px-4 py-3 rounded-xl bg-brand-black/80 border border-brand-cardBorder text-white text-sm cyan-border-glow transition-all" placeholder="reclutador@empresa.com">
                            </div>
                            <div>
                                <label class="block text-xs font-mono text-brand-textMuted mb-2">TELÉFONO / WHATSAPP</label>
                                <input type="tel" id="recruiterPhone" class="w-full px-4 py-3 rounded-xl bg-brand-black/80 border border-brand-cardBorder text-white text-sm cyan-border-glow transition-all" placeholder="+52 55 0000 0000">
                            </div>
                        </div>

                        <div>
                            <label class="block text-xs font-mono text-brand-textMuted mb-2">TIPO DE OPORTUNIDAD</label>
                            <select id="opportunityType" class="w-full px-4 py-3 rounded-xl bg-brand-black/80 border border-brand-cardBorder text-white text-sm cyan-border-glow transition-all">
                                <option value="practicas">Prácticas Profesionales en Software</option>
                                <option value="jr_developer">Desarrollador Jr Java / Spring Boot</option>
                                <option value="po_trainee">Product Owner Trainee / Jr</option>
                                <option value="iot_backoffice">Análisis IoT / Back Office Especializado</option>
                            </select>
                        </div>

                        <div>
                            <label class="block text-xs font-mono text-brand-textMuted mb-2">MENSAJE O COMENTARIOS *</label>
                            <textarea id="recruiterComment" rows="4" class="w-full px-4 py-3 rounded-xl bg-brand-black/80 border border-brand-cardBorder text-white text-sm cyan-border-glow transition-all" placeholder="Escribe aquí los detalles de la propuesta o consulta..."></textarea>
                        </div>

                        <button type="submit" class="w-full py-4 rounded-xl bg-gradient-to-r from-brand-cyan to-brand-red text-black font-extrabold text-base hover:opacity-90 transition-all cyan-glow flex items-center justify-center gap-2">
                            <i class="fa-solid fa-database"></i> GUARDAR EN MONGO DB & ENVIAR
                        </button>
                    </form>
                </div>

                <!-- MongoDB Live Payload Simulator Box -->
                <div class="lg:col-span-5 glass-panel p-6 rounded-3xl space-y-4 border-brand-cardBorder">
                    <div class="flex items-center justify-between border-b border-brand-cardBorder pb-3">
                        <span class="text-xs font-mono text-green-400 flex items-center gap-2">
                            <i class="fa-solid fa-server"></i> MONGO DB DOCUMENT SIMULATOR
                        </span>
                        <span class="text-[10px] font-mono text-slate-500">spring-data-mongodb</span>
                    </div>

                    <p class="text-xs text-brand-textMuted">
                        JSON es de cajo con mongo, los datos se mapean exactamente al documento MongoDB que procesa el backend en Spring Boot:
                    </p>

                    <pre class="p-4 rounded-xl bg-brand-black text-[11px] font-mono text-brand-cyan overflow-x-auto border border-brand-cardBorder leading-relaxed" id="mongoPreview">
{
  "_id": "66bc8a90f12c8a0012a9b3f1",
  "recruiterName": "Pendiente...",
  "company": "Pendiente...",
  "email": "Pendiente...",
  "opportunityType": "practicas",
  "comment": "Esperando input...",
  "createdAt": "2026-08-12T02:00:00Z",
  "status": "NEW_LEAD"
}
                    </pre>

                    <div class="p-3 rounded-xl bg-brand-orangeBg border border-brand-orangeError/40 text-xs text-orange-300 flex items-start gap-2">
                        <i class="fa-solid fa-triangle-exclamation text-brand-orangeError mt-0.5"></i>
                        <span><strong>Manejo de Errores:</strong> Si faltan campos requeridos, el sistema activará alertas en color naranja acorde a las especificaciones visuales.</span>
                    </div>
                </div>

            </div>
        </section>

        <!-- SCRUM & TECHNICAL ARCHITECTURE HUB -->
        <section id="scrum" class="space-y-8 pt-6">
            <div class="border-l-4 border-brand-cyan pl-4">
                <h2 class="text-3xl font-extrabold text-white">Plan Metodológico Scrum & Backend Java/Mongo</h2>
                <p class="text-brand-textMuted text-sm">Estructura del backlog, historias de usuario y código Spring Boot listo para producción.</p>
            </div>

            <!-- Tabs Navigation -->
            <div class="flex border-b border-brand-cardBorder gap-4">
                <button onclick="switchTab('backlog')" id="tabBtn-backlog" class="pb-3 text-sm font-bold border-b-2 border-brand-cyan text-brand-cyan">
                    <i class="fa-solid fa-list-check mr-1"></i> Scrum Backlog (Sprints)
                </button>
                <button onclick="switchTab('code')" id="tabBtn-code" class="pb-3 text-sm font-bold border-b-2 border-transparent text-slate-400 hover:text-white">
                    <i class="fa-solid fa-code mr-1"></i> Java Spring Boot & Mongo Code
                </button>
            </div>

            <!-- Tab Content 1: Scrum Backlog -->
            <div id="tabContent-backlog" class="space-y-6">
                <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-4">
                    
                    <!-- Sprint 1 -->
                    <div class="glass-panel p-5 rounded-2xl border-brand-cardBorder space-y-3">
                        <div class="flex justify-between items-center">
                            <span class="text-xs font-mono font-bold text-brand-cyan">SPRINT 1</span>
                            <span class="text-[10px] px-2 py-0.5 rounded bg-emerald-950 text-emerald-400">Completado</span>
                        </div>
                        <h4 class="font-bold text-white text-sm">Arquitectura & Setup Inicial</h4>
                        <ul class="text-xs text-brand-textMuted space-y-1.5 list-disc list-inside">
                            <li>Configuración Spring Boot 3 + Spring Data MongoDB.</li>
                            <li>Definición de paleta visual (Negro, Cyan, Rojo, Naranja).</li>
                            <li>Modelado de Documentos Mongo.</li>
                        </ul>
                    </div>

                    <!-- Sprint 2 -->
                    <div class="glass-panel p-5 rounded-2xl border-brand-cardBorder space-y-3">
                        <div class="flex justify-between items-center">
                            <span class="text-xs font-mono font-bold text-brand-cyan">SPRINT 2</span>
                            <span class="text-[10px] px-2 py-0.5 rounded bg-cyan-950 text-brand-cyan">En Curso</span>
                        </div>
                        <h4 class="font-bold text-white text-sm">Endpoints de Contacto & UI</h4>
                        <ul class="text-xs text-brand-textMuted space-y-1.5 list-disc list-inside">
                            <li>API REST `/api/v1/contacts` para guardar prospectos.</li>
                            <li>Validación de errores con alertas en Naranja.</li>
                            <li>Seccionado de Trayectoria e IoT.</li>
                        </ul>
                    </div>

                    <!-- Sprint 3 -->
                    <div class="glass-panel p-5 rounded-2xl border-brand-cardBorder space-y-3">
                        <div class="flex justify-between items-center">
                            <span class="text-xs font-mono font-bold text-brand-red">SPRINT 3</span>
                            <span class="text-[10px] px-2 py-0.5 rounded bg-slate-800 text-slate-400">Planeado</span>
                        </div>
                        <h4 class="font-bold text-white text-sm">Módulo de Recomendaciones</h4>
                        <ul class="text-xs text-brand-textMuted space-y-1.5 list-disc list-inside">
                            <li>CRUD de recomendaciones profesionales.</li>
                            <li>Manejo de estados (Aprobado/Pendiente).</li>
                            <li>Integración de carga de imágenes de proyectos.</li>
                        </ul>
                    </div>

                    <!-- Sprint 4 -->
                    <div class="glass-panel p-5 rounded-2xl border-brand-cardBorder space-y-3">
                        <div class="flex justify-between items-center">
                            <span class="text-xs font-mono font-bold text-brand-red">SPRINT 4</span>
                            <span class="text-[10px] px-2 py-0.5 rounded bg-slate-800 text-slate-400">Planeado</span>
                        </div>
                        <h4 class="font-bold text-white text-sm">Dashboard de Reclutador (PO)</h4>
                        <ul class="text-xs text-brand-textMuted space-y-1.5 list-disc list-inside">
                            <li>Panel administrativo protegido para Dan.</li>
                            <li>Métricas de contactos y filtrado por vacante.</li>
                            <li>Despliegue continuo en Nube.</li>
                        </ul>
                    </div>

                </div>
            </div>

            <!-- Tab Content 2: Java Spring Boot & Mongo Code -->
            <div id="tabContent-code" class="hidden space-y-4">
                <div class="glass-panel p-6 rounded-2xl border-brand-cardBorder space-y-4">
                    <div class="flex items-center justify-between">
                        <h4 class="font-bold text-white text-sm font-mono text-brand-cyan">1. Document Model (Spring Data Mongo)</h4>
                        <span class="text-xs font-mono text-slate-500">ContactDocument.java</span>
                    </div>
                    <pre class="p-4 rounded-xl bg-brand-black text-xs font-mono text-slate-300 overflow-x-auto leading-relaxed border border-brand-cardBorder">
@Document(collection = "recruiter_contacts")
@Data
@NoArgsConstructor
@AllArgsConstructor
public class ContactDocument {
    @Id
    private String id;
    
    @NotNull(message = "El nombre es obligatorio")
    private String recruiterName;
    
    private String company;
    
    @Email(message = "Email inválido")
    private String email;
    
    private String phone;
    private String opportunityType;
    private String comment;
    private LocalDateTime createdAt = LocalDateTime.now();
}
                    </pre>

                    <div class="flex items-center justify-between pt-2">
                        <h4 class="font-bold text-white text-sm font-mono text-brand-cyan">2. REST Controller (Spring Boot)</h4>
                        <span class="text-xs font-mono text-slate-500">ContactController.java</span>
                    </div>
                    <pre class="p-4 rounded-xl bg-brand-black text-xs font-mono text-slate-300 overflow-x-auto leading-relaxed border border-brand-cardBorder">
@RestController
@RequestMapping("/api/v1/contacts")
@CrossOrigin(origins = "*")
public class ContactController {

    private final ContactRepository repository;

    public ContactController(ContactRepository repository) {
        this.repository = repository;
    }

    @PostMapping
    public ResponseEntity&lt;ContactDocument&gt; createContact(@Valid @RequestBody ContactDocument contact) {
        ContactDocument saved = repository.save(contact);
        return ResponseEntity.status(HttpStatus.CREATED).body(saved);
    }
}
                    </pre>
                </div>
            </div>
        </section>

    </main>

    <!-- Footer -->
    <footer class="glass-panel border-t border-brand-cardBorder py-8 mt-20 relative z-10">
        <div class="max-w-7xl mx-auto px-4 text-center text-xs font-mono text-brand-textMuted space-y-2">
            <p>© 2026 Dan (Daniel Abraham Sánchez Bravo). Todos los derechos reservados.</p>
            <p class="text-slate-500">Desarrollado con Java Spring Boot, MongoDB & Tailwind CSS — Enfoque Product Owner</p>
        </div>
    </footer>

    <!-- Interactive JavaScript -->
    <script>
        // Dynamic Canvas Particle Engine (Cyan & Red Nodes)
        const canvas = document.getElementById('bgCanvas');
        const ctx = canvas.getContext('2d');

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        const particles = [];
        const particleCount = 45;

        for (let i = 0; i < particleCount; i++) {
            particles.push({
                x: Math.random() * canvas.width,
                y: Math.random() * canvas.height,
                vx: (Math.random() - 0.5) * 0.8,
                vy: (Math.random() - 0.5) * 0.8,
                radius: Math.random() * 2 + 1,
                color: Math.random() > 0.4 ? '#00f0ff' : '#ff2a5f'
            });
        }

        function animateCanvas() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Draw particles
            particles.forEach((p, index) => {
                p.x += p.vx;
                p.y += p.vy;

                if (p.x < 0 || p.x > canvas.width) p.vx *= -1;
                if (p.y < 0 || p.y > canvas.height) p.vy *= -1;

                ctx.beginPath();
                ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
                ctx.fillStyle = p.color;
                ctx.shadowBlur = 8;
                ctx.shadowColor = p.color;
                ctx.fill();

                // Draw connections
                for (let j = index + 1; j < particles.length; j++) {
                    const p2 = particles[j];
                    const dist = Math.hypot(p.x - p2.x, p.y - p2.y);

                    if (dist < 130) {
                        ctx.beginPath();
                        ctx.moveTo(p.x, p.y);
                        ctx.lineTo(p2.x, p2.y);
                        ctx.strokeStyle = `rgba(0, 240, 255, ${1 - dist / 130 * 0.8})`;
                        ctx.lineWidth = 0.5;
                        ctx.stroke();
                    }
                }
            });

            requestAnimationFrame(animateCanvas);
        }
        animateCanvas();

        // Live Form Validation & MongoDB Document Payload Simulator
        const formInputs = ['recruiterName', 'companyName', 'recruiterEmail', 'recruiterComment', 'opportunityType'];
        formInputs.forEach(id => {
            const el = document.getElementById(id);
            if (el) el.addEventListener('input', updateMongoPreview);
        });

        function updateMongoPreview() {
            const name = document.getElementById('recruiterName').value || 'Pendiente...';
            const company = document.getElementById('companyName').value || 'Pendiente...';
            const email = document.getElementById('recruiterEmail').value || 'Pendiente...';
            const type = document.getElementById('opportunityType').value;
            const comment = document.getElementById('recruiterComment').value || 'Esperando input...';

            const payload = {
                "_id": "66bc8a90f12c8a0012a9b3f1",
                "recruiterName": name,
                "company": company,
                "email": email,
                "opportunityType": type,
                "comment": comment,
                "createdAt": new Date().toISOString(),
                "status": "NEW_LEAD"
            };

            document.getElementById('mongoPreview').textContent = JSON.stringify(payload, null, 2);
        }

        function handleFormSubmit(e) {
            e.preventDefault();
            
            const nameEl = document.getElementById('recruiterName');
            const emailEl = document.getElementById('recruiterEmail');
            const commentEl = document.getElementById('recruiterComment');
            const alertBox = document.getElementById('formAlert');

            // Reset Errors
            [nameEl, emailEl, commentEl].forEach(el => el.classList.remove('input-error'));
            alertBox.className = 'hidden';

            let errors = [];

            if (!nameEl.value.trim()) {
                nameEl.classList.add('input-error');
                errors.push('El nombre completo es obligatorio.');
            }
            if (!emailEl.value.trim() || !emailEl.value.includes('@')) {
                emailEl.classList.add('input-error');
                errors.push('Por favor ingresa un correo electrónico válido.');
            }
            if (!commentEl.value.trim()) {
                commentEl.classList.add('input-error');
                errors.push('El campo de comentarios no puede estar vacío.');
            }

            // Display Error state in ORANGE as requested
            if (errors.length > 0) {
                alertBox.className = 'p-4 rounded-xl text-xs font-semibold bg-brand-orangeBg text-orange-300 border border-brand-orangeError flex items-center gap-2';
                alertBox.innerHTML = `<i class="fa-solid fa-triangle-exclamation text-brand-orangeError text-base"></i> <span>${errors.join(' ')}</span>`;
                alertBox.classList.remove('hidden');
                return;
            }

            // Success state
            alertBox.className = 'p-4 rounded-xl text-xs font-semibold bg-emerald-950 text-emerald-300 border border-emerald-600 flex items-center gap-2';
            alertBox.innerHTML = `<i class="fa-solid fa-circle-check text-emerald-400 text-base"></i> <span>¡Mensaje registrado exitosamente en MongoDB! Dan se pondrá en contacto a la brevedad.</span>`;
            alertBox.classList.remove('hidden');

            // Append to recommendations dynamically as an endorsement
            const container = document.getElementById('recommendationsContainer');
            const newRec = document.createElement('div');
            newRec.className = 'glass-panel p-6 rounded-2xl space-y-4 border-brand-cyan/50 cyan-glow';
            newRec.innerHTML = `
                <i class="fa-solid fa-quote-right absolute top-6 right-6 text-3xl text-brand-cyan/20"></i>
                <p class="text-sm text-slate-300 italic">"${commentEl.value.trim()}"</p>
                <div class="flex items-center gap-3 pt-2">
                    <div class="w-10 h-10 rounded-full bg-brand-cyan/30 border border-brand-cyan flex items-center justify-center font-bold text-brand-cyan text-sm">
                        ${nameEl.value.substring(0, 2).toUpperCase()}
                    </div>
                    <div>
                        <div class="font-bold text-sm text-white">${nameEl.value.trim()}</div>
                        <div class="text-xs text-brand-cyan">${document.getElementById('companyName').value.trim() || 'Empresa Reclutadora'}</div>
                    </div>
                </div>
            `;
            container.prepend(newRec);

            // Reset Form
            document.getElementById('recruiterForm').reset();
            updateMongoPreview();
        }

        // Tabs Logic for Scrum & Code
        function switchTab(tab) {
            const contentBacklog = document.getElementById('tabContent-backlog');
            const contentCode = document.getElementById('tabContent-code');
            const btnBacklog = document.getElementById('tabBtn-backlog');
            const btnCode = document.getElementById('tabBtn-code');

            if (tab === 'backlog') {
                contentBacklog.classList.remove('hidden');
                contentCode.classList.add('hidden');
                btnBacklog.className = 'pb-3 text-sm font-bold border-b-2 border-brand-cyan text-brand-cyan';
                btnCode.className = 'pb-3 text-sm font-bold border-b-2 border-transparent text-slate-400 hover:text-white';
            } else {
                contentBacklog.classList.add('hidden');
                contentCode.classList.remove('hidden');
                btnCode.className = 'pb-3 text-sm font-bold border-b-2 border-brand-red text-brand-red';
                btnBacklog.className = 'pb-3 text-sm font-bold border-b-2 border-transparent text-slate-400 hover:text-white';
            }
        }

        // Mobile Nav Toggle
        document.getElementById('mobileMenuBtn').addEventListener('click', () => {
            const nav = document.getElementById('mobileNav');
            nav.classList.toggle('hidden');
            nav.classList.toggle('flex');
        });
    </script>
    <script>
          const canvas = document.getElementById('bgCanvas');
        const ctx = canvas.getContext('2d');

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        const particles = [];
        const particleCount = 75; 
        const maxDistance = 110;  

        const mouse = { x: null, y: null, radius: 140 };
        window.addEventListener('mousemove', (e) => {
            mouse.x = e.clientX;
            mouse.y = e.clientY;
        });
        window.addEventListener('mouseleave', () => {
            mouse.x = null;
            mouse.y = null;
        });

        class Particle {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.vx = (Math.random() - 0.5) * 0.5; 
                this.vy = (Math.random() - 0.5) * 0.5; 
                this.radius = Math.random() * 2 + 1;
                this.isNearMouse = false;
            }

            update() {
                this.x += this.vx;
                this.y += this.vy;

                if (this.x < 0 || this.x > canvas.width) this.vx *= -1;
                if (this.y < 0 || this.y > canvas.height) this.vy *= -1;

                if (mouse.x !== null && mouse.y !== null) {
                    let dx = mouse.x - this.x;
                    let dy = mouse.y - this.y;
                    let dist = Math.sqrt(dx * dx + dy * dy);
                    
                    if (dist < mouse.radius) {
                        this.isNearMouse = true;
                        let force = (mouse.radius - dist) / mouse.radius;
                        this.x += (dx / dist) * force * 0.8;
                        this.y += (dy / dist) * force * 0.8;
                    } else {
                        this.isNearMouse = false;
                    }
                } else {
                    this.isNearMouse = false;
                }
            }

            draw() {
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
                ctx.fillStyle = this.isNearMouse ? '#00f0ff' : '#ff2a5f'; 
                ctx.fill();
            }
        }

        for (let i = 0; i < particleCount; i++) {
            particles.push(new Particle());
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            particles.forEach(p => {
                p.update();
                p.draw();
            });

            for (let i = 0; i < particles.length; i++) {
                for (let j = i + 1; j < particles.length; j++) {
                    let dx = particles[i].x - particles[j].x;
                    let dy = particles[i].y - particles[j].y;
                    let dist = Math.sqrt(dx * dx + dy * dy);

                    if (dist < maxDistance) {
                        let alpha = (1 - (dist / maxDistance)) * 0.18;
                        ctx.beginPath();
                        ctx.moveTo(particles[i].x, particles[i].y);
                        ctx.lineTo(particles[j].x, particles[j].y);
                        
                        if (particles[i].isNearMouse || particles[j].isNearMouse) {
                            ctx.strokeStyle = `rgba(0, 240, 255, ${alpha + 0.1})`; 
                            ctx.lineWidth = 1.0;
                        } else {
                            ctx.strokeStyle = `rgba(255, 42, 95, ${alpha})`; 
                            ctx.lineWidth = 0.7;
                        }
                        ctx.stroke();
                    }
                }
            }
            requestAnimationFrame(animate);
        }
        animate();
    </script>
    document.getElementById('profilePhotoInput').addEventListener('change', function(e) {
    const file = e.target.files[0];
    if (file) {Nop
        // Validar tamaño (máx 2MB)
        if (file.size > 2 * 1024 * 1024) {
            alert('La foto es demasiado grande. Máximo 2MB.');
            this.value = '';
            return;
        }
        
        const reader = new FileReader();
        reader.onload = function(event) {
            // Actualizar la foto en la tarjeta
            document.getElementById('profilePhotoDisplay').src = event.target.result;
            document.getElementById('profilePhotoDisplay').style.objectFit = 'cover';
        };
        reader.readAsDataURL(file);
    }
});
    </script>   
</body>

</html>
