# Asesor-pedagogico

<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CogniEval AI - Asistente de Evaluación Cognitiva</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Inter -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <!-- PDF.js para extracción de texto en PDF -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
    <!-- Mammoth.js para extracción de texto en DOCX -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mammoth/1.6.0/mammoth.browser.min.js"></script>
    <!-- Chart.js para gráficos de la Infografía -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- html2canvas y jsPDF para exportación de Infografía y Reporte General -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

    <script>
        function configureTailwind() {
            if (typeof tailwind !== 'undefined') {
                tailwind.config = {
                    theme: {
                        extend: {
                            fontFamily: {
                                sans: ['Inter', 'sans-serif'],
                            },
                            colors: {
                                indigo: {
                                    50: '#eef2ff',
                                    100: '#e0e7ff',
                                    200: '#c7d2fe',
                                    300: '#a5b4fc',
                                    400: '#818cf8',
                                    500: '#6366f1',
                                    600: '#4f46e5',
                                    700: '#4338ca',
                                    800: '#3730a3',
                                    900: '#312e81',
                                }
                            }
                        }
                    }
                };
            }
        }
        configureTailwind();
        window.addEventListener('load', configureTailwind);
    </script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f8fafc;
            color: #0f172a;
        }
        /* Scrollbar estilizado */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
        .glass-header {
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(12px);
        }
        @keyframes pulse-border {
            0%, 100% { border-color: #6366f1; }
            50% { border-color: #c7d2fe; }
        }
        .evaluating-card {
            animation: pulse-border 2s infinite;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col">

    <!-- Notificación Toast Flotante (Reemplazo seguro de alert) -->
    <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 max-w-sm w-full pointer-events-none"></div>

    <!-- Barra Superior -->
    <header class="glass-header sticky top-0 z-30 border-b border-slate-200 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3.5 flex flex-col md:flex-row md:items-center md:justify-between gap-4">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-indigo-600 to-violet-600 flex items-center justify-center text-white shadow-md shadow-indigo-200 shrink-0">
    <!-- Barra Superior Minimalista estilo CogniEval AI -->
    <header class="glass-header sticky top-0 z-30 border-b border-slate-200/80">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 py-3 flex flex-wrap items-center justify-between gap-3">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-indigo-600 flex items-center justify-center text-white shadow-sm shrink-0">
                    <i data-lucide="brain" class="w-5 h-5"></i>
                </div>
                <div>
                    <div class="flex items-center gap-2">
                        <h1 class="text-base sm:text-lg font-extrabold text-slate-900 tracking-tight">CogniEval</h1>
                        <span class="px-2 py-0.5 rounded-full text-[11px] font-bold bg-indigo-50 text-indigo-600 border border-indigo-100">AI v2.5</span>
                        <span id="cloud-sync-badge" class="hidden sm:inline-flex items-center gap-1 px-2 py-0.5 rounded-full text-[11px] font-semibold bg-emerald-50 text-emerald-700 border border-emerald-200">
                            <span class="w-1.5 h-1.5 rounded-full bg-emerald-500"></span>
                            Historial Guardado
                        </span>
                    </div>
                    <p class="text-xs text-slate-500">Asistente de Evaluación Cognitiva y Metacognición</p>
                </div>
            </div>

            <!-- Acciones Rápidas Superiores -->
            <div class="flex items-center gap-2.5">
                <button onclick="loadQuickDemo()" class="inline-flex items-center gap-1.5 px-3.5 py-2 rounded-xl text-xs font-semibold bg-amber-50 hover:bg-amber-100 text-amber-800 border border-amber-200/80 transition-colors">
                    <i data-lucide="wand-2" class="w-3.5 h-3.5 text-amber-600"></i>
                    <span>Cargar Datos Demo</span>
                </button>
                <div class="hidden sm:inline-flex items-center gap-1.5 px-3 py-2 rounded-xl text-xs font-medium bg-slate-50 text-slate-600 border border-slate-200">
                    <i data-lucide="key-round" class="w-3.5 h-3.5 text-slate-400"></i>
                    <span>Gemini AI: Conectado</span>
                </div>
            </div>
        </div>
    </header>

    <!-- Contenido Principal -->
    <main class="flex-1 max-w-6xl w-full mx-auto px-4 sm:px-6 py-6 flex flex-col gap-6">
        
        <!-- Banner Hero Oscuro con Acciones Globales -->
        <section class="rounded-2xl bg-gradient-to-r from-[#0f172a] via-[#131c38] to-[#1e1b4b] text-white p-6 sm:p-7 shadow-lg border border-slate-800/80">
            <div class="flex flex-col lg:flex-row lg:items-center justify-between gap-6">
                <div class="max-w-2xl">
                    <div class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-indigo-500/20 border border-indigo-400/30 text-indigo-200 text-xs font-semibold mb-3">
                        <i data-lucide="lightbulb" class="w-3.5 h-3.5 text-indigo-300"></i>
                        <span>Enfoque en Procesos Cognitivos Complejos</span>
                    </div>
                    <h2 class="text-xl sm:text-2xl font-extrabold tracking-tight text-white">
                        Evaluación Inteligente y Retroalimentación Formativa
                    </h2>
                    <p class="text-xs sm:text-sm text-slate-300 mt-1.5 leading-relaxed">
                        Sube trabajos de laboratorio y sus rúbricas de evaluación. La IA analiza la profundidad conceptual, resolución de problemas y argumentación metacognitiva calculando notas precisas de 0.0 a 5.0.
                    </p>
                </div>

                <!-- Botones Principales de Consolidación -->
                <div class="flex flex-col sm:flex-row lg:flex-col gap-2.5 shrink-0 min-w-[230px]">
                    <button id="btn-global-pdf" onclick="generateGlobalPDF()" disabled
                        class="w-full inline-flex items-center justify-center gap-2 px-4 py-2.5 rounded-xl text-xs sm:text-sm font-bold bg-indigo-600/40 text-indigo-200/60 border border-indigo-500/30 transition-all cursor-not-allowed">
                        <i data-lucide="file-text" class="w-4 h-4"></i>
                        <span>Informe General (PDF) (<span id="pdf-evaluated-count">0</span>)</span>
                    </button>

                    <button id="btn-global-infographic" onclick="openInfographicModal()" disabled
                        class="w-full inline-flex items-center justify-center gap-2 px-4 py-2.5 rounded-xl text-xs sm:text-sm font-bold bg-amber-500/30 text-amber-200/60 border border-amber-400/30 transition-all cursor-not-allowed">
                        <i data-lucide="pie-chart" class="w-4 h-4"></i>
                        <span>Infografía Consolidada (<span id="info-evaluated-count">0</span>)</span>
                    </button>
                </div>
            </div>
        </section>

        <!-- Grid Principal: Izquierda (Módulo 1: Carga) / Derecha (Trabajos Registrados) -->
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 items-start">
            
            <!-- COLUMNA IZQUIERDA: Módulo 1: Carga Unificada (5 cols) -->
            <div class="lg:col-span-5">
                <section class="bg-white rounded-2xl border border-slate-200/90 shadow-sm p-5 sm:p-6 flex flex-col gap-5">
                    <!-- Cabecera Tarjeta Izquierda -->
                    <div class="flex items-center justify-between border-b border-slate-100 pb-3.5">
                        <div class="flex items-center gap-2">
                            <div class="w-7 h-7 rounded-lg bg-indigo-50 text-indigo-600 flex items-center justify-center">
                                <i data-lucide="file-plus-2" class="w-4 h-4"></i>
                            </div>
                            <h2 class="font-bold text-slate-900 text-sm sm:text-base">Nuevo Trabajo / Laboratorio</h2>
                        </div>
                        <span class="text-xs font-medium text-slate-400">Módulo 1: Carga</span>
                    </div>

                    <!-- Campo Nombre o Título del Lab -->
                    <div>
                        <label for="manual-student-name" class="block text-[11px] font-bold uppercase tracking-wider text-slate-500 mb-1.5">
                            Nombre o Título del Lab / Estudiante
                        </label>
                        <input type="text" id="manual-student-name" placeholder="Ej. Laboratorio 1: Procesos Cognitivos y Memoria"
                            class="w-full rounded-xl border border-slate-200 bg-slate-50/50 focus:bg-white px-3.5 py-2.5 text-xs sm:text-sm text-slate-800 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-100 outline-none transition-all">
                    </div>

                    <!-- 1. Solución del Trabajo / Lab o Carpeta -->
                    <div>
                        <div class="flex items-center justify-between mb-1.5">
                            <label class="text-[11px] font-bold uppercase tracking-wider text-slate-600">
                                1. Solución del Trabajo / Lab o Carpeta
                            </label>
                        </div>

                        <label for="labs-file-input" class="block border-2 border-dashed border-slate-200 hover:border-indigo-400 bg-slate-50/60 hover:bg-indigo-50/30 rounded-xl p-5 text-center cursor-pointer transition-all group">
                            <input type="file" id="labs-file-input" accept=".pdf,.docx,.txt,.md" multiple class="hidden" onchange="handleLabFilesUpload(event)">
                            <div class="flex items-center justify-center gap-2 text-indigo-500 mb-2 group-hover:scale-105 transition-transform">
                                <i data-lucide="folder-open" class="w-6 h-6"></i>
                                <i data-lucide="upload-cloud" class="w-6 h-6 text-slate-400"></i>
                            </div>
                            <p class="text-xs sm:text-sm font-medium text-slate-700">
                                Arrastra <strong class="font-bold text-slate-900">Archivos o una Carpeta completa</strong> aquí
                            </p>
                            <p class="text-[11px] text-slate-400 mt-1">PDF, Word (.docx), TXT, MD o múltiples entregas</p>
                        </label>

                        <div class="flex justify-end mt-1.5">
                            <label for="labs-folder-input" class="inline-flex items-center gap-1 text-xs font-semibold text-indigo-600 hover:text-indigo-800 cursor-pointer">
                                <input type="file" id="labs-folder-input" webkitdirectory directory multiple class="hidden" onchange="handleLabFilesUpload(event)">
                                <i data-lucide="folder-plus" class="w-3.5 h-3.5"></i>
                                <span>Seleccionar Carpeta entera</span>
                            </label>
                        </div>

                        <textarea id="manual-lab-text" rows="3" placeholder="O pega directamente aquí el contenido redactado del trabajo de laboratorio..."
                            class="mt-2 w-full rounded-xl border border-slate-200 bg-slate-50/40 focus:bg-white p-3 text-xs sm:text-sm text-slate-700 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-100 outline-none transition-all"></textarea>
                    </div>

                    <!-- 2. Rúbrica de Evaluación -->
                    <div class="pt-3 border-t border-slate-100">
                        <div class="flex items-center justify-between mb-1.5">
                            <label for="rubric-text" class="text-[11px] font-bold uppercase tracking-wider text-slate-600 flex items-center gap-1.5">
                                <span>2. Rúbrica de Evaluación (0.0 - 5.0)</span>
                                <span id="stat-rubric-status" class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-amber-50 text-amber-700">Sin definir</span>
                            </label>
                            <div class="flex items-center gap-2">
                                <label for="rubric-file-input" class="text-xs font-semibold text-indigo-600 hover:text-indigo-800 cursor-pointer flex items-center gap-1">
                                    <input type="file" id="rubric-file-input" accept=".pdf,.docx,.txt,.md" class="hidden" onchange="handleRubricFileUpload(event)">
                                    <i data-lucide="paperclip" class="w-3 h-3"></i>
                                    <span>Subir archivo</span>
                                </label>
                                <button onclick="clearRubric()" class="text-xs text-slate-400 hover:text-rose-600">Limpiar</button>
                            </div>
                        </div>
                        <textarea id="rubric-text" rows="4" oninput="updateDashboardState()"
                            placeholder="Pega aquí los criterios de evaluación o súbelos con el botón 'Subir archivo'..."
                            class="w-full rounded-xl border border-slate-200 bg-slate-50/40 focus:bg-white p-3 text-xs sm:text-sm text-slate-700 leading-relaxed focus:border-indigo-500 focus:ring-2 focus:ring-indigo-100 outline-none transition-all"></textarea>
                    </div>

                    <!-- Botón Agregar Trabajo -->
                    <button onclick="addManualSubmission()" class="w-full py-2.5 px-4 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white text-xs sm:text-sm font-bold shadow-sm shadow-indigo-200 transition-all flex items-center justify-center gap-2">
                        <i data-lucide="plus-circle" class="w-4 h-4"></i>
                        <span>Registrar Trabajo en la Lista</span>
                    </button>
                </section>
            </div>

            <!-- COLUMNA DERECHA: Trabajos Registrados y Resultados (7 cols) -->
            <div class="lg:col-span-7 flex flex-col gap-4">
                
                <!-- Cabecera de Trabajos Registrados -->
                <div class="bg-white rounded-2xl border border-slate-200/90 shadow-sm px-5 py-4 flex flex-wrap items-center justify-between gap-3">
                    <div>
                        <div class="flex items-center gap-2.5">
                            <h2 class="font-bold text-slate-900 text-base">Trabajos Registrados</h2>
                            <span id="saved-history-pill" class="hidden text-[11px] font-bold text-emerald-700 bg-emerald-50 border border-emerald-200 px-2.5 py-0.5 rounded-full">
                                0 analizados
                            </span>
                        </div>
                        <p class="text-xs text-slate-500 mt-0.5">
                            <span id="stat-total-labs" class="font-semibold text-slate-700">0</span> laboratorio(s) registrado(s) • 
                            <span id="stat-evaluated-labs" class="font-semibold text-emerald-600">0</span> evaluado(s) • 
                            Promedio: <span id="stat-avg-grade" class="font-bold text-indigo-600">-- / 5.0</span>
                        </p>
                    </div>

                    <div class="flex items-center gap-2">
                        <button id="btn-evaluate-all" onclick="evaluateAllPending()" disabled
                            class="inline-flex items-center gap-1.5 px-3.5 py-2 rounded-xl text-xs font-bold bg-slate-100 text-slate-400 border border-slate-200 transition-all cursor-not-allowed">
                            <i data-lucide="sparkles" class="w-3.5 h-3.5"></i>
                            <span>Evaluar Pendientes (<span id="pending-count">0</span>)</span>
                        </button>

                        <button id="btn-clear-all-labs" onclick="clearAllSubmissions()" title="Vaciar historial y lista"
                            class="hidden p-2 rounded-xl text-slate-400 hover:text-rose-600 hover:bg-rose-50 border border-transparent hover:border-rose-200 transition-colors">
                            <i data-lucide="trash-2" class="w-4 h-4"></i>
                        </button>
                    </div>
                </div>

                <!-- Contenedor vacío estilizado como la imagen -->
                <div id="empty-state" class="bg-white rounded-2xl border-2 border-dashed border-slate-200 p-12 text-center flex flex-col items-center justify-center min-h-[340px]">
                    <div class="w-12 h-12 rounded-xl bg-slate-100 text-slate-400 flex items-center justify-center mb-3">
                        <i data-lucide="folder" class="w-6 h-6"></i>
                    </div>
                    <h3 class="text-sm sm:text-base font-bold text-slate-800">No hay laboratorios en la lista</h3>
                    <p class="text-xs text-slate-500 max-w-sm mt-1 leading-relaxed">
                        Ingresa la información en el formulario de la izquierda o haz clic en "Cargar Datos Demo" para probar la plataforma.
                    </p>
                </div>

                <!-- Lista dinámica de tarjetas de trabajos -->
                <div id="submissions-list" class="flex flex-col gap-3.5"></div>
            </div>
        </div>
    </main>

    <!-- MODAL: Informe Individual Detallado -->
    <div id="individual-modal" class="fixed inset-0 z-40 hidden bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-3 sm:p-6 overflow-y-auto">
        <div class="bg-white rounded-2xl shadow-2xl border border-slate-200 max-w-4xl w-full max-h-[90vh] flex flex-col overflow-hidden">
            <!-- Modal Header -->
            <div class="px-6 py-4 bg-slate-50 border-b border-slate-200 flex items-center justify-between gap-4">
                <div>
                    <span class="text-xs font-bold uppercase tracking-wider text-indigo-600">Informe Individual de Evaluación Cognitiva</span>
                    <h3 id="modal-student-title" class="text-lg sm:text-xl font-bold text-slate-900 mt-0.5">Nombre del Estudiante</h3>
                </div>
                <div class="flex items-center gap-3">
                    <div id="modal-grade-badge" class="px-3.5 py-1.5 rounded-xl bg-indigo-600 text-white font-extrabold text-base sm:text-lg shadow-sm">
                        0.0 / 5.0
                    </div>
                    <button onclick="closeIndividualModal()" class="p-2 rounded-xl text-slate-400 hover:text-slate-700 hover:bg-slate-200/70 transition-colors">
                        <i data-lucide="x" class="w-5 h-5"></i>
                    </button>
                </div>
            </div>

            <!-- Modal Body -->
            <div id="modal-individual-body" class="p-6 overflow-y-auto flex flex-col gap-6">
                <!-- Se llena dinámicamente -->
            </div>

            <!-- Modal Footer -->
            <div class="px-6 py-3.5 bg-slate-50 border-t border-slate-200 flex flex-wrap items-center justify-between gap-3">
                <button onclick="copyIndividualReport()" class="inline-flex items-center gap-2 px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold text-slate-700 bg-white border border-slate-300 hover:bg-slate-100 transition-colors">
                    <i data-lucide="copy" class="w-4 h-4"></i>
                    Copiar Retroalimentación
                </button>
                <div class="flex items-center gap-2">
                    <button onclick="downloadSingleStudentPDF()" class="inline-flex items-center gap-2 px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold text-white bg-indigo-600 hover:bg-indigo-700 transition-colors">
                        <i data-lucide="download" class="w-4 h-4"></i>
                        Descargar PDF Individual
                    </button>
                    <button onclick="closeIndividualModal()" class="px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold text-slate-600 hover:bg-slate-200/70 transition-colors">
                        Cerrar
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- MODAL: Infografía Consolidada del Grupo -->
    <div id="infographic-modal" class="fixed inset-0 z-40 hidden bg-slate-900/70 backdrop-blur-sm flex items-center justify-center p-3 sm:p-6 overflow-y-auto">
        <div class="bg-white rounded-2xl shadow-2xl border border-slate-200 max-w-5xl w-full max-h-[92vh] flex flex-col overflow-hidden">
            <!-- Header del Modal -->
            <div class="px-6 py-4 bg-slate-900 text-white flex flex-wrap items-center justify-between gap-3">
                <div class="flex items-center gap-2.5">
                    <div class="w-8 h-8 rounded-lg bg-indigo-500 flex items-center justify-center">
                        <i data-lucide="pie-chart" class="w-4 h-4 text-white"></i>
                    </div>
                    <div>
                        <h3 class="text-base sm:text-lg font-bold">Infografía Analítica Consolidada</h3>
                        <p class="text-xs text-slate-300">Diagnóstico cognitivo y rendimiento global del grupo</p>
                    </div>
                </div>
                <div class="flex items-center gap-2">
                    <button onclick="exportInfographicPNG()" class="inline-flex items-center gap-1.5 px-3 py-1.5 rounded-lg bg-indigo-600 hover:bg-indigo-500 text-white text-xs font-semibold transition-colors">
                        <i data-lucide="image" class="w-3.5 h-3.5"></i>
                        Descargar PNG
                    </button>
                    <button onclick="exportInfographicPDF()" class="inline-flex items-center gap-1.5 px-3 py-1.5 rounded-lg bg-emerald-600 hover:bg-emerald-500 text-white text-xs font-semibold transition-colors">
                        <i data-lucide="file-down" class="w-3.5 h-3.5"></i>
                        Descargar PDF
                    </button>
                    <button onclick="closeInfographicModal()" class="p-1.5 rounded-lg text-slate-400 hover:text-white hover:bg-slate-800 transition-colors ml-1">
                        <i data-lucide="x" class="w-5 h-5"></i>
                    </button>
                </div>
            </div>

            <!-- Estado de carga de síntesis IA -->
            <div id="infographic-loading" class="p-12 text-center flex flex-col items-center justify-center">
                <div class="w-12 h-12 border-4 border-indigo-200 border-t-indigo-600 rounded-full animate-spin mb-4"></div>
                <h4 class="text-base font-bold text-slate-800">Sintetizando resultados cognitivos del grupo...</h4>
                <p class="text-xs text-slate-500 mt-1">La IA está cruzando todas las evaluaciones para detectar patrones, fortalezas y brechas.</p>
            </div>

            <!-- Lienzo Exportable de la Infografía -->
            <div id="infographic-scroll-area" class="overflow-y-auto hidden bg-slate-100 p-4 sm:p-6">
                <div id="infographic-canvas" class="bg-white rounded-2xl shadow-lg border border-slate-200 overflow-hidden max-w-4xl mx-auto">
                    
                    <!-- Banner Superior de Infografía -->
                    <div class="bg-gradient-to-r from-indigo-900 via-indigo-800 to-violet-900 text-white p-6 sm:p-8">
                        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                            <div>
                                <span class="inline-block px-2.5 py-1 rounded-md bg-white/15 text-indigo-100 text-xs font-semibold tracking-wider uppercase mb-2">
                                    Reporte de Analítica Académica • IA
                                </span>
                                <h2 class="text-2xl sm:text-3xl font-extrabold tracking-tight">Panorama Cognitivo del Grupo</h2>
                                <p id="info-subtitle" class="text-indigo-200 text-xs sm:text-sm mt-1">Evaluación consolidada de laboratorios y entregas académicas</p>
                            </div>
                            <div class="bg-white/10 backdrop-blur-md border border-white/20 rounded-2xl p-4 text-center shrink-0">
                                <p class="text-xs text-indigo-200 uppercase font-semibold">Promedio General</p>
                                <p id="info-kpi-avg" class="text-3xl sm:text-4xl font-black text-white mt-0.5">0.0</p>
                                <p class="text-[11px] text-indigo-200">Escala 0.0 - 5.0</p>
                            </div>
                        </div>

                        <!-- KPIs Secundarios -->
                        <div class="grid grid-cols-2 sm:grid-cols-4 gap-3 mt-6 pt-5 border-t border-white/15">
                            <div class="bg-white/10 rounded-xl p-3">
                                <p class="text-[11px] text-indigo-200">Total Evaluados</p>
                                <p id="info-kpi-count" class="text-xl font-bold text-white">0</p>
                            </div>
                            <div class="bg-white/10 rounded-xl p-3">
                                <p class="text-[11px] text-indigo-200">Tasa Aprobación (≥3.0)</p>
                                <p id="info-kpi-pass" class="text-xl font-bold text-emerald-300">0%</p>
                            </div>
                            <div class="bg-white/10 rounded-xl p-3">
                                <p class="text-[11px] text-indigo-200">Nota Más Alta</p>
                                <p id="info-kpi-max" class="text-xl font-bold text-white">0.0</p>
                            </div>
                            <div class="bg-white/10 rounded-xl p-3">
                                <p class="text-[11px] text-indigo-200">Nota Más Baja</p>
                                <p id="info-kpi-min" class="text-xl font-bold text-amber-300">0.0</p>
                            </div>
                        </div>
                    </div>

                    <!-- Cuerpo de Gráficos y Hallazgos -->
                    <div class="p-6 sm:p-8 flex flex-col gap-6">
                        
                        <!-- Fila de Gráficos (Chart.js) -->
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div class="bg-slate-50 rounded-2xl p-4 border border-slate-200/80">
                                <h4 class="text-xs font-bold uppercase tracking-wider text-slate-600 mb-3 flex items-center gap-1.5">
                                    <span class="w-2.5 h-2.5 rounded-full bg-indigo-600"></span>
                                    Distribución de Calificaciones por Estudiante
                                </h4>
                                <div class="h-56 relative">
                                    <canvas id="chart-students"></canvas>
                                </div>
                            </div>

                            <div class="bg-slate-50 rounded-2xl p-4 border border-slate-200/80">
                                <h4 class="text-xs font-bold uppercase tracking-wider text-slate-600 mb-3 flex items-center gap-1.5">
                                    <span class="w-2.5 h-2.5 rounded-full bg-violet-600"></span>
                                    Desempeño Promedio por Criterio de Rúbrica
                                </h4>
                                <div class="h-56 relative">
                                    <canvas id="chart-criteria"></canvas>
                                </div>
                            </div>
                        </div>

                        <!-- Competencias Mejor Logradas vs Debilidades Cognitivas -->
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <!-- Fortalezas -->
                            <div class="bg-emerald-50/70 rounded-2xl p-5 border border-emerald-200">
                                <div class="flex items-center gap-2 text-emerald-800 font-bold text-sm mb-3">
                                    <i data-lucide="trending-up" class="w-5 h-5 text-emerald-600"></i>
                                    <span>Competencias Mejor Logradas</span>
                                </div>
                                <ul id="info-strengths-list" class="space-y-2 text-xs sm:text-sm text-emerald-950">
                                    <!-- Dinámico -->
                                </ul>
                            </div>

                            <!-- Debilidades Cognitivas -->
                            <div class="bg-amber-50/70 rounded-2xl p-5 border border-amber-200">
                                <div class="flex items-center gap-2 text-amber-900 font-bold text-sm mb-3">
                                    <i data-lucide="alert-triangle" class="w-5 h-5 text-amber-600"></i>
                                    <span>Principales Debilidades Cognitivas</span>
                                </div>
                                <ul id="info-weaknesses-list" class="space-y-2 text-xs sm:text-sm text-amber-950">
                                    <!-- Dinámico -->
                                </ul>
                            </div>
                        </div>

                        <!-- Resumen Consolidado de Trabajos Analizados y Notas Guardadas -->
                        <div class="bg-white rounded-2xl p-5 border border-slate-200 shadow-sm">
                            <div class="flex items-center justify-between mb-3">
                                <div class="flex items-center gap-2 text-slate-900 font-bold text-sm">
                                    <i data-lucide="list-checks" class="w-5 h-5 text-indigo-600"></i>
                                    <span>Resumen de Trabajos Analizados y Calificaciones Guardadas</span>
                                </div>
                                <span id="info-table-badge" class="text-xs font-semibold text-indigo-700 bg-indigo-50 px-2.5 py-0.5 rounded-full">0 trabajos</span>
                            </div>
                            <div class="overflow-x-auto">
                                <table class="w-full text-left border-collapse">
                                    <thead>
                                        <tr class="border-b border-slate-200 text-[11px] font-bold uppercase tracking-wider text-slate-500">
                                            <th class="py-2 pr-3">Trabajo / Estudiante</th>
                                            <th class="py-2 px-3">Síntesis Conceptual</th>
                                            <th class="py-2 pl-3 text-right">Nota</th>
                                        </tr>
                                    </thead>
                                    <tbody id="info-analyzed-table-body" class="divide-y divide-slate-100 text-xs">
                                        <!-- Dinámico -->
                                    </tbody>
                                </table>
                            </div>
                        </div>

                        <!-- Recomendaciones Pedagógicas para el Docente -->
                        <div class="bg-indigo-50/80 rounded-2xl p-5 border border-indigo-200">
                            <div class="flex items-center gap-2 text-indigo-900 font-bold text-sm mb-3">
                                <i data-lucide="lightbulb" class="w-5 h-5 text-indigo-600"></i>
                                <span>Recomendaciones Pedagógicas Generales para el Docente</span>
                            </div>
                            <div id="info-recommendations-list" class="grid grid-cols-1 sm:grid-cols-2 gap-3 text-xs sm:text-sm text-indigo-950">
                                <!-- Dinámico -->
                            </div>
                        </div>

                        <!-- Pie de Infografía -->
                        <div class="pt-3 border-t border-slate-200 flex items-center justify-between text-[11px] text-slate-400">
                            <span>Generado por Asistente de Evaluación Cognitiva • IA</span>
                            <span id="info-date"></span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Overlay de carga para PDF Global -->
    <div id="pdf-loading-overlay" class="fixed inset-0 z-50 hidden bg-slate-900/70 backdrop-blur-sm flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl p-6 max-w-sm w-full text-center shadow-2xl">
            <div class="w-12 h-12 border-4 border-indigo-200 border-t-indigo-600 rounded-full animate-spin mx-auto mb-4"></div>
            <h4 class="text-base font-bold text-slate-800">Generando Informe General PDF</h4>
            <p class="text-xs text-slate-500 mt-1">Analizando brechas cognitivas del grupo y compilando resultados...</p>
        </div>
    </div>

    <script>
        // Estado global accesible tanto para módulos ES como para scripts clásicos
        window.submissions = [];
        window.cachedGroupSynthesis = null;
    </script>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc, deleteDoc, onSnapshot, collection } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // Configuración de almacenamiento persistente en la nube
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        let db = null;
        let auth = null;
        let currentUser = null;
        let unsubscribeEvaluations = null;
        let unsubscribeRubric = null;

        async function initPersistentStorage() {
            try {
                if (typeof __firebase_config === 'undefined' || !__firebase_config) return;
                const firebaseConfig = JSON.parse(__firebase_config);
                const app = initializeApp(firebaseConfig);
                auth = getAuth(app);
                db = getFirestore(app);

                if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                    await signInWithCustomToken(auth, __initial_auth_token);
                } else {
                    await signInAnonymously(auth);
                }

                onAuthStateChanged(auth, (user) => {
                    if (!user) return;
                    currentUser = user;
                    subscribeToSavedData(user.uid);
                });
            } catch (err) {
                console.warn('Almacenamiento en sesión local activo:', err);
            }
        }

        function subscribeToSavedData(userId) {
            if (!db || !userId) return;

            // 1. Escuchar rúbrica guardada
            const rubricDocRef = doc(db, 'artifacts', appId, 'users', userId, 'config', 'active_rubric');
            if (unsubscribeRubric) unsubscribeRubric();
            unsubscribeRubric = onSnapshot(rubricDocRef, (snap) => {
                if (snap.exists()) {
                    const savedRubric = snap.data().text || '';
                    const textarea = document.getElementById('rubric-text');
                    if (textarea && document.activeElement !== textarea && textarea.value !== savedRubric) {
                        textarea.value = savedRubric;
                        if (typeof updateDashboardState === 'function') updateDashboardState();
                    }
                }
            }, (err) => console.error('Error sincronizando rúbrica:', err));

            // 2. Escuchar trabajos evaluados y guardados
            const evalsColRef = collection(db, 'artifacts', appId, 'users', userId, 'evaluated_works');
            if (unsubscribeEvaluations) unsubscribeEvaluations();
            unsubscribeEvaluations = onSnapshot(evalsColRef, (snapshot) => {
                const cloudMap = new Map();
                snapshot.forEach((docSnap) => {
                    const data = docSnap.data();
                    cloudMap.set(docSnap.id, {
                        id: docSnap.id,
                        studentName: data.studentName || 'Estudiante',
                        fileName: data.fileName || 'Documento guardado',
                        content: data.content || '',
                        status: 'evaluated',
                        errorMsg: null,
                        evaluatedAt: data.evaluatedAt || Date.now(),
                        evaluation: data.evaluation ? JSON.parse(data.evaluation) : null
                    });
                });

                // Mantener trabajos pendientes locales y fusionar con los guardados en la nube
                const currentList = Array.isArray(window.submissions) ? window.submissions : [];
                const localPending = currentList.filter(s => s.status !== 'evaluated' && !cloudMap.has(s.id));
                const cloudList = Array.from(cloudMap.values()).sort((a, b) => (a.evaluatedAt || 0) - (b.evaluatedAt || 0));

                window.submissions = [...cloudList, ...localPending];
                window.cachedGroupSynthesis = null;
                if (typeof renderSubmissions === 'function') renderSubmissions();
                if (typeof updateDashboardState === 'function') updateDashboardState();
            }, (err) => console.error('Error sincronizando historial:', err));
        }

        // Exponer funciones de guardado para el flujo principal
        window.saveEvaluatedWorkToCloud = async function(item) {
            if (!db || !currentUser || !item || !item.evaluation) return;
            try {
                const workRef = doc(db, 'artifacts', appId, 'users', currentUser.uid, 'evaluated_works', item.id);
                await setDoc(workRef, {
                    studentName: item.studentName,
                    fileName: item.fileName,
                    content: (item.content || '').slice(0, 25000),
                    evaluatedAt: item.evaluatedAt || Date.now(),
                    evaluation: JSON.stringify(item.evaluation)
                });
            } catch (err) {
                console.error('Error guardando evaluación:', err);
            }
        };

        window.deleteWorkFromCloud = async function(id) {
            if (!db || !currentUser) return;
            try {
                const workRef = doc(db, 'artifacts', appId, 'users', currentUser.uid, 'evaluated_works', id);
                await deleteDoc(workRef);
            } catch (err) {
                console.error('Error eliminando registro:', err);
            }
        };

        window.saveRubricToCloud = async function(text) {
            if (!db || !currentUser) return;
            try {
                const rubricRef = doc(db, 'artifacts', appId, 'users', currentUser.uid, 'config', 'active_rubric');
                await setDoc(rubricRef, { text: text || '', updatedAt: Date.now() });
            } catch (err) {
                console.error('Error guardando rúbrica:', err);
            }
        };

        initPersistentStorage();
    </script>

    <script>
        // Configuración inicial de PDF.js Worker
        if (window.pdfjsLib) {
            pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';
        }

        // Configuración API Gemini (Clave inyectada en tiempo de ejecución)
        const apiKey = "";
        const GEMINI_MODEL = "gemini-3-flash-preview";

        // Estado global de la aplicación enlazado a window
        var submissions = window.submissions;
        let activeModalSubmissionId = null;
        let chartStudentsInstance = null;
        let chartCriteriaInstance = null;
        var cachedGroupSynthesis = window.cachedGroupSynthesis;

        // Inicializar iconos de Lucide al cargar
        window.addEventListener('DOMContentLoaded', () => {
            lucide.createIcons();
            renderSubmissions();
            updateDashboardState();
        });

        // ==========================================
        // 1. UTILIDADES DE INTERFAZ Y NOTIFICACIONES
        // ==========================================
        function showToast(message, type = 'info') {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            
            const colors = {
                info: 'bg-slate-800 text-white border-slate-700',
                success: 'bg-emerald-600 text-white border-emerald-500',
                warning: 'bg-amber-600 text-white border-amber-500',
                error: 'bg-rose-600 text-white border-rose-500'
            };
            const icons = {
                info: 'info',
                success: 'check-circle',
                warning: 'alert-circle',
                error: 'x-circle'
            };

            toast.className = `pointer-events-auto flex items-center gap-2.5 px-4 py-3 rounded-xl shadow-lg border text-xs sm:text-sm font-medium transition-all transform translate-y-2 opacity-0 ${colors[type] || colors.info}`;
            toast.innerHTML = `
                <i data-lucide="${icons[type] || 'info'}" class="w-4 h-4 shrink-0"></i>
                <span class="flex-1">${message}</span>
            `;

            container.appendChild(toast);
            lucide.createIcons({ nodes: [toast] });

            requestAnimationFrame(() => {
                toast.classList.remove('translate-y-2', 'opacity-0');
            });

            setTimeout(() => {
                toast.classList.add('opacity-0', 'translate-y-2');
                setTimeout(() => toast.remove(), 300);
            }, 3800);
        }

        function escapeHTML(str) {
            if (!str) return '';
            return String(str)
                .replace(/&/g, '&amp;')
                .replace(/</g, '&lt;')
                .replace(/>/g, '&gt;')
                .replace(/"/g, '&quot;')
                .replace(/'/g, '&#039;');
        }

        // ==========================================
        // 2. EXTRACCIÓN DE TEXTO (PDF, DOCX, TXT)
        // ==========================================
        async function extractTextFromFile(file) {
            const fileName = file.name.toLowerCase();
            
            if (fileName.endsWith('.txt') || fileName.endsWith('.md')) {
                return await file.text();
            } 
            else if (fileName.endsWith('.pdf')) {
                const arrayBuffer = await file.arrayBuffer();
                const pdf = await pdfjsLib.getDocument({ data: arrayBuffer }).promise;
                let fullText = '';
                for (let pageNum = 1; pageNum <= pdf.numPages; pageNum++) {
                    const page = await pdf.getPage(pageNum);
                    const textContent = await page.getTextContent();
                    const pageText = textContent.items.map(item => item.str).join(' ');
                    fullText += pageText + '\n\n';
                }
                return fullText.trim();
            } 
            else if (fileName.endsWith('.docx')) {
                const arrayBuffer = await file.arrayBuffer();
                const result = await mammoth.extractRawText({ arrayBuffer });
                return result.value.trim();
            } 
            else {
                throw new Error('Formato no soportado. Usa PDF, DOCX o TXT.');
            }
        }

        async function handleRubricFileUpload(event) {
            const file = event.target.files[0];
            if (!file) return;
            try {
                showToast(`Leyendo rúbrica "${file.name}"...`, 'info');
                const text = await extractTextFromFile(file);
                if (!text) throw new Error('El archivo parece estar vacío o es una imagen escaneada sin texto.');
                document.getElementById('rubric-text').value = text;
                cachedGroupSynthesis = null;
                updateDashboardState();
                showToast('Rúbrica cargada correctamente.', 'success');
            } catch (err) {
                showToast(`Error al leer rúbrica: ${err.message}`, 'error');
            } finally {
                event.target.value = '';
            }
        }

        async function handleLabFilesUpload(event) {
            const files = Array.from(event.target.files);
            if (!files.length) return;

            let loadedCount = 0;
            for (const file of files) {
                try {
                    const text = await extractTextFromFile(file);
                    if (!text || text.length < 10) {
                        showToast(`"${file.name}" no contiene texto legible suficiente.`, 'warning');
                        continue;
                    }
                    // Limpiar extensión para sugerir nombre del estudiante/laboratorio
                    const cleanName = file.name.replace(/\.[^/.]+$/, "").replace(/[_-]+/g, " ");
                    submissions.push({
                        id: 'lab_' + Date.now() + '_' + Math.random().toString(36).substr(2, 6),
                        studentName: cleanName,
                        fileName: file.name,
                        content: text,
                        status: 'pending',
                        errorMsg: null,
                        evaluation: null
                    });
                    loadedCount++;
                } catch (err) {
                    showToast(`Error en "${file.name}": ${err.message}`, 'error');
                }
            }

            if (loadedCount > 0) {
                cachedGroupSynthesis = null;
                renderSubmissions();
                updateDashboardState();
                showToast(`${loadedCount} trabajo(s) agregado(s) a la bandeja.`, 'success');
            }
            event.target.value = '';
        }

        function addManualSubmission() {
            const nameInput = document.getElementById('manual-student-name');
            const textInput = document.getElementById('manual-lab-text');
            const studentName = nameInput.value.trim() || `Estudiante #${submissions.length + 1}`;
            const content = textInput.value.trim();

            if (content.length < 15) {
                showToast('Por favor ingresa el contenido del trabajo (mínimo 15 caracteres).', 'warning');
                return;
            }

            submissions.push({
                id: 'lab_' + Date.now() + '_' + Math.random().toString(36).substr(2, 6),
                studentName,
                fileName: 'Entrada manual',
                content,
                status: 'pending',
                errorMsg: null,
                evaluation: null
            });

            nameInput.value = '';
            textInput.value = '';
            cachedGroupSynthesis = null;
            renderSubmissions();
            updateDashboardState();
            showToast(`Trabajo de "${studentName}" agregado.`, 'success');
        }

        function updateStudentName(id, newName) {
            const item = submissions.find(s => s.id === id);
            if (item && newName.trim()) {
                item.studentName = newName.trim();
                cachedGroupSynthesis = null;
                if (item.status === 'evaluated' && window.saveEvaluatedWorkToCloud) {
                    window.saveEvaluatedWorkToCloud(item);
                }
            }
        }

        function deleteSubmission(id) {
            window.submissions = window.submissions.filter(s => s.id !== id);
            submissions = window.submissions;
            window.cachedGroupSynthesis = null;
            cachedGroupSynthesis = null;
            if (window.deleteWorkFromCloud) {
                window.deleteWorkFromCloud(id);
            }
            renderSubmissions();
            updateDashboardState();
        }

        function clearAllSubmissions() {
            const idsToDelete = window.submissions.map(s => s.id);
            window.submissions = [];
            submissions = window.submissions;
            window.cachedGroupSynthesis = null;
            cachedGroupSynthesis = null;
            if (window.deleteWorkFromCloud) {
                idsToDelete.forEach(id => window.deleteWorkFromCloud(id));
            }
            renderSubmissions();
            updateDashboardState();
            showToast('Historial y lista de trabajos vaciados.', 'info');
        }

        function clearRubric() {
            document.getElementById('rubric-text').value = '';
            cachedGroupSynthesis = null;
            if (window.saveRubricToCloud) window.saveRubricToCloud('');
            updateDashboardState();
        }

        // ==========================================
        // 3. DATOS DE DEMOSTRACIÓN RÁPIDA
        // ==========================================
        function loadSampleRubric() {
            const sampleText = `RÚBRICA DE EVALUACIÓN - LABORATORIO DE TERMODINÁMICA Y TRANSFERENCIA DE CALOR (ESCALA 0.0 A 5.0)

Criterio 1: Dominio Conceptual y Fundamentación Teórica (Peso 30%)
- Define con precisión las leyes de la termodinámica aplicadas (conducción, convección, radiación) y relaciona las variables físicas sin errores conceptuales.

Criterio 2: Rigor Metodológico y Tratamiento de Datos (Peso 30%)
- Describe el montaje experimental, registra mediciones con unidades del Sistema Internacional (SI) y realiza cálculos de propagación de incertidumbre.

Criterio 3: Análisis Crítico de Resultados (Peso 25%)
- Contrasta los valores experimentales frente a los teóricos, explica las desviaciones físicas (pérdidas térmicas) y valida hipótesis.

Criterio 4: Coherencia Argumentativa y Síntesis (Peso 15%)
- Estructura el informe con claridad científica, redacción técnica precisa y conclusiones directamente respaldadas por la evidencia empírica.`;
            document.getElementById('rubric-text').value = sampleText;
            if (window.saveRubricToCloud) window.saveRubricToCloud(sampleText);
            cachedGroupSynthesis = null;
            updateDashboardState();
            showToast('Rúbrica de ejemplo cargada.', 'success');
        }

        function loadSampleSubmissions() {
            const samples = [
                {
                    studentName: "Lab 01 - Camila Restrepo",
                    fileName: "Lab01_Camila_Restrepo.pdf",
                    content: `INFORME DE LABORATORIO: TRANSFERENCIA DE CALOR POR CONDUCCIÓN EN BARRAS METÁLICAS
1. Marco Teórico: La conducción térmica se rige por la Ley de Fourier, donde el flujo de calor q = -k * A * (dT/dx). El signo negativo indica que el calor fluye desde la región de mayor temperatura hacia la de menor temperatura.
2. Metodología: Se emplearon barras cilíndricas de cobre (k_teórico = 385 W/m·K) y aluminio (k_teórico = 205 W/m·K) de 0.30 m de longitud y 0.025 m de diámetro. Se registraron temperaturas en 5 termopares cada 60 segundos hasta alcanzar estado estacionario, considerando incertidumbre instrumental de ±0.5 K.
3. Resultados y Análisis: Para el cobre se obtuvo k_exp = 368.4 ± 14.2 W/m·K (error relativo del 4.3%). Esta leve subestimación se debe a pérdidas convectivas radiales hacia el ambiente a pesar del aislamiento de fibra de vidrio, así como resistencia térmica de contacto en la interfaz con la fuente de calor.
4. Conclusiones: Se verificó experimentalmente la linealidad del gradiente térmico en régimen estacionario. La conductividad del cobre resultó 1.82 veces superior a la del aluminio, concordando con la teoría electrónica de conducción en metales.`
                },
                {
                    studentName: "Lab 02 - Andrés Felipe Gómez",
                    fileName: "Lab02_Andres_Gomez.docx",
                    content: `LABORATORIO DE CALOR
En este laboratorio medimos cómo se calienta una barra de cobre y una de aluminio. La ley de Fourier dice que el calor pasa por los metales.
Metodología: Pusimos el calentador en un lado de la barra y medimos la temperatura con unos sensores. Anotamos los números en una tabla: en el cobre subió hasta 85 grados y en el otro lado estaba en 32 grados. En el aluminio subió hasta 80 grados y al final 28 grados.
Cálculos: Calculamos la k y nos dio 310 para el cobre y 170 para el aluminio. Los valores son un poco diferentes a los del libro porque el laboratorio tenía aire acondicionado y los sensores no estaban bien pegados.
Conclusión: El cobre conduce más calor que el aluminio porque se calentó más rápido al otro lado. El experimento salió bien aunque hubo errores.`
                },
                {
                    studentName: "Lab 03 - Valentina Morales",
                    fileName: "Lab03_Valentina_Morales.pdf",
                    content: `PRÁCTICA 3: CONDUCCIÓN TÉRMICA UNIDIMENSIONAL
Introducción: Según la Primera Ley de la Termodinámica y la Ley de Fourier, en estado estacionario sin generación interna de calor, la tasa de transferencia de calor permanece constante a lo largo del eje axial de una barra aislada.
Procedimiento: Se midió el gradiente térmico dT/dx en barras de cobre y acero inoxidable usando termopares tipo K calibrados (incertidumbre ±0.2 °C) y potencia eléctrica de entrada P = 45.0 W.
Análisis: Obtuvimos k_cobre = 374 W/m·K (error 2.8%) y k_acero = 15.8 W/m·K (error 3.1%). Sin embargo, no se cuantificó matemáticamente la propagación del error en las mediciones de diámetro ni la potencia disipada por radiación en los extremos. Se observa claramente que el gradiente térmico en el acero es mucho más pronunciado debido a su menor difusividad y conductividad térmica.
Conclusiones: Los datos confirman la proporcionalidad inversa entre conductividad térmica y gradiente de temperatura para un flujo de calor constante.`
                }
            ];

            samples.forEach(s => {
                submissions.push({
                    id: 'lab_' + Date.now() + '_' + Math.random().toString(36).substr(2, 6),
                    studentName: s.studentName,
                    fileName: s.fileName,
                    content: s.content,
                    status: 'pending',
                    errorMsg: null,
                    evaluation: null
                });
            });

            cachedGroupSynthesis = null;
            renderSubmissions();
            updateDashboardState();
            showToast('3 trabajos de muestra cargados.', 'success');
        }

        function loadQuickDemo() {
            loadSampleRubric();
            if (submissions.length === 0) {
                loadSampleSubmissions();
            }
        }

        // ==========================================
        // 4. INTEGRACIÓN CON GEMINI API (CON REINTENTOS)
        // ==========================================
        async function callGeminiWithBackoff(payload, maxRetries = 3) {
            const url = `https://generativelanguage.googleapis.com/v1beta/models/${GEMINI_MODEL}:generateContent?key=${apiKey}`;
            let delay = 1000;

            for (let attempt = 0; attempt <= maxRetries; attempt++) {
                try {
                    const response = await fetch(url, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });

                    if (!response.ok) {
                        const errData = await response.json().catch(() => ({}));
                        throw new Error(errData.error?.message || `HTTP ${response.status}`);
                    }

                    const data = await response.json();
                    const text = data?.candidates?.[0]?.content?.parts?.[0]?.text;
                    if (!text) {
                        throw new Error('Respuesta vacía del modelo.');
                    }
                    return text;
                } catch (error) {
                    if (attempt === maxRetries) {
                        throw error;
                    }
                    await new Promise(resolve => setTimeout(resolve, delay));
                    delay *= 2;
                }
            }
        }

        // Evaluación Individual de un Trabajo
        async function evaluateSubmission(id) {
            const rubric = document.getElementById('rubric-text').value.trim();
            if (!rubric || rubric.length < 15) {
                showToast('Primero debes ingresar o subir una Rúbrica de Evaluación.', 'warning');
                document.getElementById('rubric-text').focus();
                return;
            }

            const item = submissions.find(s => s.id === id);
            if (!item) return;

            item.status = 'evaluating';
            item.errorMsg = null;
            renderSubmissions();
            updateDashboardState();

            const systemPrompt = `Actúa como un evaluador académico experto en pedagogía universitaria, evaluación cognitiva y retroalimentación formativa.
Tu tarea es evaluar el trabajo o informe de laboratorio de un estudiante cruzándolo estrictamente con la Rúbrica de Evaluación proporcionada.
Evalúa el nivel de procesamiento cognitivo (comprensión, aplicación, análisis crítico y síntesis), evitando calificaciones arbitrarias.
Todas las puntuaciones deben estar estrictamente en la escala de 0.0 a 5.0 (con un decimal).
Responde exclusivamente en español y cumpliendo el esquema JSON solicitado.`;

            const userPrompt = `RÚBRICA DE EVALUACIÓN:
"""
${rubric}
"""

ESTUDIANTE / IDENTIFICADOR: ${item.studentName}
CONTENIDO DEL TRABAJO / LABORATORIO:
"""
${item.content.slice(0, 28000)}
"""

Genera la evaluación detallada con:
1. "valoracion_conceptual": Análisis cualitativo profundo del dominio del tema, coherencia cognitiva, fortalezas evidenciadas y nivel de cumplimiento de los objetivos de aprendizaje.
2. "recomendaciones_mejora": Lista de 3 a 5 acciones concretas, pedagógicas y accionables para que el estudiante corrija errores conceptuales o metodológicos y profundice en el tema.
3. "desglose_criterios": Evaluación criterio por criterio según la rúbrica, asignando puntaje de 0.0 a 5.0 y una justificación breve basada en evidencia del texto.
4. "nota_final": Calificación final ponderada o promedio de 0.0 a 5.0.`;

            const payload = {
                contents: [{ parts: [{ text: userPrompt }] }],
                systemInstruction: { parts: [{ text: systemPrompt }] },
                generationConfig: {
                    responseMimeType: "application/json",
                    responseSchema: {
                        type: "OBJECT",
                        properties: {
                            valoracion_conceptual: { type: "STRING" },
                            recomendaciones_mejora: {
                                type: "ARRAY",
                                items: { type: "STRING" }
                            },
                            desglose_criterios: {
                                type: "ARRAY",
                                items: {
                                    type: "OBJECT",
                                    properties: {
                                        criterio: { type: "STRING" },
                                        puntaje: { type: "NUMBER" },
                                        justificacion: { type: "STRING" }
                                    },
                                    required: ["criterio", "puntaje", "justificacion"]
                                }
                            },
                            nota_final: { type: "NUMBER" }
                        },
                        required: ["valoracion_conceptual", "recomendaciones_mejora", "desglose_criterios", "nota_final"]
                    }
                }
            };

            try {
                const rawJson = await callGeminiWithBackoff(payload);
                const parsed = JSON.parse(rawJson);

                // Asegurar límites 0.0 a 5.0
                parsed.nota_final = Math.min(5, Math.max(0, Number(parsed.nota_final) || 0));
                if (Array.isArray(parsed.desglose_criterios)) {
                    parsed.desglose_criterios.forEach(c => {
                        c.puntaje = Math.min(5, Math.max(0, Number(c.puntaje) || 0));
                    });
                }

                item.evaluation = parsed;
                item.status = 'evaluated';
                item.evaluatedAt = Date.now();
                cachedGroupSynthesis = null;
                if (window.saveEvaluatedWorkToCloud) {
                    await window.saveEvaluatedWorkToCloud(item);
                }
                showToast(`Evaluación guardada: ${item.studentName} (${parsed.nota_final.toFixed(1)}/5.0)`, 'success');
            } catch (err) {
                item.status = 'error';
                item.errorMsg = err.message || 'Error de conexión con Gemini API.';
                showToast(`Error al evaluar "${item.studentName}": ${item.errorMsg}`, 'error');
            }

            renderSubmissions();
            updateDashboardState();
        }

        async function evaluateAllPending() {
            const rubric = document.getElementById('rubric-text').value.trim();
            if (!rubric || rubric.length < 15) {
                showToast('Primero ingresa o sube una Rúbrica de Evaluación.', 'warning');
                return;
            }

            const pendingItems = submissions.filter(s => s.status === 'pending' || s.status === 'error');
            if (!pendingItems.length) return;

            showToast(`Iniciando evaluación de ${pendingItems.length} trabajo(s)...`, 'info');
            for (const item of pendingItems) {
                await evaluateSubmission(item.id);
            }
        }

        // Síntesis Grupal con Gemini (para PDF General e Infografía)
        async function getGroupSynthesis() {
            const evaluated = submissions.filter(s => s.status === 'evaluated' && s.evaluation);
            if (!evaluated.length) throw new Error('No hay trabajos evaluados.');

            if (cachedGroupSynthesis) {
                return cachedGroupSynthesis;
            }

            const rubric = document.getElementById('rubric-text').value.trim();
            const summaryData = evaluated.map(s => ({
                estudiante: s.studentName,
                nota_final: s.evaluation.nota_final,
                valoracion: s.evaluation.valoracion_conceptual,
                criterios: s.evaluation.desglose_criterios,
                recomendaciones: s.evaluation.recomendaciones_mejora
            }));

            const prompt = `Analiza en conjunto los siguientes resultados de evaluación académica de un grupo de estudiantes basados en esta rúbrica:
RÚBRICA:
${rubric}

RESULTADOS INDIVIDUALES DEL GRUPO:
${JSON.stringify(summaryData, null, 2)}

Genera una síntesis diagnóstica grupal en español con:
1. "resumen_ejecutivo": Párrafo breve sintetizando el desempeño cognitivo general del grupo.
2. "competencias_logradas": Lista de 3 a 4 fortalezas o competencias mejor logradas por la mayoría del grupo.
3. "brechas_cognitivas": Lista de 3 a 4 debilidades cognitivas, errores conceptuales o brechas metodológicas comunes detectadas en el grupo.
4. "recomendaciones_docente": Lista de 4 acciones pedagógicas concretas que el docente puede implementar en la próxima sesión para reforzar los aprendizajes.`;

            const payload = {
                contents: [{ parts: [{ text: prompt }] }],
                generationConfig: {
                    responseMimeType: "application/json",
                    responseSchema: {
                        type: "OBJECT",
                        properties: {
                            resumen_ejecutivo: { type: "STRING" },
                            competencias_logradas: { type: "ARRAY", items: { type: "STRING" } },
                            brechas_cognitivas: { type: "ARRAY", items: { type: "STRING" } },
                            recomendaciones_docente: { type: "ARRAY", items: { type: "STRING" } }
                        },
                        required: ["resumen_ejecutivo", "competencias_logradas", "brechas_cognitivas", "recomendaciones_docente"]
                    }
                }
            };

            const raw = await callGeminiWithBackoff(payload);
            cachedGroupSynthesis = JSON.parse(raw);
            window.cachedGroupSynthesis = cachedGroupSynthesis;
            return cachedGroupSynthesis;
        }

        // ==========================================
        // 5. RENDERIZADO Y ACTUALIZACIÓN DEL ESTADO
        // ==========================================
        function getGradeColorClasses(grade) {
            if (grade >= 4.0) return { badge: 'bg-emerald-50 text-emerald-700 border-emerald-200', bar: 'bg-emerald-500' };
            if (grade >= 3.0) return { badge: 'bg-amber-50 text-amber-700 border-amber-200', bar: 'bg-amber-500' };
            return { badge: 'bg-rose-50 text-rose-700 border-rose-200', bar: 'bg-rose-500' };
        }

        let rubricSaveTimeout = null;
        function updateDashboardState() {
            submissions = window.submissions;
            const rubricText = document.getElementById('rubric-text').value.trim();
            clearTimeout(rubricSaveTimeout);
            rubricSaveTimeout = setTimeout(() => {
                if (window.saveRubricToCloud) window.saveRubricToCloud(rubricText);
            }, 800);

            const rubricStatusEl = document.getElementById('stat-rubric-status');
            if (rubricText.length >= 15) {
                rubricStatusEl.textContent = 'Activa';
                rubricStatusEl.className = 'px-2 py-0.5 rounded-full text-[10px] font-bold bg-emerald-50 text-emerald-700';
            } else {
                rubricStatusEl.textContent = 'Sin definir';
                rubricStatusEl.className = 'px-2 py-0.5 rounded-full text-[10px] font-bold bg-amber-50 text-amber-700';
            }

            const total = submissions.length;
            const evaluated = submissions.filter(s => s.status === 'evaluated' && s.evaluation);
            const pending = submissions.filter(s => s.status === 'pending' || s.status === 'error');

            document.getElementById('stat-total-labs').textContent = total;
            document.getElementById('stat-evaluated-labs').textContent = evaluated.length;
            document.getElementById('pending-count').textContent = pending.length;
            document.getElementById('pdf-evaluated-count').textContent = evaluated.length;
            document.getElementById('info-evaluated-count').textContent = evaluated.length;

            const savedPill = document.getElementById('saved-history-pill');
            if (evaluated.length > 0) {
                savedPill.textContent = `${evaluated.length} analizado(s) guardado(s)`;
                savedPill.classList.remove('hidden');
            } else {
                savedPill.classList.add('hidden');
            }

            const avgEl = document.getElementById('stat-avg-grade');
            if (evaluated.length > 0) {
                const avg = evaluated.reduce((acc, s) => acc + s.evaluation.nota_final, 0) / evaluated.length;
                avgEl.textContent = `${avg.toFixed(2)} / 5.0`;
            } else {
                avgEl.textContent = '-- / 5.0';
            }

            // Botón Evaluar Pendientes
            const btnEvalAll = document.getElementById('btn-evaluate-all');
            if (pending.length > 0) {
                btnEvalAll.disabled = false;
                btnEvalAll.className = 'inline-flex items-center gap-1.5 px-3.5 py-2 rounded-xl text-xs font-bold bg-indigo-50 text-indigo-700 hover:bg-indigo-100 border border-indigo-200 transition-all cursor-pointer';
            } else {
                btnEvalAll.disabled = true;
                btnEvalAll.className = 'inline-flex items-center gap-1.5 px-3.5 py-2 rounded-xl text-xs font-bold bg-slate-100 text-slate-400 border border-slate-200 transition-all cursor-not-allowed';
            }

            // Botones Globales del Banner Oscuro (PDF e Infografía)
            const btnPdf = document.getElementById('btn-global-pdf');
            const btnInfo = document.getElementById('btn-global-infographic');
            if (evaluated.length > 0) {
                btnPdf.disabled = false;
                btnPdf.className = 'w-full inline-flex items-center justify-center gap-2 px-4 py-2.5 rounded-xl text-xs sm:text-sm font-bold bg-indigo-600 hover:bg-indigo-500 text-white shadow-md shadow-indigo-950/50 transition-all cursor-pointer';
                
                btnInfo.disabled = false;
                btnInfo.className = 'w-full inline-flex items-center justify-center gap-2 px-4 py-2.5 rounded-xl text-xs sm:text-sm font-bold bg-amber-500 hover:bg-amber-400 text-slate-950 shadow-md shadow-amber-950/30 transition-all cursor-pointer';
            } else {
                btnPdf.disabled = true;
                btnPdf.className = 'w-full inline-flex items-center justify-center gap-2 px-4 py-2.5 rounded-xl text-xs sm:text-sm font-bold bg-indigo-600/35 text-indigo-200/60 border border-indigo-500/30 transition-all cursor-not-allowed';
                
                btnInfo.disabled = true;
                btnInfo.className = 'w-full inline-flex items-center justify-center gap-2 px-4 py-2.5 rounded-xl text-xs sm:text-sm font-bold bg-amber-500/25 text-amber-200/60 border border-amber-400/30 transition-all cursor-not-allowed';
            }

            // Empty state vs lista
            const emptyState = document.getElementById('empty-state');
            const clearAllBtn = document.getElementById('btn-clear-all-labs');
            if (total === 0) {
                emptyState.classList.remove('hidden');
                clearAllBtn.classList.add('hidden');
            } else {
                emptyState.classList.add('hidden');
                clearAllBtn.classList.remove('hidden');
            }
        }

        function renderSubmissions() {
            submissions = window.submissions;
            const container = document.getElementById('submissions-list');
            container.innerHTML = '';

            submissions.forEach((item) => {
                const card = document.createElement('div');
                const isEvaluating = item.status === 'evaluating';
                const isEvaluated = item.status === 'evaluated' && item.evaluation;
                const isError = item.status === 'error';

                card.className = `bg-white rounded-2xl border ${isEvaluating ? 'border-indigo-500 evaluating-card' : 'border-slate-200'} shadow-sm overflow-hidden transition-all`;

                // Badge de estado
                let statusBadge = '';
                if (item.status === 'pending') {
                    statusBadge = `<span class="inline-flex items-center gap-1.5 px-2.5 py-1 rounded-full text-xs font-semibold bg-slate-100 text-slate-600 border border-slate-200">
                        <span class="w-1.5 h-1.5 rounded-full bg-slate-400"></span> Pendiente
                    </span>`;
                } else if (isEvaluating) {
                    statusBadge = `<span class="inline-flex items-center gap-1.5 px-2.5 py-1 rounded-full text-xs font-semibold bg-indigo-50 text-indigo-700 border border-indigo-200">
                        <span class="w-3 h-3 border-2 border-indigo-600 border-t-transparent rounded-full animate-spin"></span> Evaluando...
                    </span>`;
                } else if (isEvaluated) {
                    const colors = getGradeColorClasses(item.evaluation.nota_final);
                    statusBadge = `<span class="inline-flex items-center gap-1.5 px-2.5 py-1 rounded-full text-xs font-bold border ${colors.badge}">
                        <i data-lucide="check-circle-2" class="w-3.5 h-3.5"></i> Guardado: ${item.evaluation.nota_final.toFixed(1)} / 5.0
                    </span>`;
                } else if (isError) {
                    statusBadge = `<span class="inline-flex items-center gap-1.5 px-2.5 py-1 rounded-full text-xs font-semibold bg-rose-50 text-rose-700 border border-rose-200">
                        <i data-lucide="alert-circle" class="w-3.5 h-3.5"></i> Error
                    </span>`;
                }

                // Vista previa de resultados si está evaluado
                let evaluatedPreviewHTML = '';
                if (isEvaluated) {
                    const ev = item.evaluation;
                    evaluatedPreviewHTML = `
                        <div class="mt-4 pt-4 border-t border-slate-100 flex flex-col gap-3">
                            <div class="bg-slate-50 rounded-xl p-3.5 border border-slate-200/60">
                                <p class="text-[11px] font-bold uppercase tracking-wider text-indigo-600 mb-1">1. Valoración Conceptual</p>
                                <p class="text-xs sm:text-sm text-slate-700 line-clamp-3 leading-relaxed">${escapeHTML(ev.valoracion_conceptual)}</p>
                            </div>

                            <div class="grid grid-cols-1 sm:grid-cols-2 gap-2.5">
                                <div class="bg-amber-50/50 rounded-xl p-3 border border-amber-200/70">
                                    <p class="text-[11px] font-bold uppercase tracking-wider text-amber-800 mb-1">2. Recomendaciones Clave</p>
                                    <ul class="text-xs text-slate-700 space-y-1 list-disc list-inside">
                                        ${ev.recomendaciones_mejora.slice(0, 2).map(r => `<li class="truncate">${escapeHTML(r)}</li>`).join('')}
                                    </ul>
                                </div>
                                <div class="bg-indigo-50/40 rounded-xl p-3 border border-indigo-200/70">
                                    <p class="text-[11px] font-bold uppercase tracking-wider text-indigo-800 mb-1">3. Desglose Criterios (0 - 5)</p>
                                    <div class="space-y-1">
                                        ${ev.desglose_criterios.slice(0, 2).map(c => `
                                            <div class="flex items-center justify-between text-xs">
                                                <span class="text-slate-600 truncate pr-2">${escapeHTML(c.criterio)}</span>
                                                <span class="font-bold text-slate-900 shrink-0">${Number(c.puntaje).toFixed(1)}</span>
                                            </div>
                                        `).join('')}
                                    </div>
                                </div>
                            </div>
                        </div>
                    `;
                } else if (isError) {
                    evaluatedPreviewHTML = `
                        <div class="mt-3 p-3 rounded-xl bg-rose-50 border border-rose-200 text-xs text-rose-700">
                            ${escapeHTML(item.errorMsg)}
                        </div>
                    `;
                }

                card.innerHTML = `
                    <div class="p-4 sm:p-5">
                        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3">
                            <div class="flex-1 min-w-0">
                                <div class="flex items-center gap-2">
                                    <input type="text" value="${escapeHTML(item.studentName)}" 
                                        onchange="updateStudentName('${item.id}', this.value)"
                                        title="Haz clic para editar el nombre del estudiante o laboratorio"
                                        class="font-bold text-slate-900 text-sm sm:text-base bg-transparent hover:bg-slate-100 focus:bg-white focus:ring-2 focus:ring-indigo-200 rounded-lg px-1.5 py-0.5 -ml-1.5 outline-none transition-all w-full max-w-md">
                                </div>
                                <p class="text-xs text-slate-400 mt-0.5 flex items-center gap-2">
                                    <span>Archivo: ${escapeHTML(item.fileName)}</span>
                                    <span>•</span>
                                    <span>${item.content.length.toLocaleString()} caracteres</span>
                                </p>
                            </div>

                            <div class="flex items-center flex-wrap gap-2 shrink-0">
                                ${statusBadge}
                                
                                ${isEvaluated ? `
                                    <button onclick="openIndividualModal('${item.id}')" class="inline-flex items-center gap-1.5 px-3 py-1.5 rounded-xl text-xs font-semibold bg-indigo-600 hover:bg-indigo-700 text-white shadow-sm transition-colors">
                                        <i data-lucide="eye" class="w-3.5 h-3.5"></i>
                                        Ver Informe Completo
                                    </button>
                                    <button onclick="evaluateSubmission('${item.id}')" title="Re-evaluar trabajo" class="p-1.5 rounded-xl text-slate-400 hover:text-indigo-600 hover:bg-indigo-50 transition-colors">
                                        <i data-lucide="refresh-cw" class="w-4 h-4"></i>
                                    </button>
                                ` : `
                                    <button onclick="evaluateSubmission('${item.id}')" ${isEvaluating ? 'disabled' : ''} 
                                        class="inline-flex items-center gap-1.5 px-3.5 py-1.5 rounded-xl text-xs font-semibold ${isEvaluating ? 'bg-slate-200 text-slate-500 cursor-not-allowed' : 'bg-indigo-600 hover:bg-indigo-700 text-white shadow-sm'} transition-colors">
                                        <i data-lucide="sparkles" class="w-3.5 h-3.5"></i>
                                        ${isEvaluating ? 'Analizando...' : 'Evaluar Trabajo'}
                                    </button>
                                `}

                                <button onclick="deleteSubmission('${item.id}')" title="Eliminar entrega" class="p-1.5 rounded-xl text-slate-400 hover:text-rose-600 hover:bg-rose-50 transition-colors">
                                    <i data-lucide="trash-2" class="w-4 h-4"></i>
                                </button>
                            </div>
                        </div>

                        ${evaluatedPreviewHTML}
                    </div>
                `;

                container.appendChild(card);
            });

            lucide.createIcons({ nodes: [container] });
        }

        // ==========================================
        // 6. MODAL DE INFORME INDIVIDUAL
        // ==========================================
        function openIndividualModal(id) {
            const item = submissions.find(s => s.id === id);
            if (!item || !item.evaluation) return;

            activeModalSubmissionId = id;
            const ev = item.evaluation;
            const colors = getGradeColorClasses(ev.nota_final);

            document.getElementById('modal-student-title').textContent = item.studentName;
            const gradeBadge = document.getElementById('modal-grade-badge');
            gradeBadge.textContent = `${ev.nota_final.toFixed(1)} / 5.0`;
            gradeBadge.className = `px-4 py-1.5 rounded-xl font-extrabold text-base sm:text-lg shadow-sm border ${colors.badge}`;

            const body = document.getElementById('modal-individual-body');
            body.innerHTML = `
                <!-- 1. Valoración Conceptual -->
                <div class="bg-slate-50 rounded-2xl p-5 border border-slate-200">
                    <div class="flex items-center gap-2 mb-2.5">
                        <div class="w-7 h-7 rounded-lg bg-indigo-600 text-white flex items-center justify-center">
                            <i data-lucide="brain" class="w-4 h-4"></i>
                        </div>
                        <h4 class="font-bold text-slate-900 text-sm sm:text-base">1. Valoración Conceptual y Dominio Cognitivo</h4>
                    </div>
                    <p class="text-xs sm:text-sm text-slate-700 leading-relaxed whitespace-pre-line">${escapeHTML(ev.valoracion_conceptual)}</p>
                </div>

                <!-- 2. Recomendaciones de Mejora -->
                <div class="bg-amber-50/60 rounded-2xl p-5 border border-amber-200">
                    <div class="flex items-center gap-2 mb-3">
                        <div class="w-7 h-7 rounded-lg bg-amber-500 text-white flex items-center justify-center">
                            <i data-lucide="compass" class="w-4 h-4"></i>
                        </div>
                        <h4 class="font-bold text-amber-950 text-sm sm:text-base">2. Recomendaciones Pedagógicas de Mejora</h4>
                    </div>
                    <ul class="space-y-2.5">
                        ${ev.recomendaciones_mejora.map((rec, idx) => `
                            <li class="flex items-start gap-2.5 text-xs sm:text-sm text-slate-800 bg-white/80 p-3 rounded-xl border border-amber-200/60">
                                <span class="w-5 h-5 rounded-full bg-amber-100 text-amber-800 font-bold text-xs flex items-center justify-center shrink-0 mt-0.5">${idx + 1}</span>
                                <span class="leading-relaxed">${escapeHTML(rec)}</span>
                            </li>
                        `).join('')}
                    </ul>
                </div>

                <!-- 3. Verificación de Cuantificación (0 a 5) -->
                <div class="bg-white rounded-2xl p-5 border border-slate-200">
                    <div class="flex items-center justify-between mb-4">
                        <div class="flex items-center gap-2">
                            <div class="w-7 h-7 rounded-lg bg-emerald-600 text-white flex items-center justify-center">
                                <i data-lucide="calculator" class="w-4 h-4"></i>
                            </div>
                            <h4 class="font-bold text-slate-900 text-sm sm:text-base">3. Verificación de Cuantificación por Criterio (0.0 - 5.0)</h4>
                        </div>
                        <span class="text-xs font-bold text-slate-500">Nota Final: <strong class="text-slate-900 text-sm">${ev.nota_final.toFixed(2)} / 5.0</strong></span>
                    </div>

                    <div class="space-y-3">
                        ${ev.desglose_criterios.map(c => {
                            const pct = Math.min(100, Math.max(0, (c.puntaje / 5) * 100));
                            const cColors = getGradeColorClasses(c.puntaje);
                            return `
                                <div class="p-3.5 rounded-xl bg-slate-50 border border-slate-200/80">
                                    <div class="flex items-center justify-between gap-3 mb-1.5">
                                        <span class="font-bold text-xs sm:text-sm text-slate-800">${escapeHTML(c.criterio)}</span>
                                        <span class="px-2.5 py-0.5 rounded-lg text-xs font-extrabold border ${cColors.badge} shrink-0">
                                            ${Number(c.puntaje).toFixed(1)} / 5.0
                                        </span>
                                    </div>
                                    <div class="w-full h-1.5 bg-slate-200 rounded-full overflow-hidden mb-2">
                                        <div class="h-full ${cColors.bar} rounded-full" style="width: ${pct}%"></div>
                                    </div>
                                    <p class="text-xs text-slate-600 leading-relaxed">${escapeHTML(c.justificacion)}</p>
                                </div>
                            `;
                        }).join('')}
                    </div>
                </div>
            `;

            document.getElementById('individual-modal').classList.remove('hidden');
            lucide.createIcons({ nodes: [body] });
        }

        function closeIndividualModal() {
            document.getElementById('individual-modal').classList.add('hidden');
            activeModalSubmissionId = null;
        }

        function copyIndividualReport() {
            const item = submissions.find(s => s.id === activeModalSubmissionId);
            if (!item || !item.evaluation) return;
            const ev = item.evaluation;

            const textReport = `INFORME DE EVALUACIÓN COGNITIVA
Estudiante / Laboratorio: ${item.studentName}
Calificación Final: ${ev.nota_final.toFixed(1)} / 5.0

1. VALORACIÓN CONCEPTUAL:
${ev.valoracion_conceptual}

2. RECOMENDACIONES DE MEJORA:
${ev.recomendaciones_mejora.map((r, i) => `${i + 1}. ${r}`).join('\n')}

3. DESGLOSE POR CRITERIO (0.0 - 5.0):
${ev.desglose_criterios.map(c => `- ${c.criterio}: ${Number(c.puntaje).toFixed(1)}/5.0 -> ${c.justificacion}`).join('\n')}`;

            const tempArea = document.createElement('textarea');
            tempArea.value = textReport;
            document.body.appendChild(tempArea);
            tempArea.select();
            document.execCommand('copy');
            document.body.removeChild(tempArea);

            showToast('Retroalimentación copiada al portapapeles.', 'success');
        }

        // Descarga PDF de un solo estudiante
        function downloadSingleStudentPDF() {
            const item = submissions.find(s => s.id === activeModalSubmissionId);
            if (!item || !item.evaluation) return;
            const ev = item.evaluation;

            const { jsPDF } = window.jspdf;
            const doc = new jsPDF({ orientation: 'portrait', unit: 'mm', format: 'a4' });
            const margin = 18;
            const pageWidth = doc.internal.pageSize.getWidth();
            const contentWidth = pageWidth - margin * 2;
            let y = 20;

            function checkPage(needed = 15) {
                if (y + needed > 278) {
                    doc.addPage();
                    y = 20;
                }
            }

            // Encabezado
            doc.setFillColor(49, 46, 129);
            doc.rect(0, 0, pageWidth, 34, 'F');
            doc.setTextColor(255, 255, 255);
            doc.setFont('helvetica', 'bold');
            doc.setFontSize(15);
            doc.text('INFORME INDIVIDUAL DE EVALUACIÓN COGNITIVA', margin, 15);
            doc.setFont('helvetica', 'normal');
            doc.setFontSize(10);
            doc.text(`Estudiante: ${item.studentName}   |   Nota Final: ${ev.nota_final.toFixed(1)} / 5.0`, margin, 24);

            y = 44;

            // Sección 1
            doc.setTextColor(49, 46, 129);
            doc.setFont('helvetica', 'bold');
            doc.setFontSize(12);
            doc.text('1. Valoración Conceptual', margin, y);
            y += 6;

            doc.setTextColor(51, 65, 85);
            doc.setFont('helvetica', 'normal');
            doc.setFontSize(10);
            const valLines = doc.splitTextToSize(ev.valoracion_conceptual, contentWidth);
            valLines.forEach(line => {
                checkPage(6);
                doc.text(line, margin, y);
                y += 5.2;
            });
            y += 6;

            // Sección 2
            checkPage(14);
            doc.setTextColor(180, 83, 9);
            doc.setFont('helvetica', 'bold');
            doc.setFontSize(12);
            doc.text('2. Recomendaciones de Mejora', margin, y);
            y += 6;

            doc.setTextColor(51, 65, 85);
            doc.setFont('helvetica', 'normal');
            doc.setFontSize(10);
            ev.recomendaciones_mejora.forEach((rec, i) => {
                const recLines = doc.splitTextToSize(`${i + 1}. ${rec}`, contentWidth);
                recLines.forEach(line => {
                    checkPage(6);
                    doc.text(line, margin, y);
                    y += 5.2;
                });
                y += 2;
            });
            y += 4;

            // Sección 3
            checkPage(16);
            doc.setTextColor(6, 95, 70);
            doc.setFont('helvetica', 'bold');
            doc.setFontSize(12);
            doc.text('3. Verificación de Cuantificación (Escala 0.0 - 5.0)', margin, y);
            y += 7;

            ev.desglose_criterios.forEach(c => {
                checkPage(18);
                doc.setTextColor(15, 23, 42);
                doc.setFont('helvetica', 'bold');
                doc.setFontSize(10);
                doc.text(`• ${c.criterio}: ${Number(c.puntaje).toFixed(1)} / 5.0`, margin, y);
                y += 5;

                doc.setTextColor(71, 85, 105);
                doc.setFont('helvetica', 'normal');
                doc.setFontSize(9.5);
                const jLines = doc.splitTextToSize(c.justificacion, contentWidth - 4);
                jLines.forEach(line => {
                    checkPage(5);
                    doc.text(line, margin + 4, y);
                    y += 4.8;
                });
                y += 3;
            });

            const safeName = item.studentName.replace(/[^a-zA-Z0-9_-]/g, '_');
            doc.save(`Evaluacion_${safeName}.pdf`);
            showToast('PDF individual descargado.', 'success');
        }

        // ==========================================
        // 7. INFORME GENERAL CONSOLIDADO EN PDF
        // ==========================================
        async function generateGlobalPDF() {
            const evaluated = submissions.filter(s => s.status === 'evaluated' && s.evaluation);
            if (!evaluated.length) {
                showToast('Evalúa al menos un trabajo antes de generar el informe PDF.', 'warning');
                return;
            }

            const overlay = document.getElementById('pdf-loading-overlay');
            overlay.classList.remove('hidden');

            try {
                const synthesis = await getGroupSynthesis();
                const { jsPDF } = window.jspdf;
                const doc = new jsPDF({ orientation: 'portrait', unit: 'mm', format: 'a4' });
                const margin = 16;
                const pageWidth = doc.internal.pageSize.getWidth();
                const contentWidth = pageWidth - margin * 2;
                let y = 20;

                function checkPage(needed = 14) {
                    if (y + needed > 278) {
                        doc.addPage();
                        y = 20;
                    }
                }

                // Estadísticas
                const grades = evaluated.map(s => s.evaluation.nota_final);
                const avg = grades.reduce((a, b) => a + b, 0) / grades.length;
                const maxGrade = Math.max(...grades);
                const minGrade = Math.min(...grades);
                const passedCount = grades.filter(g => g >= 3.0).length;
                const passRate = ((passedCount / grades.length) * 100).toFixed(0);

                // Portada / Encabezado Ejecutivo
                doc.setFillColor(49, 46, 129);
                doc.rect(0, 0, pageWidth, 38, 'F');
                doc.setTextColor(255, 255, 255);
                doc.setFont('helvetica', 'bold');
                doc.setFontSize(16);
                doc.text('INFORME GENERAL DE EVALUACIÓN COGNITIVA', margin, 16);
                doc.setFont('helvetica', 'normal');
                doc.setFontSize(10);
                const dateStr = new Date().toLocaleDateString('es-ES', { year: 'numeric', month: 'long', day: 'numeric' });
                doc.text(`Consolidado Académico Grupal  •  Fecha: ${dateStr}  •  Trabajos Evaluados: ${evaluated.length}`, margin, 26);

                y = 48;

                // Cajas de Estadísticas Generales
                doc.setFillColor(248, 250, 252);
                doc.setDrawColor(203, 213, 225);
                doc.roundedRect(margin, y, contentWidth, 22, 3, 3, 'FD');

                const colW = contentWidth / 4;
                const kpis = [
                    { label: 'PROMEDIO GRUPO', val: `${avg.toFixed(2)} / 5.0` },
                    { label: 'NOTA MÁXIMA', val: `${maxGrade.toFixed(1)} / 5.0` },
                    { label: 'NOTA MÍNIMA', val: `${minGrade.toFixed(1)} / 5.0` },
                    { label: 'APROBACIÓN (>=3.0)', val: `${passRate}% (${passedCount}/${evaluated.length})` }
                ];

                kpis.forEach((k, idx) => {
                    const cx = margin + colW * idx + colW / 2;
                    doc.setTextColor(100, 116, 139);
                    doc.setFont('helvetica', 'bold');
                    doc.setFontSize(7.5);
                    doc.text(k.label, cx, y + 7, { align: 'center' });

                    doc.setTextColor(30, 27, 75);
                    doc.setFont('helvetica', 'bold');
                    doc.setFontSize(11);
                    doc.text(k.val, cx, y + 15.5, { align: 'center' });
                });

                y += 30;

                // Brechas Cognitivas Comunes
                doc.setTextColor(49, 46, 129);
                doc.setFont('helvetica', 'bold');
                doc.setFontSize(12);
                doc.text('1. Síntesis y Brechas Cognitivas Comunes del Grupo', margin, y);
                y += 6;

                doc.setTextColor(51, 65, 85);
                doc.setFont('helvetica', 'normal');
                doc.setFontSize(9.5);
                const execLines = doc.splitTextToSize(synthesis.resumen_ejecutivo, contentWidth);
                execLines.forEach(line => {
                    checkPage(5);
                    doc.text(line, margin, y);
                    y += 4.8;
                });
                y += 4;

                synthesis.brechas_cognitivas.forEach(brecha => {
                    const bLines = doc.splitTextToSize(`• ${brecha}`, contentWidth - 4);
                    bLines.forEach(line => {
                        checkPage(5);
                        doc.text(line, margin + 2, y);
                        y += 4.8;
                    });
                });

                y += 6;

                // Tabla Resumen de Calificaciones
                checkPage(24);
                doc.setTextColor(49, 46, 129);
                doc.setFont('helvetica', 'bold');
                doc.setFontSize(12);
                doc.text('2. Tabla Resumen de Calificaciones', margin, y);
                y += 5;

                // Cabecera Tabla
                doc.setFillColor(224, 231, 255);
                doc.rect(margin, y, contentWidth, 8, 'F');
                doc.setTextColor(30, 27, 75);
                doc.setFontSize(9);
                doc.text('Estudiante / Laboratorio', margin + 3, y + 5.5);
                doc.text('Estado', margin + 115, y + 5.5);
                doc.text('Nota Final', margin + 152, y + 5.5);
                y += 8;

                evaluated.forEach((s, idx) => {
                    checkPage(8);
                    if (idx % 2 === 1) {
                        doc.setFillColor(248, 250, 252);
                        doc.rect(margin, y, contentWidth, 7.5, 'F');
                    }
                    doc.setTextColor(30, 41, 59);
                    doc.setFont('helvetica', 'normal');
                    doc.setFontSize(9);
                    const truncName = s.studentName.length > 52 ? s.studentName.slice(0, 49) + '...' : s.studentName;
                    doc.text(truncName, margin + 3, y + 5);

                    const passed = s.evaluation.nota_final >= 3.0;
                    doc.setTextColor(passed ? 5 : 190, passed ? 150 : 18, passed ? 105 : 60);
                    doc.text(passed ? 'Aprobado' : 'Requiere refuerzo', margin + 115, y + 5);

                    doc.setTextColor(15, 23, 42);
                    doc.setFont('helvetica', 'bold');
                    doc.text(`${s.evaluation.nota_final.toFixed(1)} / 5.0`, margin + 152, y + 5);
                    y += 7.5;
                });

                y += 8;

                // Detalle Individual por Estudiante
                checkPage(20);
                doc.setTextColor(49, 46, 129);
                doc.setFont('helvetica', 'bold');
                doc.setFontSize(12);
                doc.text('3. Detalle Estructurado por Estudiante', margin, y);
                y += 7;

                evaluated.forEach((s, idx) => {
                    checkPage(28);
                    doc.setFillColor(241, 245, 249);
                    doc.rect(margin, y, contentWidth, 8, 'F');
                    doc.setTextColor(15, 23, 42);
                    doc.setFont('helvetica', 'bold');
                    doc.setFontSize(10);
                    doc.text(`${idx + 1}. ${s.studentName}  —  Nota: ${s.evaluation.nota_final.toFixed(1)} / 5.0`, margin + 3, y + 5.5);
                    y += 11;

                    // Valoración
                    doc.setFont('helvetica', 'bold');
                    doc.setFontSize(9);
                    doc.setTextColor(67, 56, 202);
                    doc.text('Valoración Conceptual:', margin + 2, y);
                    y += 4.5;

                    doc.setFont('helvetica', 'normal');
                    doc.setTextColor(51, 65, 85);
                    const vLines = doc.splitTextToSize(s.evaluation.valoracion_conceptual, contentWidth - 4);
                    vLines.forEach(line => {
                        checkPage(5);
                        doc.text(line, margin + 2, y);
                        y += 4.5;
                    });
                    y += 2;

                    // Recomendaciones
                    checkPage(10);
                    doc.setFont('helvetica', 'bold');
                    doc.setTextColor(180, 83, 9);
                    doc.text('Recomendaciones de Mejora:', margin + 2, y);
                    y += 4.5;

                    doc.setFont('helvetica', 'normal');
                    doc.setTextColor(51, 65, 85);
                    s.evaluation.recomendaciones_mejora.forEach(r => {
                        const rLines = doc.splitTextToSize(`- ${r}`, contentWidth - 6);
                        rLines.forEach(line => {
                            checkPage(5);
                            doc.text(line, margin + 4, y);
                            y += 4.5;
                        });
                    });
                    y += 6;
                });

                doc.save(`Informe_General_Evaluacion_Cognitiva.pdf`);
                showToast('Informe General PDF generado y descargado.', 'success');
            } catch (err) {
                showToast(`Error al generar PDF: ${err.message}`, 'error');
            } finally {
                overlay.classList.add('hidden');
            }
        }

        // ==========================================
        // 8. INFOGRAFÍA CONSOLIDADA Y EXPORTACIÓN
        // ==========================================
        async function openInfographicModal() {
            const evaluated = submissions.filter(s => s.status === 'evaluated' && s.evaluation);
            if (!evaluated.length) {
                showToast('Evalúa al menos un trabajo primero.', 'warning');
                return;
            }

            const modal = document.getElementById('infographic-modal');
            const loading = document.getElementById('infographic-loading');
            const scrollArea = document.getElementById('infographic-scroll-area');

            modal.classList.remove('hidden');
            loading.classList.remove('hidden');
            scrollArea.classList.add('hidden');

            try {
                const synthesis = await getGroupSynthesis();

                // Calcular KPIs
                const grades = evaluated.map(s => s.evaluation.nota_final);
                const avg = grades.reduce((a, b) => a + b, 0) / grades.length;
                const maxGrade = Math.max(...grades);
                const minGrade = Math.min(...grades);
                const passedCount = grades.filter(g => g >= 3.0).length;
                const passRate = Math.round((passedCount / grades.length) * 100);

                document.getElementById('info-kpi-avg').textContent = avg.toFixed(2);
                document.getElementById('info-kpi-count').textContent = evaluated.length;
                document.getElementById('info-kpi-pass').textContent = `${passRate}%`;
                document.getElementById('info-kpi-max').textContent = maxGrade.toFixed(1);
                document.getElementById('info-kpi-min').textContent = minGrade.toFixed(1);
                document.getElementById('info-subtitle').textContent = synthesis.resumen_ejecutivo;
                document.getElementById('info-date').textContent = new Date().toLocaleDateString('es-ES', { year: 'numeric', month: 'long', day: 'numeric' });

                // Listas de Fortalezas, Debilidades y Recomendaciones
                document.getElementById('info-strengths-list').innerHTML = synthesis.competencias_logradas
                    .map(item => `<li class="flex items-start gap-2"><span class="text-emerald-600 font-bold">✓</span><span>${escapeHTML(item)}</span></li>`)
                    .join('');

                document.getElementById('info-weaknesses-list').innerHTML = synthesis.brechas_cognitivas
                    .map(item => `<li class="flex items-start gap-2"><span class="text-amber-600 font-bold">!</span><span>${escapeHTML(item)}</span></li>`)
                    .join('');

                document.getElementById('info-recommendations-list').innerHTML = synthesis.recomendaciones_docente
                    .map((item, i) => `
                        <div class="bg-white/90 rounded-xl p-3 border border-indigo-200/70 flex items-start gap-2.5">
                            <span class="w-5 h-5 rounded-md bg-indigo-600 text-white text-xs font-bold flex items-center justify-center shrink-0 mt-0.5">${i + 1}</span>
                            <span>${escapeHTML(item)}</span>
                        </div>
                    `).join('');

                // Tabla resumen de todos los trabajos analizados y sus notas guardadas
                document.getElementById('info-table-badge').textContent = `${evaluated.length} trabajo(s) analizado(s)`;
                document.getElementById('info-analyzed-table-body').innerHTML = evaluated.map(s => {
                    const grade = Number(s.evaluation.nota_final || 0);
                    const c = getGradeColorClasses(grade);
                    const shortSummary = s.evaluation.valoracion_conceptual.length > 135
                        ? s.evaluation.valoracion_conceptual.slice(0, 132) + '...'
                        : s.evaluation.valoracion_conceptual;
                    return `
                        <tr class="hover:bg-slate-50/80">
                            <td class="py-2.5 pr-3 font-bold text-slate-800 align-top whitespace-nowrap">${escapeHTML(s.studentName)}</td>
                            <td class="py-2.5 px-3 text-slate-600 align-top leading-relaxed">${escapeHTML(shortSummary)}</td>
                            <td class="py-2.5 pl-3 text-right align-top whitespace-nowrap">
                                <span class="inline-block px-2 py-0.5 rounded-md font-extrabold border ${c.badge}">
                                    ${grade.toFixed(1)} / 5.0
                                </span>
                            </td>
                        </tr>
                    `;
                }).join('');

                loading.classList.add('hidden');
                scrollArea.classList.remove('hidden');

                // Renderizar Gráficos Chart.js
                renderInfographicCharts(evaluated);
                lucide.createIcons({ nodes: [scrollArea] });
            } catch (err) {
                closeInfographicModal();
                showToast(`Error al generar infografía: ${err.message}`, 'error');
            }
        }

        function renderInfographicCharts(evaluated) {
            // 1. Gráfico de barras de estudiantes
            const ctxStudents = document.getElementById('chart-students').getContext('2d');
            if (chartStudentsInstance) chartStudentsInstance.destroy();

            const labels = evaluated.map(s => s.studentName.length > 18 ? s.studentName.slice(0, 16) + '…' : s.studentName);
            const dataScores = evaluated.map(s => Number(s.evaluation.nota_final.toFixed(2)));
            const bgColors = dataScores.map(score => score >= 4.0 ? '#10b981' : (score >= 3.0 ? '#f59e0b' : '#f43f5e'));

            chartStudentsInstance = new Chart(ctxStudents, {
                type: 'bar',
                data: {
                    labels,
                    datasets: [{
                        label: 'Nota Final (0 - 5)',
                        data: dataScores,
                        backgroundColor: bgColors,
                        borderRadius: 6,
                        maxBarThickness: 36
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: {
                        y: { beginAtZero: true, max: 5, ticks: { stepSize: 1 } },
                        x: { ticks: { font: { size: 11 } } }
                    }
                }
            });

            // 2. Gráfico horizontal promedio por criterio
            const criteriaMap = new Map();
            evaluated.forEach(s => {
                (s.evaluation.desglose_criterios || []).forEach(c => {
                    const key = c.criterio.trim();
                    if (!criteriaMap.has(key)) criteriaMap.set(key, []);
                    criteriaMap.get(key).push(Number(c.puntaje) || 0);
                });
            });

            const critLabels = [];
            const critAvgs = [];
            criteriaMap.forEach((scores, name) => {
                critLabels.push(name.length > 26 ? name.slice(0, 24) + '…' : name);
                const avg = scores.reduce((a, b) => a + b, 0) / scores.length;
                critAvgs.push(Number(avg.toFixed(2)));
            });

            const ctxCriteria = document.getElementById('chart-criteria').getContext('2d');
            if (chartCriteriaInstance) chartCriteriaInstance.destroy();

            chartCriteriaInstance = new Chart(ctxCriteria, {
                type: 'bar',
                data: {
                    labels: critLabels,
                    datasets: [{
                        label: 'Promedio Criterio',
                        data: critAvgs,
                        backgroundColor: '#6366f1',
                        borderRadius: 6,
                        maxBarThickness: 26
                    }]
                },
                options: {
                    indexAxis: 'y',
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: {
                        x: { beginAtZero: true, max: 5, ticks: { stepSize: 1 } },
                        y: { ticks: { font: { size: 11 } } }
                    }
                }
            });
        }

        function closeInfographicModal() {
            document.getElementById('infographic-modal').classList.add('hidden');
        }

        async function exportInfographicPNG() {
            const element = document.getElementById('infographic-canvas');
            try {
                showToast('Exportando infografía como imagen PNG...', 'info');
                const canvas = await html2canvas(element, { scale: 2, useCORS: true, backgroundColor: '#ffffff' });
                const link = document.createElement('a');
                link.download = 'Infografia_Evaluacion_Cognitiva.png';
                link.href = canvas.toDataURL('image/png');
                link.click();
                showToast('Infografía PNG descargada.', 'success');
            } catch (err) {
                showToast('No se pudo exportar la imagen PNG.', 'error');
            }
        }

        async function exportInfographicPDF() {
            const element = document.getElementById('infographic-canvas');
            try {
                showToast('Exportando infografía a PDF...', 'info');
                const canvas = await html2canvas(element, { scale: 2, useCORS: true, backgroundColor: '#ffffff' });
                const imgData = canvas.toDataURL('image/png');
                const { jsPDF } = window.jspdf;
                const pdf = new jsPDF({
                    orientation: canvas.width > canvas.height ? 'landscape' : 'portrait',
                    unit: 'px',
                    format: [canvas.width, canvas.height]
                });
                pdf.addImage(imgData, 'PNG', 0, 0, canvas.width, canvas.height);
                pdf.save('Infografia_Evaluacion_Cognitiva.pdf');
                showToast('Infografía PDF descargada.', 'success');
            } catch (err) {
                showToast('No se pudo exportar la infografía a PDF.', 'error');
            }
        }
    </script>
</body>
</html>
