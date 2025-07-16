<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Informe de Avance de Pruebas QA (En Vivo) - Ticketera</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f4f7f9;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 400px;
        }
        @media (min-width: 768px) { .chart-container { height: 350px; } }
        .loader {
            border: 8px solid #f3f3f3;
            border-radius: 50%;
            border-top: 8px solid #3498db;
            width: 60px;
            height: 60px;
            animation: spin 2s linear infinite;
        }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
    </style>
</head>
<body class="text-gray-800">

    <div id="loading-screen" class="fixed inset-0 bg-white bg-opacity-90 flex flex-col justify-center items-center z-50">
        <div class="loader"></div>
        <p class="mt-4 text-lg text-gray-600">Cargando datos del informe...</p>
    </div>

    <div id="report-content" class="container mx-auto p-4 md:p-8 opacity-0 transition-opacity duration-500">
        <header class="text-center mb-12 bg-white rounded-lg shadow-lg p-6">
            <h1 class="text-4xl md:text-5xl font-extrabold text-blue-700 mb-4">Análisis de Calidad: <span id="report-version"></span></h1>
            <p class="text-xl md:text-2xl text-gray-600">Informe de Avance de Pruebas QA (En Vivo)</p>
            <p class="text-md text-gray-500 mt-2">Última actualización: <span id="report-date"></span> | Generado por: <span id="report-author"></span></p>
        </header>

        <section id="resumen-ejecutivo" class="bg-white rounded-lg shadow-lg p-6 mb-12">
            <h2 class="text-3xl font-bold text-blue-600 mb-6">1. Resumen Ejecutivo</h2>
            <p id="resumen-texto" class="text-lg leading-relaxed mb-4"></p>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-center">
                <div>
                    <h3 class="text-2xl font-semibold text-blue-500 mb-4">Resultados Clave</h3>
                    <ul class="list-disc list-inside text-lg space-y-2">
                        <li><strong class="text-green-600">OK:</strong> <span id="summary-ok">0</span> casos</li>
                        <li><strong class="text-red-600">Fallido:</strong> <span id="summary-failed">0</span> casos</li>
                        <li><strong class="text-yellow-600">En Desarrollo:</strong> <span id="summary-dev">0</span> casos</li>
                        <li><strong class="text-blue-400">Sugerencias:</strong> <span id="summary-sug">0</span> propuestas</li>
                    </ul>
                </div>
                <div class="chart-container">
                    <canvas id="resumenEstadoChart"></canvas>
                </div>
            </div>
            <p id="resumen-conclusion" class="text-lg leading-relaxed mt-6"></p>
        </section>

        <section id="defectos-identificados" class="bg-white rounded-lg shadow-lg p-6 mb-12">
            <h2 class="text-3xl font-bold text-red-600 mb-6">2. Defectos Identificados y Persistentes</h2>
            <p id="defectos-intro" class="text-lg leading-relaxed mb-4"></p>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-center">
                 <div class="chart-container">
                    <canvas id="fallidosPorModuloChart"></canvas>
                </div>
                <div>
                    <h3 class="text-2xl font-semibold text-red-500 mb-4">Defectos Críticos Destacados</h3>
                    <ul id="defectos-lista" class="list-disc list-inside text-lg space-y-2">
                        <!-- Los defectos se cargarán aquí dinámicamente -->
                    </ul>
                </div>
            </div>
        </section>

        <section id="mejoras-y-pendientes" class="bg-white rounded-lg shadow-lg p-6 mb-12">
            <h2 class="text-3xl font-bold text-green-600 mb-6">3. Funcionalidades OK y Pendientes</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <div>
                    <h3 class="text-2xl font-semibold text-green-500 mb-4">Funcionalidades OK</h3>
                    <ul id="ok-lista" class="list-disc list-inside text-lg space-y-2">
                        <!-- Funcionalidades OK se cargarán aquí -->
                    </ul>
                </div>
                <div>
                    <h3 class="text-2xl font-semibold text-yellow-600 mb-4">En Desarrollo / Pendiente</h3>
                    <ul id="dev-lista" class="list-disc list-inside text-lg space-y-2">
                        <!-- Funcionalidades en desarrollo se cargarán aquí -->
                    </ul>
                </div>
            </div>
        </section>

        <section id="sugerencias-ux" class="bg-white rounded-lg shadow-lg p-6 mb-12">
            <h2 class="text-3xl font-bold text-blue-500 mb-6">4. Sugerencias de Mejora (UX/UI)</h2>
            <ul id="sugerencias-lista" class="list-disc list-inside text-lg space-y-2">
                <!-- Sugerencias se cargarán aquí -->
            </ul>
        </section>

        <footer class="text-center text-gray-500 text-sm mt-12">
            <p>Este informe se actualiza en tiempo real. ID del Documento: <span id="doc-id-display"></span></p>
        </footer>
    </div>

    <!-- Firebase SDKs -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getFirestore, doc, onSnapshot, setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
        import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";

        // =====================================================================================
        // Your web app's Firebase configuration
        // =====================================================================================
        const firebaseConfig = {
            apiKey: "AIzaSyBDCUXIq7vwsLPZthJKBg3AqOTqFXV-m_Y",
            authDomain: "informe-qa-ticketera.firebaseapp.com",
            projectId: "informe-qa-ticketera",
            storageBucket: "informe-qa-ticketera.appspot.com",
            messagingSenderId: "466777678809",
            appId: "1:466777678809:web:02ed304f610f52582fafc8"
        };
        
        // =====================================================================================
        // Define el ID del documento que quieres mostrar
        // =====================================================================================
        const DOCUMENT_ID = "ticketera-2.0.4";

        // Initialize Firebase
        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);
        const auth = getAuth(app);
        
        const loadingScreen = document.getElementById('loading-screen');
        const reportContent = document.getElementById('report-content');

        let resumenChart, fallidosChart;

        function renderList(elementId, items, colorClass) {
            const listElement = document.getElementById(elementId);
            if (!listElement) return;
            listElement.innerHTML = '';
            if (items && items.length > 0) {
                items.forEach(itemText => {
                    const li = document.createElement('li');
                    li.innerHTML = `<strong class="${colorClass}">${itemText.split('(')[0]}</strong> (${itemText.split('(').slice(1).join('(')}`;
                    listElement.appendChild(li);
                });
            } else {
                 listElement.innerHTML = '<li>No hay datos para mostrar.</li>';
            }
        }

        function updateUI(data) {
            // Header
            document.getElementById('report-version').textContent = data.version || 'N/A';
            document.getElementById('report-date').textContent = new Date(data.lastUpdated.seconds * 1000).toLocaleString('es-AR');
            document.getElementById('report-author').textContent = data.author || 'N/A';
            document.getElementById('doc-id-display').textContent = DOCUMENT_ID;

            // Resumen
            document.getElementById('resumen-texto').textContent = data.summary.executiveSummary || '';
            document.getElementById('resumen-conclusion').textContent = data.summary.conclusion || '';
            document.getElementById('summary-ok').textContent = data.summary.stats.ok;
            document.getElementById('summary-failed').textContent = data.summary.stats.failed;
            document.getElementById('summary-dev').textContent = data.summary.stats.inDev;
            document.getElementById('summary-sug').textContent = data.summary.stats.suggestions;
            
            // Listas
            renderList('defectos-lista', data.defects.critical, 'text-red-600');
            renderList('ok-lista', data.features.ok, 'text-green-600');
            renderList('dev-lista', data.features.inDev, 'text-yellow-600');
            renderList('sugerencias-lista', data.suggestions, 'text-blue-600');

            // --- Chart 1: Resumen de Estado ---
            const resumenCtx = document.getElementById('resumenEstadoChart').getContext('2d');
            const resumenData = {
                labels: ['OK', 'Fallido', 'En Desarrollo', 'Sugerencias'],
                datasets: [{
                    data: [
                        data.summary.stats.ok,
                        data.summary.stats.failed,
                        data.summary.stats.inDev,
                        data.summary.stats.suggestions
                    ],
                    backgroundColor: ['#2ECC71', '#E74C3C', '#F39C12', '#3498DB'],
                    hoverOffset: 4
                }]
            };
            if (resumenChart) {
                resumenChart.data = resumenData;
                resumenChart.update();
            } else {
                resumenChart = new Chart(resumenCtx, {
                    type: 'doughnut',
                    data: resumenData,
                    options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { position: 'top' }, title: { display: true, text: 'Resumen de Casos de Prueba', font: { size: 16 } } } }
                });
            }

            // --- Chart 2: Fallidos por Módulo ---
            const fallidosCtx = document.getElementById('fallidosPorModuloChart').getContext('2d');
            const fallidosData = {
                labels: data.defects.byModule.map(d => d.module),
                datasets: [{
                    label: 'Casos Fallidos',
                    data: data.defects.byModule.map(d => d.count),
                    backgroundColor: '#E74C3C',
                }]
            };
             if (fallidosChart) {
                fallidosChart.data = fallidosData;
                fallidosChart.update();
            } else {
                fallidosChart = new Chart(fallidosCtx, {
                    type: 'bar',
                    data: fallidosData,
                    options: { responsive: true, maintainAspectRatio: false, scales: { y: { beginAtZero: true } }, plugins: { legend: { display: false }, title: { display: true, text: 'Fallos por Módulo', font: { size: 16 } } } }
                });
            }

            // Show content
            loadingScreen.style.display = 'none';
            reportContent.classList.remove('opacity-0');
        }

        onAuthStateChanged(auth, user => {
            if (user) {
                console.log("Usuario autenticado anónimamente:", user.uid);
                const docRef = doc(db, "qa-reports", DOCUMENT_ID);
                
                onSnapshot(docRef, (docSnap) => {
                    if (docSnap.exists()) {
                        console.log("Datos recibidos:", docSnap.data());
                        updateUI(docSnap.data());
                    } else {
                        console.error("El documento del informe no existe!");
                        loadingScreen.innerHTML = `<p class="text-red-500 text-lg">Error: No se encontró el documento '${DOCUMENT_ID}'. Verifica la configuración.</p>`;
                    }
                }, (error) => {
                    console.error("Error al escuchar cambios en el documento:", error);
                    loadingScreen.innerHTML = `<p class="text-red-500 text-lg">Error de conexión con la base de datos.</p>`;
                });

            } else {
                console.log("Usuario no autenticado, iniciando sesión anónima...");
                signInAnonymously(auth).catch(error => {
                    console.error("Error en la autenticación anónima:", error);
                    loadingScreen.innerHTML = `<p class="text-red-500 text-lg">Error de autenticación. No se puede cargar el informe.</p>`;
                });
            }
        });

    </script>
</body>
</html>
