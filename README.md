# village-problem-reporter
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pune District Data Entry</title>
    <style>
        :root {
            --primary: #4f46e5; /* Indigo 600 */
            --primary-hover: #4338ca;
            --secondary: #64748b;
            --bg-body: #f8fafc;
            --bg-card: #ffffff;
            --text-main: #1e293b;
            --text-muted: #64748b;
            --border: #e2e8f0;
            --radius: 12px;
            --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; }

        body {
            background-color: var(--bg-body);
            color: var(--text-main);
            padding: 2rem 1rem;
            line-height: 1.5;
        }

        .container {
            max-width: 1100px;
            margin: 0 auto;
        }

        header {
            margin-bottom: 2.5rem;
            text-align: center;
        }

        header h1 {
            font-size: 2rem;
            font-weight: 800;
            color: var(--text-main);
            margin-bottom: 0.5rem;
        }

        header p { color: var(--text-muted); }

        /* Main Grid Layout */
        .main-grid {
            display: grid;
            grid-template-columns: 1.5fr 1fr; /* Left: Selections, Right: Inputs */
            gap: 2rem;
        }

        @media (max-width: 850px) {
            .main-grid { grid-template-columns: 1fr; }
        }

        /* Section Cards */
        .card {
            background: var(--bg-card);
            border-radius: var(--radius);
            box-shadow: var(--shadow);
            border: 1px solid var(--border);
            padding: 1.5rem;
            height: 100%;
        }

        .section-title {
            font-size: 1.1rem;
            font-weight: 600;
            margin-bottom: 1.25rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            padding-bottom: 0.75rem;
            border-bottom: 1px solid var(--border);
        }

        /* --- LEFT COLUMN: SELECTORS --- */
        .scroll-area {
            max-height: 600px;
            overflow-y: auto;
            padding-right: 0.5rem;
        }

        /* Custom Checkbox */
        .chk-group { margin-bottom: 1rem; }
        .chk-header {
            font-weight: 600;
            color: var(--primary);
            margin-bottom: 0.5rem;
            font-size: 0.95rem;
        }

        .custom-checkbox {
            display: flex;
            align-items: center;
            padding: 0.5rem;
            border-radius: 6px;
            cursor: pointer;
            transition: background 0.2s;
            user-select: none;
        }
        .custom-checkbox:hover { background-color: #f1f5f9; }
        
        .custom-checkbox input {
            appearance: none;
            width: 18px;
            height: 18px;
            border: 2px solid var(--secondary);
            border-radius: 4px;
            margin-right: 10px;
            position: relative;
            cursor: pointer;
        }

        .custom-checkbox input:checked {
            background-color: var(--primary);
            border-color: var(--primary);
        }

        .custom-checkbox input:checked::after {
            content: '✓';
            color: white;
            position: absolute;
            font-size: 12px;
            top: -1px;
            left: 2px;
        }

        /* Village Section Specifics */
        #village-container {
            margin-top: 1.5rem;
            border-top: 2px dashed var(--border);
            padding-top: 1rem;
        }
        
        .village-list-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
            gap: 0.5rem;
            margin-bottom: 1.5rem;
        }
        
        .empty-msg {
            color: var(--text-muted);
            font-style: italic;
            font-size: 0.9rem;
            padding: 1rem 0;
            text-align: center;
        }

        /* --- RIGHT COLUMN: FORM INPUTS --- */
        .form-group { margin-bottom: 1.5rem; }
        
        label.input-label {
            display: block;
            font-weight: 500;
            margin-bottom: 0.5rem;
            color: var(--text-main);
        }

        /* Image Upload Styling */
        .image-upload-area {
            border: 2px dashed var(--border);
            border-radius: var(--radius);
            padding: 2rem;
            text-align: center;
            cursor: pointer;
            transition: all 0.2s;
            position: relative;
            background: #f9fafb;
        }

        .image-upload-area:hover {
            border-color: var(--primary);
            background: #eef2ff;
        }

        .image-upload-area input[type="file"] {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            opacity: 0;
            cursor: pointer;
        }

        .upload-icon {
            font-size: 2rem;
            color: var(--secondary);
            margin-bottom: 0.5rem;
        }

        .preview-container {
            margin-top: 1rem;
            display: none;
            position: relative;
        }
        
        .preview-container img {
            width: 100%;
            height: 200px;
            object-fit: cover;
            border-radius: 8px;
            border: 1px solid var(--border);
        }

        .remove-btn {
            position: absolute;
            top: 5px;
            right: 5px;
            background: rgba(0,0,0,0.6);
            color: white;
            border: none;
            border-radius: 50%;
            width: 25px;
            height: 25px;
            cursor: pointer;
        }

        /* Text Input */
        textarea.text-input {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid var(--border);
            border-radius: 6px;
            font-size: 1rem;
            resize: vertical;
            min-height: 100px;
            transition: border 0.2s;
        }
        
        textarea.text-input:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
        }

        /* Submit Button */
        .btn-submit {
            width: 100%;
            padding: 1rem;
            background-color: var(--primary);
            color: white;
            border: none;
            border-radius: 6px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: background 0.2s;
        }
        
        .btn-submit:hover { background-color: var(--primary-hover); }

        /* --- MODAL --- */
        .modal-overlay {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.5);
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: 1rem;
        }

        .modal-content {
            background: white;
            padding: 2rem;
            border-radius: var(--radius);
            width: 100%;
            max-width: 500px;
            max-height: 80vh;
            overflow-y: auto;
            animation: slideUp 0.3s ease;
        }

        .modal-title { font-size: 1.5rem; font-weight: 700; margin-bottom: 1rem; color: var(--primary); }
        .modal-data-row { margin-bottom: 1rem; border-bottom: 1px solid var(--border); padding-bottom: 0.5rem; }
        .modal-label { font-size: 0.85rem; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.5px; }
        .modal-value { font-size: 1rem; color: var(--text-main); margin-top: 0.25rem; word-break: break-word; }

        @keyframes slideUp {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

    </style>
</head>
<body>

    <header>
        <div class="container">
            <h1>Pune District Portal</h1>
            <p>Select locations and upload details</p>
        </div>
    </header>

    <form id="mainForm" class="container main-grid" onsubmit="handleSubmit(event)">
        
        <!-- Left Column: Selection -->
        <section class="card scroll-area">
            <div class="section-title">
                <span>📍</span> Location Selection
            </div>

            <!-- Taluka Selection -->
            <div class="chk-group">
                <div class="chk-header">Step 1: Select Talukas</div>
                <div id="taluka-list-container">
                    <!-- Javascript will populate this -->
                </div>
            </div>

            <!-- Village Selection -->
            <div id="village-section" style="display:none;">
                <div class="section-title" style="font-size: 1rem; border: none; margin-top: 1rem;">
                    <span>🏘️</span> Step 2: Select Villages
                </div>
                <div id="village-list-container">
                    <!-- Javascript will populate this -->
                </div>
            </div>
        </section>

        <!-- Right Column: Inputs -->
        <section class="card">
            <div class="section-title">
                <span>📝</span> Details Entry
            </div>

            <!-- Image Input -->
            <div class="form-group">
                <label class="input-label">Upload Image</label>
                <div class="image-upload-area" id="dropZone">
                    <input type="file" id="imageInput" accept="image/*" onchange="handleImageUpload(event)">
                    <div class="upload-icon">📷</div>
                    <p id="uploadText">Click or drag image here</p>
                </div>
                
                <!-- Preview -->
                <div class="preview-container" id="previewContainer">
                    <img id="imagePreview" src="" alt="Preview">
                    <button type="button" class="remove-btn" onclick="removeImage()">×</button>
                </div>
            </div>

            <!-- Text Input -->
            <div class="form-group">
                <label class="input-label" for="textInput">Description / Remarks</label>
                <textarea id="textInput" class="text-input" placeholder="Enter any specific details or notes here..."></textarea>
            </div>

            <!-- Submit -->
            <button type="submit" class="btn-submit">Submit Data</button>
        </section>

    </form>

    <!-- Result Modal -->
    <div id="resultModal" class="modal-overlay" onclick="closeModal(event)">
        <div class="modal-content">
            <h2 class="modal-title">Submission Successful!</h2>
            <div id="modalBody"></div>
            <button class="btn-submit" style="margin-top: 1.5rem;" onclick="closeModalDirectly()">Close</button>
        </div>
    </div>

    <script>
        // --- DATA STRUCTURE (Mock Pune Data) ---
        const districtData = {
            "Haveli": ["Pune City", "Shivajinagar", "Warje", "Kothrud", "Bavdhan", "Hadapsar"],
            "Junnar": ["Narayangaon", "Otur", "Junnar City", "Alephata", "Nimgaon"],
            "Purandar": ["Saswad", "Jejuri", "Shirwal", "Vadgaon"],
            "Velhe": ["Velhe", "Khanapur", "Panshet", "Raireshwar"],
            "Maval": ["Lonavala", "Kamshet", "Wadgaon", "Dehu Road"],
            "Baramati": ["Baramati", "Nira", "Supa", "Garade"],
            "Daund": ["Daund", "Kadus", "Yevat"]
        };

        // --- STATE ---
        const state = {
            selectedTalukas: new Set(),
            selectedVillages: new Set(), // stored as "Taluka|Village"
            imageFile: null,
            textValue: ""
        };

        // --- DOM ELEMENTS ---
        const talukaListEl = document.getElementById('taluka-list-container');
        const villageSectionEl = document.getElementById('village-section');
        const villageListEl = document.getElementById('village-list-container');
        const modalEl = document.getElementById('resultModal');
        const modalBody = document.getElementById('modalBody');

        // --- INITIALIZATION ---
        function init() {
            renderTalukas();
        }

        // 1. RENDER TALUKAS
        function renderTalukas() {
            talukaListEl.innerHTML = '';
            Object.keys(districtData).sort().forEach(taluka => {
                const label = document.createElement('label');
                label.className = 'custom-checkbox';
                
                const input = document.createElement('input');
                input.type = 'checkbox';
                input.value = taluka;
                input.onchange = (e) => toggleTaluka(taluka, e.target.checked);

                label.appendChild(input);
                label.appendChild(document.createTextNode(taluka));
                talukaListEl.appendChild(label);
            });
        }

        // 2. TOGGLE TALUKA LOGIC
        function toggleTaluka(taluka, isChecked) {
            if (isChecked) {
                state.selectedTalukas.add(taluka);
            } else {
                state.selectedTalukas.delete(taluka);
                // Also remove associated villages from state
                const villages = districtData[taluka];
                villages.forEach(v => state.selectedVillages.delete(`${taluka}|${v}`));
            }
            renderVillages();
        }

        // 3. RENDER VILLAGES
        function renderVillages() {
            villageListEl.innerHTML = '';
            
            if (state.selectedTalukas.size === 0) {
                villageSectionEl.style.display = 'none';
                return;
            }

            villageSectionEl.style.display = 'block';

            // Iterate through selected talukas (sorted)
            Array.from(state.selectedTalukas).sort().forEach(taluka => {
                const group = document.createElement('div');
                group.style.marginBottom = '1rem';

                // Sub-header for this specific taluka
                const header = document.createElement('div');
                header.className = 'chk-header';
                header.style.fontSize = '0.85rem';
                header.style.color = 'var(--text-main)';
                header.textContent = `Villages in ${taluka}`;
                
                const grid = document.createElement('div');
                grid.className = 'village-list-grid';

                // Render village checkboxes
                const villages = districtData[taluka];
                villages.forEach(village => {
                    const villageId = `${taluka}|${village}`;
                    const isSelected = state.selectedVillages.has(villageId);

                    const vLabel = document.createElement('label');
                    vLabel.className = 'custom-checkbox';

                    const vInput = document.createElement('input');
                    vInput.type = 'checkbox';
                    vInput.checked = isSelected;
                    vInput.onchange = (e) => toggleVillage(villageId, e.target.checked);

                    vLabel.appendChild(vInput);
                    vLabel.appendChild(document.createTextNode(village));
                    grid.appendChild(vLabel);
                });

                group.appendChild(header);
                group.appendChild(grid);
                villageListEl.appendChild(group);
            });
        }

        function toggleVillage(id, isChecked) {
            if (isChecked) state.selectedVillages.add(id);
            else state.selectedVillages.delete(id);
        }

        // 4. IMAGE HANDLING
        function handleImageUpload(event) {
            const file = event.target.files[0];
            if (file) {
                state.imageFile = file;
                const reader = new FileReader();
                reader.onload = function(e) {
                    document.getElementById('imagePreview').src = e.target.result;
                    document.getElementById('previewContainer').style.display = 'block';
                    document.getElementById('dropZone').style.display = 'none';
                }
                reader.readAsDataURL(file);
            }
        }

        function removeImage() {
            state.imageFile = null;
            document.getElementById('imageInput').value = ''; // Reset input
            document.getElementById('previewContainer').style.display = 'none';
            document.getElementById('dropZone').style.display = 'block';
        }

        // 5. SUBMISSION LOGIC
        function handleSubmit(e) {
            e.preventDefault();
            
            // Get Text
            state.textValue = document.getElementById('textInput').value;

            // Basic Validation
            if (state.selectedTalukas.size === 0) {
                alert("Please select at least one Taluka.");
                return;
            }

            // Prepare Data for Modal
            let talukaHtml = Array.from(state.selectedTalukas).map(t => `<span style="background:#e0e7ff; color:#4338ca; padding:2px 6px; border-radius:4px; font-size:0.85rem; margin-right:4px;">${t}</span>`).join('');
            
            let villageHtml = '';
            if(state.selectedVillages.size > 0) {
                villageHtml = Array.from(state.selectedVillages).map(id => {
                    const [t, v] = id.split('|');
                    return `<li>${v} <small style="color:#999">(${t})</small></li>`;
                }).join('');
            } else {
                villageHtml = '<li style="color:#999; font-style:italic;">No specific villages selected</li>';
            }

            let imageHtml = state.imageFile 
                ? `<img src="${document.getElementById('imagePreview').src}" style="max-height:100px; border-radius:4px; margin-top:5px;">` 
                : '<span style="color:#999;">No image uploaded</span>';

            const content = `
                <div class="modal-data-row">
                    <div class="modal-label">Selected Talukas</div>
                    <div class="modal-value" style="margin-top:0.5rem;">${talukaHtml}</div>
                </div>
                <div class="modal-data-row">
                    <div class="modal-label">Selected Villages</div>
                    <ul class="modal-value" style="padding-left:1.2rem; margin-top:0.25rem;">${villageHtml}</ul>
                </div>
                <div class="modal-data-row">
                    <div class="modal-label">Uploaded Image</div>
                    <div class="modal-value">${imageHtml}</div>
                </div>
                <div class="modal-data-row" style="border-bottom:none;">
                    <div class="modal-label">Remarks / Text</div>
                    <div class="modal-value">${state.textValue || '<em style="color:#999">No text entered</em>'}</div>
                </div>
            `;

            modalBody.innerHTML = content;
            modalEl.style.display = 'flex';
        }

        function closeModal(e) {
            if (e.target === modalEl) {
                modalEl.style.display = 'none';
            }
        }
        function closeModalDirectly() {
            modalEl.style.display = 'none';
        }

        // Run Init
        init();

    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pune District Data Entry</title>
    <style>
        :root {
            --primary: #4f46e5; /* Indigo 600 */
            --p