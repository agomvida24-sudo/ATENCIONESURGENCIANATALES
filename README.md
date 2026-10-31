# ATENCIONESURGENCIANATALES
ATENCION DE URGENCIAS ULTIMA ESPERANZA
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Urgencias Puerto Natales - Personas en espera</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap');
        body {
            font-family: 'Inter', system-ui, -apple-system, sans-serif;
            background-color: #f8fafc;
        }
        .header-blue {
            color: #0d3b66;
        }
        .bg-header-blue {
            background-color: #0d3b66;
        }
        .card-border {
            border: 1px solid #e2e8f0;
        }
        .bg-banner-green {
            background-color: #e6f4ea;
            border-color: #ceead6;
            color: #137333;
        }
    </style>
</head>
<body class="text-slate-800 min-h-screen flex flex-col justify-between antialiased">

    <div>
        <!-- Encabezado Institucional -->
        <header class="bg-white border-b border-slate-200 sticky top-0 z-40 shadow-sm">
            <div class="max-w-3xl mx-auto px-4 py-3 flex items-center justify-between">
                <div class="flex items-center space-x-3">
                    <div class="flex flex-col border-r border-slate-300 pr-3">
                        <span class="text-[10px] font-bold uppercase tracking-wider text-slate-500">Servicio de Salud</span>
                        <span class="text-xs md:text-sm font-extrabold header-blue leading-none">Magallanes</span>
                    </div>
                    <div>
                        <h1 class="font-bold header-blue text-xs md:text-base leading-tight">
                            Red de Salud Última Esperanza
                        </h1>
                        <p class="text-[11px] text-slate-500 font-medium">Puerto Natales</p>
                    </div>
                </div>

                <div class="flex items-center space-x-2">
                    <!-- Botón Acceso Admin -->
                    <button onclick="openAdminAuth()" id="btn-admin-access" class="inline-flex items-center space-x-1.5 px-3 py-1.5 bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-semibold rounded-lg transition">
                        <i data-lucide="lock" class="w-3.5 h-3.5 text-slate-500"></i>
                        <span class="hidden sm:inline">Acceso Personal</span>
                    </button>
                    <!-- Indicador de Admin Activo (Oculto por defecto) -->
                    <button onclick="openAdminPanel()" id="badge-admin-logged" class="hidden inline-flex items-center space-x-1.5 px-3 py-1.5 bg-amber-100 border border-amber-300 text-amber-900 text-xs font-bold rounded-lg animate-pulse">
                        <i data-lucide="user-check" class="w-3.5 h-3.5 text-amber-700"></i>
                        <span>Modo Admin</span>
                    </button>
                </div>
            </div>
        </header>

        <main class="max-w-3xl mx-auto px-4 py-6 space-y-5">

            <!-- Encabezado de la página -->
            <div class="flex flex-col sm:flex-row sm:items-end justify-between gap-3">
                <div>
                    <span class="text-[11px] font-bold uppercase tracking-widest text-slate-400">Urgencias Puerto Natales</span>
                    <h2 class="text-2xl md:text-3xl font-extrabold header-blue">Personas en espera</h2>
                    <p class="text-xs md:text-sm text-slate-500 mt-1">Consulta los últimos reportes de nuestros centros de urgencia.</p>
                </div>

                <button id="btn-refresh" onclick="loadPublicData(true)" class="self-start sm:self-auto inline-flex items-center justify-center px-4 py-2 bg-white border-2 border-[#0d3b66] text-[#0d3b66] hover:bg-slate-50 active:bg-slate-100 rounded-xl font-bold text-xs md:text-sm transition-all duration-200 shadow-sm">
                    <i data-lucide="rotate-cw" id="refresh-icon" class="w-4 h-4 mr-2"></i>
                    <span>Actualizar</span>
                </button>
            </div>

            <!-- Banner verde destacado: Menor número reportado -->
            <div id="highlight-banner" class="bg-banner-green border rounded-xl p-3.5 flex items-center space-x-3 transition-all duration-300">
                <div class="w-6 h-6 rounded-full bg-[#137333] text-white flex items-center justify-center flex-shrink-0">
                    <i data-lucide="check" class="w-4 h-4 stroke-[3]"></i>
                </div>
                <div class="text-xs md:text-sm font-semibold">
                    <span>Menor número reportado</span>
                    <span class="font-normal block text-xs text-[#0f5223] mt-0.5" id="highlight-detail">
                        Cargando información...
                    </span>
                </div>
            </div>

            <!-- Timestamp de la consulta -->
            <div class="text-xs text-slate-500 px-1 flex justify-between items-center">
                <span>Consulta realizada: <strong id="timestamp" class="text-slate-700">--/--/---- --:--</strong></span>
                <span class="text-[10px] bg-slate-200 text-slate-600 px-2 py-0.5 rounded font-mono">En tiempo real</span>
            </div>

            <!-- Tarjeta 1: UEH Hospital Dr. Augusto Essmann Burgos -->
            <div class="bg-white rounded-2xl card-border shadow-sm overflow-hidden transition-all duration-200 hover:shadow-md">
                <div class="grid grid-cols-1 md:grid-cols-12">
                    
                    <div class="md:col-span-5 relative bg-slate-200 min-h-[190px]">
                        <img src="https://placehold.co/600x450/0d3b66/ffffff?text=UEH+Hospital+Puerto+Natales" 
                             alt="UEH Hospital Dr. Augusto Essmann Burgos" 
                             class="w-full h-full object-cover min-h-[190px]">
                        <div class="absolute top-3 left-3 bg-[#0d3b66] text-white text-[10px] px-2.5 py-0.5 rounded-full font-bold shadow">
                            Hospitalaria · Mediana Complejidad
                        </div>
                    </div>

                    <div class="md:col-span-7 p-5 flex flex-col justify-between space-y-4">
                        <div>
                            <div class="flex items-center justify-between">
                                <h3 class="text-lg md:text-xl font-extrabold header-blue">
                                    UEH Hospital Dr. Augusto Essmann Burgos
                                </h3>
                            </div>
                            <p class="text-xs text-slate-400 font-medium mt-0.5">Unidad de Emergencia Hospitalaria</p>
                        </div>

                        <!-- Número de pacientes en espera -->
                        <div class="grid grid-cols-2 gap-2 py-2 border-y border-slate-100">
                            <div>
                                <span class="text-xs font-semibold text-slate-400 block">Pacientes en espera</span>
                                <div class="flex items-baseline space-x-2">
                                    <span id="ueh-count" class="text-4xl font-extrabold header-blue leading-none mt-1 block">0</span>
                                    <span id="ueh-status-badge" class="text-[10px] px-2 py-0.5 rounded-md font-bold bg-emerald-100 text-emerald-800">Normal</span>
                                </div>
                            </div>
                            <div class="border-l border-slate-100 pl-4 flex flex-col justify-center">
                                <span class="text-xs font-semibold text-slate-400 block">Último reporte</span>
                                <div class="flex items-center space-x-1 mt-1 text-slate-700 font-bold text-xs md:text-sm">
                                    <i data-lucide="clock" class="w-4 h-4 text-slate-400"></i>
                                    <span id="ueh-report">Hace instantes</span>
                                </div>
                            </div>
                        </div>

                        <div class="bg-slate-50 rounded-xl p-3 space-y-1.5 text-xs text-slate-600">
                            <div class="flex items-start space-x-2">
                                <i data-lucide="map-pin" class="w-3.5 h-3.5 text-slate-400 mt-0.5 flex-shrink-0"></i>
                                <span><strong>Dirección:</strong> Ignacio Carrera Pinto N° 537, Puerto Natales</span>
                            </div>
                            <div class="flex items-start space-x-2">
                                <i data-lucide="clock" class="w-3.5 h-3.5 text-slate-400 mt-0.5 flex-shrink-0"></i>
                                <span><strong>Horario de atención:</strong> 24 horas continuo</span>
                            </div>
                        </div>

                        <div class="pt-1 flex items-center justify-between text-xs font-bold">
                            <button onclick="toggleModal('modal-info')" class="inline-flex items-center text-[#0d3b66] hover:underline">
                                <i data-lucide="info" class="w-3.5 h-3.5 mr-1"></i>
                                <span>Más información</span>
                            </button>

                            <a href="https://maps.google.com/?q=Ignacio+Carrera+Pinto+537,+Puerto+Natales" 
                               target="_blank" 
                               rel="noopener noreferrer"
                               class="inline-flex items-center text-slate-600 hover:text-[#0d3b66] transition">
                                <i data-lucide="map-pin" class="w-3.5 h-3.5 mr-1 text-[#0d3b66]"></i>
                                <span>Ver ubicación</span>
                                <i data-lucide="chevron-right" class="w-3.5 h-3.5 ml-0.5"></i>
                            </a>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Tarjeta 2: SAPU Dr. Juan Lozic Pérez -->
            <div class="bg-white rounded-2xl card-border shadow-sm overflow-hidden transition-all duration-200 hover:shadow-md">
                <div class="grid grid-cols-1 md:grid-cols-12">
                    
                    <div class="md:col-span-5 relative bg-slate-200 min-h-[190px]">
                        <img src="https://placehold.co/600x450/137333/ffffff?text=SAPU+Dr.+Juan+Lozic" 
                             alt="SAPU Dr. Juan Lozic Pérez" 
                             class="w-full h-full object-cover min-h-[190px]">
                        <div class="absolute top-3 left-3 bg-[#137333] text-white text-[10px] px-2.5 py-0.5 rounded-full font-bold shadow">
                            APS · Servicio de Urgencia Primaria
                        </div>
                    </div>

                    <div class="md:col-span-7 p-5 flex flex-col justify-between space-y-4">
                        <div>
                            <h3 class="text-lg md:text-xl font-extrabold header-blue">
                                SAPU Dr. Juan Lozic Pérez
                            </h3>
                            <p class="text-xs text-slate-400 font-medium mt-0.5">Servicio de Atención Primaria de Urgencia</p>
                        </div>

                        <!-- Número de pacientes en espera -->
                        <div class="grid grid-cols-2 gap-2 py-2 border-y border-slate-100">
                            <div>
                                <span class="text-xs font-semibold text-slate-400 block">Pacientes en espera</span>
                                <div class="flex items-baseline space-x-2">
                                    <span id="sapu-count" class="text-4xl font-extrabold header-blue leading-none mt-1 block">0</span>
                                    <span id="sapu-status-badge" class="text-[10px] px-2 py-0.5 rounded-md font-bold bg-emerald-100 text-emerald-800">Normal</span>
                                </div>
                            </div>
                            <div class="border-l border-slate-100 pl-4 flex flex-col justify-center">
                                <span class="text-xs font-semibold text-slate-400 block">Último reporte</span>
                                <div class="flex items-center space-x-1 mt-1 text-slate-700 font-bold text-xs md:text-sm">
                                    <i data-lucide="clock" class="w-4 h-4 text-slate-400"></i>
                                    <span id="sapu-report">Hace instantes</span>
                                </div>
                            </div>
                        </div>

                        <div class="bg-slate-50 rounded-xl p-3 space-y-1.5 text-xs text-slate-600">
                            <div class="flex items-start space-x-2">
                                <i data-lucide="map-pin" class="w-3.5 h-3.5 text-slate-400 mt-0.5 flex-shrink-0"></i>
                                <span><strong>Dirección:</strong> Calle Javiera Carrera s/n, Puerto Natales</span>
                            </div>
                            <div class="flex items-start space-x-2">
                                <i data-lucide="clock" class="w-3.5 h-3.5 text-slate-400 mt-0.5 flex-shrink-0"></i>
                                <span><strong>Horario de atención:</strong> Lun-Vie: 17:00 a 23:59 hrs · Sáb-Dom-Festivos: 08:00 a 23:59 hrs</span>
                            </div>
                        </div>

                        <div class="pt-1 flex items-center justify-between text-xs font-bold">
                            <span class="text-slate-400 font-normal">Urgencia Primaria APS</span>

                            <a href="https://maps.google.com/?q=Javiera+Carrera,+Puerto+Natales" 
                               target="_blank" 
                               rel="noopener noreferrer"
                               class="inline-flex items-center text-slate-600 hover:text-[#0d3b66] transition">
                                <i data-lucide="map-pin" class="w-3.5 h-3.5 mr-1 text-[#0d3b66]"></i>
                                <span>Ver ubicación</span>
                                <i data-lucide="chevron-right" class="w-3.5 h-3.5 ml-0.5"></i>
                            </a>
                        </div>
                    </div>
                </div>
            </div>

        </main>
    </div>

    <!-- MODAL 1: Login de Administrador -->
    <div id="modal-auth" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-sm w-full p-6 space-y-4 shadow-xl border border-slate-200">
            <div class="text-center space-y-1">
                <div class="w-12 h-12 bg-slate-100 rounded-full flex items-center justify-center mx-auto text-[#0d3b66]">
                    <i data-lucide="lock" class="w-6 h-6"></i>
                </div>
                <h3 class="font-extrabold text-lg header-blue">Acceso de Personal</h3>
                <p class="text-xs text-slate-500">Ingresa tu clave de acceso de turno para actualizar los conteos.</p>
            </div>

            <form onsubmit="handleLogin(event)" class="space-y-3">
                <div>
                    <label class="block text-xs font-bold text-slate-600 mb-1">PIN / Contraseña</label>
                    <input type="password" id="input-pin" placeholder="Clave (Por defecto: 1234)" class="w-full px-3 py-2 border border-slate-300 rounded-xl text-sm focus:ring-2 focus:ring-[#0d3b66] focus:outline-none">
                </div>
                <p id="login-error" class="text-xs text-red-600 font-semibold hidden text-center">Clave incorrecta. Intenta nuevamente.</p>
                <div class="flex space-x-2 pt-2">
                    <button type="button" onclick="toggleModal('modal-auth')" class="w-1/2 py-2 bg-slate-100 text-slate-600 font-bold text-xs rounded-xl hover:bg-slate-200">
                        Cancelar
                    </button>
                    <button type="submit" class="w-1/2 py-2 bg-[#0d3b66] text-white font-bold text-xs rounded-xl hover:bg-blue-900">
                        Ingresar
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- MODAL 2: Panel de Administración (Edición de Pacientes) -->
    <div id="modal-admin" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-lg w-full p-6 space-y-5 shadow-2xl border border-slate-200 max-h-[90vh] overflow-y-auto">
            
            <div class="flex items-center justify-between border-b border-slate-100 pb-3">
                <div class="flex items-center space-x-2">
                    <span class="w-3 h-3 bg-emerald-500 rounded-full animate-ping"></span>
                    <h3 class="font-extrabold text-lg header-blue">Panel de Edición en Vivo</h3>
                </div>
                <button onclick="toggleModal('modal-admin')" class="text-slate-400 hover:text-slate-600">
                    <i data-lucide="x" class="w-5 h-5"></i>
                </button>
            </div>

            <!-- Edición UEH Hospital -->
            <div class="bg-slate-50 p-4 rounded-xl space-y-3 border border-slate-200">
                <h4 class="font-bold text-xs uppercase tracking-wider text-slate-500">1. UEH Hospital Natales</h4>
                
                <div class="flex items-center justify-between bg-white p-3 rounded-lg border border-slate-200">
                    <span class="text-xs font-bold text-slate-700">Pacientes en espera:</span>
                    <div class="flex items-center space-x-3">
                        <button onclick="changeCount('ueh', -1)" class="w-9 h-9 rounded-lg bg-slate-100 hover:bg-slate-200 text-slate-800 font-extrabold text-lg flex items-center justify-center border border-slate-300">-</button>
                        <span id="admin-ueh-count" class="text-2xl font-black header-blue min-w-[30px] text-center">0</span>
                        <button onclick="changeCount('ueh', 1)" class="w-9 h-9 rounded-lg bg-slate-100 hover:bg-slate-200 text-slate-800 font-extrabold text-lg flex items-center justify-center border border-slate-300">+</button>
                    </div>
                </div>

                <div class="grid grid-cols-2 gap-2 text-xs">
                    <div>
                        <label class="block font-semibold text-slate-500 mb-1">Estado de Demanda</label>
                        <select id="admin-ueh-status" onchange="updateStatus('ueh')" class="w-full p-2 border border-slate-300 rounded-lg text-xs font-semibold">
                            <option value="Normal">Normal</option>
                            <option value="Media">Demanda Media</option>
                            <option value="Alta">Alta Demanda / Sat.</option>
                        </select>
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-500 mb-1">Último Reporte</label>
                        <input type="text" id="admin-ueh-time" placeholder="Ej: Hace instantes" class="w-full p-2 border border-slate-300 rounded-lg text-xs">
                    </div>
                </div>
            </div>

            <!-- Edición SAPU Lozic -->
            <div class="bg-slate-50 p-4 rounded-xl space-y-3 border border-slate-200">
                <h4 class="font-bold text-xs uppercase tracking-wider text-slate-500">2. SAPU Dr. Juan Lozic</h4>
                
                <div class="flex items-center justify-between bg-white p-3 rounded-lg border border-slate-200">
                    <span class="text-xs font-bold text-slate-700">Pacientes en espera:</span>
                    <div class="flex items-center space-x-3">
                        <button onclick="changeCount('sapu', -1)" class="w-9 h-9 rounded-lg bg-slate-100 hover:bg-slate-200 text-slate-800 font-extrabold text-lg flex items-center justify-center border border-slate-300">-</button>
                        <span id="admin-sapu-count" class="text-2xl font-black header-blue min-w-[30px] text-center">0</span>
                        <button onclick="changeCount('sapu', 1)" class="w-9 h-9 rounded-lg bg-slate-100 hover:bg-slate-200 text-slate-800 font-extrabold text-lg flex items-center justify-center border border-slate-300">+</button>
                    </div>
                </div>

                <div class="grid grid-cols-2 gap-2 text-xs">
                    <div>
                        <label class="block font-semibold text-slate-500 mb-1">Estado de Demanda</label>
                        <select id="admin-sapu-status" onchange="updateStatus('sapu')" class="w-full p-2 border border-slate-300 rounded-lg text-xs font-semibold">
                            <option value="Normal">Normal</option>
                            <option value="Media">Demanda Media</option>
                            <option value="Alta">Alta Demanda / Sat.</option>
                        </select>
                    </div>
                    <div>
                        <label class="block font-semibold text-slate-500 mb-1">Último Reporte</label>
                        <input type="text" id="admin-sapu-time" placeholder="Ej: Hace 10 min" class="w-full p-2 border border-slate-300 rounded-lg text-xs">
                    </div>
                </div>
            </div>

            <!-- Cambiar Clave Admin -->
            <div class="border-t border-slate-100 pt-3">
                <details class="text-xs text-slate-500">
                    <summary class="cursor-pointer font-bold hover:text-slate-700">Configuración de Seguridad (Cambiar PIN)</summary>
                    <div class="mt-2 flex space-x-2">
                        <input type="password" id="new-pin-input" placeholder="Nuevo PIN" class="p-2 border border-slate-300 rounded-lg text-xs w-full">
                        <button onclick="changePIN()" class="bg-slate-700 text-white px-3 py-1.5 rounded-lg font-bold">Guardar</button>
                    </div>
                </details>
            </div>

            <div class="flex space-x-2 pt-2">
                <button onclick="logoutAdmin()" class="w-1/3 py-2.5 bg-red-100 hover:bg-red-200 text-red-800 font-bold text-xs rounded-xl">
                    Cerrar Sesión
                </button>
                <button onclick="saveAndApplyAdminData()" class="w-2/3 py-2.5 bg-[#0d3b66] hover:bg-blue-900 text-white font-bold text-xs rounded-xl shadow-md">
                    Guardar y Publicar
                </button>
            </div>

        </div>
    </div>

    <!-- MODAL 3: Información ESI -->
    <div id="modal-info" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-lg w-full p-6 space-y-4 shadow-xl border border-slate-200">
            <div class="flex items-start justify-between">
                <div>
                    <h3 class="font-extrabold text-lg header-blue">Categorización ESI</h3>
                    <p class="text-xs text-slate-500">La atención es por gravedad médica, no por llegada.</p>
                </div>
                <button onclick="toggleModal('modal-info')" class="text-slate-400 hover:text-slate-600 p-1">
                    <i data-lucide="x" class="w-5 h-5"></i>
                </button>
            </div>

            <div class="space-y-2 text-xs">
                <div class="p-2.5 rounded-lg bg-red-100 text-red-900 border-l-4 border-red-600 font-medium">
                    <strong>C1 (Emergencia):</strong> Atención inmediata por riesgo vital.
                </div>
                <div class="p-2.5 rounded-lg bg-orange-100 text-orange-900 border-l-4 border-orange-500 font-medium">
                    <strong>C2 (Alta Urgencia):</strong> Atención rápida, posible riesgo vital.
                </div>
                <div class="p-2.5 rounded-lg bg-yellow-100 text-yellow-900 border-l-4 border-yellow-500 font-medium">
                    <strong>C3 (Mediana Urgencia):</strong> Requiere evaluación médica completa.
                </div>
                <div class="p-2.5 rounded-lg bg-green-100 text-green-900 border-l-4 border-green-600 font-medium">
                    <strong>C4 (Baja Urgencia):</strong> Atención diferida o derivación a SAPU.
                </div>
                <div class="p-2.5 rounded-lg bg-blue-100 text-blue-900 border-l-4 border-blue-600 font-medium">
                    <strong>C5 (No Urgente):</strong> Atención ambulatoria general.
                </div>
            </div>

            <button onclick="toggleModal('modal-info')" class="w-full py-2.5 bg-[#0d3b66] hover:bg-blue-900 text-white font-bold text-xs rounded-xl">
                Entendido
            </button>
        </div>
    </div>

    <!-- Pie de página -->
    <footer class="bg-white border-t border-slate-200 mt-10 py-6 text-xs text-slate-500">
        <div class="max-w-3xl mx-auto px-4 space-y-4">
            <div class="flex flex-wrap justify-center items-center gap-6 font-bold text-slate-700">
                <a href="tel:131" class="flex items-center space-x-1.5 hover:text-red-600">
                    <i data-lucide="phone" class="w-4 h-4 text-red-600"></i>
                    <span>131 SAMU</span>
                </a>
                <a href="tel:132" class="flex items-center space-x-1.5 hover:text-red-600">
                    <i data-lucide="flame" class="w-4 h-4 text-red-600"></i>
                    <span>132 Bomberos</span>
                </a>
                <a href="tel:133" class="flex items-center space-x-1.5 hover:text-blue-700">
                    <i data-lucide="shield" class="w-4 h-4 text-blue-700"></i>
                    <span>133 Carabineros</span>
                </a>
                <a href="tel:6003607777" class="flex items-center space-x-1.5 hover:text-emerald-700">
                    <i data-lucide="headphones" class="w-4 h-4 text-emerald-700"></i>
                    <span>600 360 7777 Salud Responde</span>
                </a>
            </div>
            <div class="text-center text-[11px] text-slate-400 border-t border-slate-100 pt-3">
                <p>Servicio de Salud Magallanes · Puerto Natales, Chile</p>
            </div>
        </div>
    </footer>

    <!-- LÓGICA JAVASCRIPT CON PERSISTENCIA EN LOCALSTORAGE -->
    <script>
        // Clave por defecto
        const DEFAULT_PIN = "1234";

        // Estructura de estado inicial por defecto
        const defaultData = {
            ueh: { count: 4, status: 'Normal', reportTime: 'Hace instantes' },
            sapu: { count: 1, status: 'Normal', reportTime: 'Hace instantes' },
            lastUpdate: ''
        };

        let appData = { ...defaultData };
        let isAdminLoggedIn = false;

        // Cargar datos al iniciar
        window.onload = function() {
            lucide.createIcons();
            initData();
            loadPublicData();
        };

        function initData() {
            const saved = localStorage.getItem('natales_urgencias_data');
            if (saved) {
                try {
                    appData = JSON.parse(saved);
                } catch(e) {
                    appData = { ...defaultData };
                }
            } else {
                appData.lastUpdate = formatChileDate();
                saveDataToStorage();
            }
        }

        function saveDataToStorage() {
            localStorage.setItem('natales_urgencias_data', JSON.stringify(appData));
        }

        function formatChileDate() {
            const now = new Date();
            const d = String(now.getDate()).padStart(2, '0');
            const m = String(now.getMonth() + 1).padStart(2, '0');
            const y = now.getFullYear();
            const hh = String(now.getHours()).padStart(2, '0');
            const mm = String(now.getMinutes()).padStart(2, '0');
            return `${d}/${m}/${y} ${hh}:${mm}`;
        }

        function loadPublicData(animate = false) {
            initData();

            if (animate) {
                const icon = document.getElementById('refresh-icon');
                icon.classList.add('rotate-180');
                setTimeout(() => icon.classList.remove('rotate-180'), 500);
            }

            // Valores de conteo
            document.getElementById('ueh-count').textContent = appData.ueh.count;
            document.getElementById('sapu-count').textContent = appData.sapu.count;

            // Reportes
            document.getElementById('ueh-report').textContent = appData.ueh.reportTime || 'Hace instantes';
            document.getElementById('sapu-report').textContent = appData.sapu.reportTime || 'Hace instantes';

            // Badges de estado
            renderStatusBadge('ueh-status-badge', appData.ueh.status);
            renderStatusBadge('sapu-status-badge', appData.sapu.status);

            // Menor número reportado
            const highlightDetail = document.getElementById('highlight-detail');
            if (appData.sapu.count <= appData.ueh.count) {
                highlightDetail.textContent = `SAPU Dr. Juan Lozic Pérez · ${appData.sapu.count} pacientes en espera`;
            } else {
                highlightDetail.textContent = `UEH Hospital Natales · ${appData.ueh.count} pacientes en espera`;
            }

            // Timestamp de consulta
            document.getElementById('timestamp').textContent = appData.lastUpdate || formatChileDate();
        }

        function renderStatusBadge(elementId, status) {
            const el = document.getElementById(elementId);
            el.textContent = status || 'Normal';
            if (status === 'Alta') {
                el.className = 'text-[10px] px-2 py-0.5 rounded-md font-bold bg-red-100 text-red-800';
            } else if (status === 'Media') {
                el.className = 'text-[10px] px-2 py-0.5 rounded-md font-bold bg-amber-100 text-amber-800';
            } else {
                el.className = 'text-[10px] px-2 py-0.5 rounded-md font-bold bg-emerald-100 text-emerald-800';
            }
        }

        // --- SISTEMA DE AUTENTICACIÓN ADMIN ---

        function openAdminAuth() {
            if (isAdminLoggedIn) {
                openAdminPanel();
            } else {
                document.getElementById('input-pin').value = '';
                document.getElementById('login-error').classList.add('hidden');
                toggleModal('modal-auth');
            }
        }

        function handleLogin(e) {
            e.preventDefault();
            const pin = document.getElementById('input-pin').value;
            const currentPin = localStorage.getItem('natales_admin_pin') || DEFAULT_PIN;

            if (pin === currentPin) {
                isAdminLoggedIn = true;
                toggleModal('modal-auth');
                document.getElementById('badge-admin-logged').classList.remove('hidden');
                document.getElementById('btn-admin-access').classList.add('hidden');
                openAdminPanel();
            } else {
                document.getElementById('login-error').classList.remove('hidden');
            }
        }

        function logoutAdmin() {
            isAdminLoggedIn = false;
            document.getElementById('badge-admin-logged').classList.add('hidden');
            document.getElementById('btn-admin-access').classList.remove('hidden');
            toggleModal('modal-admin');
        }

        function openAdminPanel() {
            // Sincronizar inputs del modal admin con los datos actuales
            document.getElementById('admin-ueh-count').textContent = appData.ueh.count;
            document.getElementById('admin-sapu-count').textContent = appData.sapu.count;

            document.getElementById('admin-ueh-status').value = appData.ueh.status || 'Normal';
            document.getElementById('admin-sapu-status').value = appData.sapu.status || 'Normal';

            document.getElementById('admin-ueh-time').value = appData.ueh.reportTime || 'Hace instantes';
            document.getElementById('admin-sapu-time').value = appData.sapu.reportTime || 'Hace instantes';

            toggleModal('modal-admin');
        }

        function changeCount(center, delta) {
            if (center === 'ueh') {
                appData.ueh.count = Math.max(0, appData.ueh.count + delta);
                document.getElementById('admin-ueh-count').textContent = appData.ueh.count;
            } else {
                appData.sapu.count = Math.max(0, appData.sapu.count + delta);
                document.getElementById('admin-sapu-count').textContent = appData.sapu.count;
            }
        }

        function saveAndApplyAdminData() {
            appData.ueh.reportTime = document.getElementById('admin-ueh-time').value || 'Hace instantes';
            appData.sapu.reportTime = document.getElementById('admin-sapu-time').value || 'Hace instantes';
            
            appData.ueh.status = document.getElementById('admin-ueh-status').value;
            appData.sapu.status = document.getElementById('admin-sapu-status').value;

            appData.lastUpdate = formatChileDate();

            saveDataToStorage();
            loadPublicData();
            toggleModal('modal-admin');
        }

        function changePIN() {
            const newPin = document.getElementById('new-pin-input').value.trim();
            if (newPin.length >= 4) {
                localStorage.setItem('natales_admin_pin', newPin);
                alert("PIN actualizado con éxito.");
                document.getElementById('new-pin-input').value = '';
            } else {
                alert("El PIN debe tener al menos 4 dígitos.");
            }
        }

        function toggleModal(modalId) {
            const modal = document.getElementById(modalId);
            modal.classList.toggle('hidden');
        }
    </script>
</body>
</html>
