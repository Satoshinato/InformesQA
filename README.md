<!DOCTYPE html>
<html lang="es">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Infografía: Informe de Avance de Pruebas QA - Ticketera 2.0.4</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #ECF0F1;
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

        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
    </style>
</head>

<body class="text-gray-800">
    <div class="container mx-auto p-4 md:p-8">
        <header class="text-center mb-12 bg-white rounded-lg shadow-lg p-6">
            <h1 class="text-4xl md:text-5xl font-extrabold text-blue-700 mb-4">Análisis de Calidad: Ticketera 2.0.4</h1>
            <p class="text-xl md:text-2xl text-gray-600">Informe de Avance de Pruebas QA</p>
            <p class="text-md text-gray-500 mt-2">Fecha: 15 de Julio de 2025 | Generado por: Leandro Diaz</p>
        </header>

        <section id="resumen-ejecutivo" class="bg-white rounded-lg shadow-lg p-6 mb-12">
            <h2 class="text-3xl font-bold text-blue-600 mb-6">1. Resumen Ejecutivo</h2>
            <p class="text-lg leading-relaxed mb-4">
                Este informe presenta el avance de las pruebas QA para la **Ticketera 2.0.4**. El objetivo fue verificar
                correcciones de defectos, detectar regresiones y proponer mejoras de UX. Se ejecutaron **21 casos de
                prueba (CP001-CP021)** y se registraron **4 sugerencias (SUG001-SUG004)**, con foco en los módulos de
                Configuración (Empresas, Áreas, Proyectos, Grupos), Flujos, Formularios, Creación de Tickets,
                Notificaciones y Exportación.
            </p>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-center">
                <div>
                    <h3 class="text-2xl font-semibold text-blue-500 mb-4">Resultados Clave</h3>
                    <ul class="list-disc list-inside text-lg space-y-2">
                        <li><strong class="text-green-600">Defectos Corregidos:</strong> Creación y edición de Empresas
                            y Áreas ahora OK. Indicador de conectividad OK.</li>
                        <li><strong class="text-yellow-600">En Desarrollo:</strong> Eliminación en varios módulos y
                            módulo de Usuarios en desarrollo.</li>
                        <li><strong class="text-red-600">Defectos Persistentes/Nuevos:</strong> 11 defectos
                            críticos/importantes impactan usabilidad y funcionalidad.</li>
                        <li><strong class="text-blue-400">Sugerencias de Mejora:</strong> 4 propuestas para optimizar
                            estética y claridad.</li>
                    </ul>
                </div>
                <div class="chart-container">
                    <canvas id="resumenEstadoChart"></canvas>
                </div>
            </div>
            <p class="text-lg leading-relaxed mt-6">
                La versión Ticketera 2.0.4 muestra avances significativos. Sin embargo, persiste una cantidad
                considerable de defectos funcionales y de usabilidad. Se recomienda priorizar la resolución de los
                defectos "Fallido" para mejorar la calidad y experiencia del usuario.
            </p>
        </section>

        <section id="defectos-identificados" class="bg-white rounded-lg shadow-lg p-6 mb-12">
            <h2 class="text-3xl font-bold text-red-600 mb-6">2. Defectos Identificados y Persistentes</h2>
            <p class="text-lg leading-relaxed mb-4">
                Esta sección detalla los casos de prueba que resultaron en un estado "Fallido", indicando áreas que
                requieren atención inmediata para garantizar la estabilidad y funcionalidad de la aplicación.
            </p>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-center">
                <div class="chart-container">
                    <canvas id="fallidosPorModuloChart"></canvas>
                </div>
                <div>
                    <h3 class="text-2xl font-semibold text-red-500 mb-4">Defectos Críticos Destacados</h3>
                    <ul class="list-disc list-inside text-lg space-y-2">
                        <li><strong class="text-red-600">CP001 (Formularios):</strong> Los formularios y campos no
                            pueden eliminarse, ni modificarse.</li>
                        <li><strong class="text-red-600">CP011 (Flujos):</strong> Edición abre ventana incorrecta y no
                            carga datos.</li>
                        <li><strong class="text-red-600">CP014 (Formularios):</strong> Error al guardar modificaciones.
                        </li>
                        <li><strong class="text-red-600">CP018 (Exportación):</strong> Botones de exportación PDF/Excel
                            no funcionan.</li>
                        <li><strong class="text-red-600">CP020 (Formularios):</strong> Persistencia de datos (usuarios a
                            notificar/checkboxes) fallida.</li>
                    </ul>
                </div>
            </div>
        </section>

        <section id="mejoras-y-pendientes" class="bg-white rounded-lg shadow-lg p-6 mb-12">
            <h2 class="text-3xl font-bold text-green-600 mb-6">3. Funcionalidades OK y Pendientes</h2>
            <p class="text-lg leading-relaxed mb-4">
                A pesar de los defectos, la versión 2.0.4 ha logrado avances importantes en la estabilidad de
                operaciones básicas y algunas funcionalidades se comportan según lo diseñado o están en desarrollo.
            </p>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-center">
                <div>
                    <h3 class="text-2xl font-semibold text-green-500 mb-4">Funcionalidades OK</h3>
                    <ul class="list-disc list-inside text-lg space-y-2">
                        <li><strong class="text-green-600">CP002 (Empresas):</strong> Edición de empresas operativa.
                        </li>
                        <li><strong class="text-green-600">CP004 (Áreas):</strong> Edición de áreas operativa.</li>
                        <li><strong class="text-green-600">CP008 (Áreas):</strong> Creación de área en otra empresa (por
                            diseño).</li>
                        <li><strong class="text-green-600">CP015 (Nuevo Ticket):</strong> Creación de tickets con
                            combinaciones Tipo/Subárea.</li>
                        <li><strong class="text-green-600">CP021 (General):</strong> Indicador de Conectividad (barrita
                            blanca) funciona correctamente.</li>
                    </ul>
                </div>
                <div class="chart-container">
                    <canvas id="okVsNaChart"></canvas>
                </div>
            </div>
            <div class="mt-8">
                <h3 class="text-2xl font-semibold text-yellow-600 mb-4">En Desarrollo</h3>
                <ul class="list-disc list-inside text-lg space-y-2">
                    <li><strong class="text-gray-700">Eliminación de Elementos:</strong> Áreas (CP005), Proyectos
                        (CP006), Grupos (CP007), Flujos (CP012), Formularios (CP014) - Funcionalidad no implementada,
                        planeada para futuras versiones.</li>
                    <li><strong class="text-gray-700">Módulo de Usuarios (CP009):</strong> Aún en desarrollo, impide
                        pruebas completas de gestión.</li>
                </ul>
            </div>
        </section>

        <section id="sugerencias-ux" class="bg-white rounded-lg shadow-lg p-6 mb-12">
            <h2 class="text-3xl font-bold text-blue-500 mb-6">4. Sugerencias de Mejora (UX/UI)</h2>
            <p class="text-lg leading-relaxed mb-4">
                Se han identificado oportunidades para optimizar la experiencia del usuario y la estética general de la
                interfaz.
            </p>
            <ul class="list-disc list-inside text-lg space-y-2">
                <li><strong class="text-blue-600">SUG001 (Nuevo Ticket):</strong> Reducir el espacio vertical excesivo
                    debajo del "Título del Ticket" para mejorar la estética.</li>
                <li><strong class="text-blue-600">SUG002 (Edición de Formulario):</strong> Corregir el título de la
                    ventana de edición de formulario a "Editar Formulario" en lugar de "Nuevo Formulario".</li>
                <li><strong class="text-blue-600">SUG003 (Funcionalidad de Eliminación):</strong> Proporcionar
                    retroalimentación al usuario (ej. botón deshabilitado con tooltip) para funcionalidades de
                    eliminación que no están disponibles.</li>
                <li><strong class="text-blue-600">SUG004 (Información de Versión):</strong> Actualizar la versión de la
                    aplicación en el margen inferior izquierdo .</li>
            </ul>
        </section>

        <footer class="text-center text-gray-500 text-sm mt-12">
            <p>Infografía generada automáticamente. Para detalles completos, consulte el informe de QA adjunto.</p>
        </footer>
    </div>

    <script>
        function wrapLabel(label) {
            if (typeof label !== 'string') return label;
            if (label.length <= 16) return label;

            const words = label.split(' ');
            let lines = [];
            let currentLine = '';

            for (let i = 0; i < words.length; i++) {
                const word = words[i];
                if ((currentLine + word).length <= 16 || currentLine === '') {
                    currentLine += (currentLine === '' ? '' : ' ') + word;
                } else {
                    lines.push(currentLine);
                    currentLine = word;
                }
            }
            if (currentLine !== '') {
                lines.push(currentLine);
            }
            return lines;
        }

        const tooltipConfig = {
            plugins: {
                tooltip: {
                    callbacks: {
                        title: function (tooltipItems) {
                            const item = tooltipItems[0];
                            let label = item.chart.data.labels[item.dataIndex];
                            if (Array.isArray(label)) {
                                return label.join(' ');
                            } else {
                                return label;
                            }
                        }
                    }
                }
            }
        };

        const resumenEstadoCtx = document.getElementById('resumenEstadoChart').getContext('2d');
        new Chart(resumenEstadoCtx, {
            type: 'doughnut',
            data: {
                labels: ['OK', 'Fallido', 'En Desarrollo', 'Sugerencias'],
                datasets: [{
                    data: [6, 10, 5, 4],
                    backgroundColor: ['#2ECC71', '#E74C3C', '#F39C12', '#3498DB'],
                    hoverOffset: 4
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                ...tooltipConfig,
                plugins: {
                    legend: {
                        position: 'top',
                    },
                    title: {
                        display: true,
                        text: 'Resumen de Casos de Prueba por Estado',
                        font: {
                            size: 16
                        }
                    },
                    ...tooltipConfig.plugins
                }
            }
        });

        const fallidosPorModuloCtx = document.getElementById('fallidosPorModuloChart').getContext('2d');
        new Chart(fallidosPorModuloCtx, {
            type: 'bar',
            data: {
                labels: [
                    wrapLabel('Empresas (Acentuación)'),
                    wrapLabel('Flujos (Desactivar)'),
                    wrapLabel('Flujos (Editar)'),
                    wrapLabel('Proyectos (Cliente no visible)'),
                    wrapLabel('Flujos (Eliminar)'),
                    wrapLabel('Formularios (Editar)'),
                    wrapLabel('Formularios (Eliminar)'),
                    wrapLabel('Actualización UI'),
                    wrapLabel('Exportación Datos'),
                    wrapLabel('Email Criticidad'),
                    wrapLabel('Formularios (Persistencia)')
                ],
                datasets: [{
                    label: 'Casos Fallidos',
                    data: [1, 4, 2, 2, 2, 4, 4, 5, 1, 1, 4],
                    backgroundColor: '#E74C3C',
                    borderColor: '#C0392B',
                    borderWidth: 6
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                ...tooltipConfig,
                scales: {
                    y: {
                        beginAtZero: true,
                        title: {
                            display: true,
                            text: 'Cantidad de Fallos'
                        }
                    },
                    x: {
                        title: {
                            display: true,
                            text: 'Módulo / Funcionalidad'
                        }
                    }
                },
                plugins: {
                    legend: {
                        display: false
                    },
                    title: {
                        display: true,
                        text: 'Casos Fallidos por Módulo/Funcionalidad',
                        font: {
                            size: 16
                        }
                    },
                    ...tooltipConfig.plugins
                }
            }
        });

        const okVsNaCtx = document.getElementById('okVsNaChart').getContext('2d');
        new Chart(okVsNaCtx, {
            type: 'bar',
            data: {
                labels: [
                    wrapLabel('Empresas (Crear)'),
                    wrapLabel('Empresas (Editar)'),
                    wrapLabel('Áreas (Crear)'),
                    wrapLabel('Áreas (Editar)'),
                    wrapLabel('Áreas (Crear en otra empresa)'),
                    wrapLabel('Nuevo Ticket (Combinaciones)'),
                    wrapLabel('Indicador Conectividad')
                ],
                datasets: [{
                    label: 'Casos OK',
                    data: [1, 1, 1, 1, 1, 1, 1],
                    backgroundColor: '#2ECC71',
                    borderColor: '#27AE60',
                    borderWidth: 1
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                ...tooltipConfig,
                scales: {
                    y: {
                        beginAtZero: true,
                        title: {
                            display: true,
                            text: 'Cantidad de Casos OK'
                        }
                    },
                    x: {
                        title: {
                            display: true,
                            text: 'Módulo / Funcionalidad'
                        }
                    }
                },
                plugins: {
                    legend: {
                        display: false
                    },
                    title: {
                        display: true,
                        text: 'Funcionalidades OK',
                        font: {
                            size: 16
                        }
                    },
                    ...tooltipConfig.plugins
                }
            }
        });
    </script>
</body>

</html>
