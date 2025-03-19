<!DOCTYPE html>
<html lang="ca">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fusionador d'App Inventor</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.7.1/jszip.min.js"></script>
    <style>
        body {
            background: #f0f8ff;
            font-family: Arial, sans-serif;
        }
        .header {
            background: #4a90e2;
            color: white;
            text-align: center;
            padding: 2rem 0;
        }
        .project-card {
            background: white;
            border-radius: 10px;
            padding: 1rem;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            margin-bottom: 1rem;
        }
        .merge-btn {
            background: #28a745;
            color: white;
            padding: 1rem 2rem;
            border-radius: 50px;
            font-size: 1.2rem;
            transition: 0.3s ease;
            border: none;
        }
        .merge-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 4px 15px rgba(40, 167, 69, 0.4);
        }
        .debug-console {
            background: #222;
            color: #0f0;
            font-family: monospace;
            padding: 1rem;
            max-height: 300px;
            overflow-y: auto;
            border-radius: 8px;
            margin-top: 2rem;
        }
    </style>
</head>
<body>
    <header class="header">
        <h1><i class="fas fa-code-merge"></i> Fusionador d'App Inventor</h1>
        <p>Combina els teus projectes .aia de manera segura</p>
    </header>

    <main class="container">
        <div id="projects-container"></div>
        <button class="btn btn-secondary mt-3" onclick="addProject()">
            <i class="fas fa-plus"></i> Afegeix un Projecte
        </button>
        <div class="text-center mt-4">
            <button class="btn merge-btn" onclick="mergeProjects()" id="merge-btn">
                <i class="fas fa-magic"></i> Fusiona Projectes
            </button>
        </div>
        <div class="debug-console" id="debug-console"></div>
    </main>

    <script>
        let projects = [];

        function logDebug(message) {
            const debugConsole = document.getElementById('debug-console');
            debugConsole.innerHTML += `<p>> ${message}</p>`;
            debugConsole.scrollTop = debugConsole.scrollHeight;
        }

        function addProject() {
            const container = document.getElementById('projects-container');
            const projectId = `project-${projects.length}`;
            
            const projectHtml = `
                <div class="project-card" id="${projectId}">
                    <h4>Projecte ${projects.length + 1}</h4>
                    <label class="file-input-label d-block text-center mb-3">
                        <i class="fas fa-file-upload"></i> Puja un fitxer .aia
                        <input type="file" class="d-none" accept=".aia" onchange="loadProject(event, '${projectId}')">
                    </label>
                    <div class="project-content" style="display: none;">
                        <h5>Pantalles</h5>
                        <div class="screens-list"></div>
                        <h5>Recursos</h5>
                        <div class="assets-list"></div>
                    </div>
                </div>
            `;
            
            container.insertAdjacentHTML('beforeend', projectHtml);
            projects.push({ id: projectId, screens: [], assets: [], zip: null });
            logDebug(`Afegit projecte ${projects.length}`);
        }

        async function loadProject(event, projectId) {
            const file = event.target.files[0];
            if (!file) return;
            
            try {
                const project = projects.find(p => p.id === projectId);
                project.zip = await JSZip.loadAsync(file);
                project.screens = [];
                project.assets = [];

                project.zip.forEach((relativePath, file) => {
                    if (relativePath.endsWith('.scm')) {
                        let screenName = relativePath.split('/').pop().replace('.scm', '');
                        if (!project.screens.includes(screenName)) {
                            project.screens.push(screenName);
                        }
                    } else if (relativePath.startsWith('assets/')) {
                        let assetName = relativePath.split('/').pop();
                        if (!project.assets.includes(assetName)) {
                            project.assets.push(assetName);
                        }
                    }
                });

                document.getElementById(projectId).querySelector('.project-content').style.display = 'block';
                logDebug(`Projecte carregat: ${file.name}`);
            } catch (error) {
                alert(`Error carregant el projecte: ${error.message}`);
                logDebug(`Error: ${error.message}`);
            }
        }

        async function mergeProjects() {
            if (projects.length < 2) {
                alert("Necessites afegir almenys dos projectes per fusionar.");
                return;
            }

            const mergeBtn = document.getElementById('merge-btn');
            mergeBtn.innerText = "Fusionant...";
            mergeBtn.disabled = true;
            logDebug("Iniciant fusió de projectes...");

            try {
                const mergedZip = new JSZip();
                mergedZip.file("youngandroidproject/project.properties", "name=ProjecteFusionat");

                for (const project of projects) {
                    if (!project.zip) continue;
                    for (const screen of project.screens) {
                        await addFileToZip(project.zip, mergedZip, `src/${screen}.scm`);
                        await addFileToZip(project.zip, mergedZip, `src/${screen}.bky`);
                    }
                    for (const asset of project.assets) {
                        await addFileToZip(project.zip, mergedZip, `assets/${asset}`);
                    }
                }

                const content = await mergedZip.generateAsync({ type: 'blob' });
                const link = document.createElement('a');
                link.href = URL.createObjectURL(content);
                link.download = `projecte-fusionat-${Date.now()}.aia`;
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);

                logDebug("Projecte fusionat correctament!");
            } catch (error) {
                alert(`Error durant la fusió: ${error.message}`);
                logDebug(`Error: ${error.message}`);
            } finally {
                mergeBtn.innerText = "Fusiona Projectes";
                mergeBtn.disabled = false;
            }
        }

        async function addFileToZip(sourceZip, targetZip, path) {
            const file = sourceZip.file(path);
            if (file) {
                const content = await file.async('uint8array');
                targetZip.file(path, content);
            } else {
                logDebug(`No trobat: ${path}`);
            }
        }

        addProject();
    </script>
</body>
</html>
