<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Pedágios, Tributos e Frete</title>
    <style>
        :root {
            --bg-color: #f5f7f9;
            --text-color: #333;
            --container-bg: white;
            --section-bg: #f8f9fa;
            --result-bg: #e8f4fc;
            --tribut-bg: #f0f8f0;
            --frete-bg: #fef2f2;
            --border-color: #ddd;
            --header-color: #2c3e50;
            --accent-color: #3498db;
            --highlight-bg: #fff8e1;
            --success-bg: #d4edda;
            --error-color: #e74c3c;
        }
        
        [data-theme="dark"] {
            --bg-color: #1a1a1a;
            --text-color: #f0f0f0;
            --container-bg: #2a2a2a;
            --section-bg: #333;
            --result-bg: #1e3a5f;
            --tribut-bg: #1e4620;
            --frete-bg: #4a1c1c;
            --border-color: #555;
            --header-color: #e0e0e0;
            --accent-color: #60a5fa;
            --highlight-bg: #4a3f00;
            --success-bg: #2d5a2d;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.5;
            padding: 10px;
            transition: background-color 0.3s, color 0.3s;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            background-color: var(--container-bg);
            border-radius: 6px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
            padding: 15px;
        }
        
        h1 {
            text-align: center;
            color: var(--header-color);
            margin-bottom: 10px;
            font-size: 22px;
        }
        
        h2 {
            color: var(--header-color);
            margin: 10px 0 8px;
            padding-bottom: 6px;
            border-bottom: 1px solid var(--accent-color);
            font-size: 16px;
        }
        
        h3 {
            color: var(--header-color);
            margin: 10px 0 6px;
            font-size: 14px;
        }
        
        .description {
            text-align: center;
            margin-bottom: 15px;
            color: var(--text-color);
            opacity: 0.8;
            font-size: 13px;
        }
        
        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 15px;
        }
        
        @media (max-width: 1100px) {
            .main-content {
                grid-template-columns: 1fr;
            }
        }
        
        .input-section, .tribut-section, .frete-section {
            background-color: var(--section-bg);
            padding: 12px;
            border-radius: 5px;
        }
        
        .tribut-section {
            background-color: var(--tribut-bg);
        }
        
        .frete-section {
            background-color: var(--frete-bg);
        }
        
        .result-section, .tribut-result, .frete-result {
            background-color: var(--result-bg);
            padding: 12px;
            border-radius: 5px;
            margin-top: 10px;
        }
        
        .form-group {
            margin-bottom: 10px;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            color: var(--header-color);
            font-size: 13px;
        }
        
        select, input {
            width: 100%;
            padding: 8px;
            border: 1px solid var(--border-color);
            border-radius: 4px;
            font-size: 13px;
            background-color: var(--container-bg);
            color: var(--text-color);
        }
        
        select:focus, input:focus {
            outline: none;
            border-color: var(--accent-color);
            box-shadow: 0 0 3px rgba(52, 152, 219, 0.5);
        }
        
        .checkbox-group {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-top: 6px;
        }
        
        .checkbox-item {
            display: flex;
            align-items: center;
            background-color: var(--highlight-bg);
            padding: 5px 8px;
            border-radius: 4px;
            border: 1px solid var(--border-color);
            font-size: 12px;
        }
        
        .checkbox-item input {
            width: auto;
            margin-right: 5px;
        }
        
        button {
            padding: 8px;
            background-color: var(--accent-color);
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 13px;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.3s;
            margin: 6px 3px;
        }
        
        button:hover {
            background-color: #2980b9;
        }
        
        .button-group {
            display: flex;
            flex-wrap: wrap;
            gap: 6px;
            margin-top: 10px;
        }
        
        .result-item {
            display: flex;
            justify-content: space-between;
            margin-bottom: 8px;
            padding-bottom: 8px;
            border-bottom: 1px dashed var(--border-color);
            font-size: 13px;
        }
        
        .result-item:last-child {
            border-bottom: none;
        }
        
        .result-label, .result-value {
            font-weight: 600;
            color: var(--header-color);
        }
        
        .total {
            font-size: 16px;
            color: var(--error-color);
            margin-top: 10px;
            padding-top: 10px;
            border-top: 1px solid var(--border-color);
        }
        
        .table-container {
            margin-top: 20px;
            overflow-x: auto;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }
        
        th, td {
            padding: 8px 10px;
            text-align: center;
            border: 1px solid var(--border-color);
        }
        
        th {
            background-color: var(--accent-color);
            color: white;
            font-weight: 600;
        }
        
        tr:nth-child(even) {
            background-color: var(--section-bg);
        }
        
        tr:hover {
            background-color: var(--highlight-bg);
        }
        
        .editable-cell {
            background-color: var(--highlight-bg);
        }
        
        .editable-cell input {
            width: 90%;
            padding: 3px;
            text-align: center;
            font-size: 12px;
            background-color: var(--container-bg);
            color: var(--text-color);
        }
        
        .note {
            margin-top: 10px;
            padding: 10px;
            background-color: var(--highlight-bg);
            border-left: 3px solid #ffc107;
            font-size: 12px;
        }
        
        .edit-buttons {
            margin: 10px 0;
            text-align: center;
        }
        
        .save-btn {
            background-color: #27ae60;
        }
        
        .save-btn:hover {
            background-color: #219653;
        }
        
        .reset-btn {
            background-color: var(--error-color);
        }
        
        .reset-btn:hover {
            background-color: #c0392b;
        }
        
        .copy-btn {
            background-color: #9b59b6;
            margin-top: 6px;
            width: 100%;
        }
        
        .copy-btn:hover {
            background-color: #8e44ad;
        }
        
        .tribut-form, .frete-form {
            display: grid;
            grid-template-columns: 1fr;
            gap: 10px;
        }
        
        .success-message {
            background-color: var(--success-bg);
            color: #155724;
            padding: 6px;
            border-radius: 4px;
            margin-top: 6px;
            text-align: center;
            display: none;
            font-size: 12px;
        }
        
        .theme-toggle {
            position: fixed;
            top: 10px;
            right: 10px;
            background: none;
            border: 2px solid var(--accent-color);
            color: var(--accent-color);
            width: 35px;
            height: 35px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 16px;
            transition: all 0.3s;
            z-index: 1000;
        }
        
        .theme-toggle:hover {
            background-color: var(--accent-color);
            color: white;
        }
        
        .theme-toggle[data-theme="dark"] {
            color: var(--accent-color);
        }
    </style>
</head>
<body>
    <button class="theme-toggle" id="themeToggle" title="Alternar tema">☀️</button>
    
    <div class="container">
        <h1>Calculadora de Pedágios, Tributos e Frete</h1>
        <p class="description">Calcule pedágios, tributos (Advalorem e GRISS) e frete com ajustes</p>
        
        <div class="main-content">
            <div class="input-section">
                <h2>Cálculo de Pedágios</h2>
                <div class="form-group">
                    <label for="vehicleType">Veículo:</label>
                    <select id="vehicleType">
                        <option value="pickup">PICK UP (2 eixos)</option>
                        <option value="sprinter">SPRINTER/F350 (2 eixos)</option>
                        <option value="toco">TOCO (2 eixos - Duplo)</option>
                        <option value="truck">TRUCK (3 eixos - Duplo)</option>
                        <option value="carreta5">CARRETA (5 eixos - Duplo)</option>
                        <option value="carreta6" selected>CARRETA (6 eixos - Duplo)</option>
                        <option value="carreta7">CARRETA (7 eixos - Duplo)</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label>Trechos de pedágio:</label>
                    <div class="checkbox-group">
                        <!-- Checkboxes serão populados via JavaScript -->
                    </div>
                </div>
                
                <div class="button-group">
                    <button id="calculateBtn">Calcular</button>
                    <button id="selectAllBtn">Selecionar Todos</button>
                    <button id="clearAllBtn">Limpar</button>
                </div>
                
                <div class="result-section">
                    <h3>Resultado</h3>
                    <div class="result-item">
                        <span class="result-label">Veículo:</span>
                        <span class="result-value" id="resultVehicle">CARRETA (6 eixos)</span>
                    </div>
                    <div class="result-item">
                        <span class="result-label">Trechos:</span>
                        <span class="result-value" id="resultSegments">Nenhum</span>
                    </div>
                    <div class="result-item">
                        <span class="result-label">Pedágios:</span>
                        <span class="result-value" id="resultToll">R$ 0,00</span>
                    </div>
                    <div class="result-item">
                        <span class="result-label">Taxa (15%):</span>
                        <span class="result-value" id="resultFee">R$ 0,00</span>
                    </div>
                    <div class="result-item total">
                        <span class="result-label">TOTAL:</span>
                        <span class="result-value" id="resultTotal">R$ 0,00</span>
                    </div>
                    
                    <button id="copyTollBtn" class="copy-btn">Copiar</button>
                    <div id="tollCopySuccess" class="success-message">Copiado!</div>
                </div>
            </div>
            
            <div class="tribut-section">
                <h2>Cálculo de Tributos</h2>
                <div class="tribut-form">
                    <div class="form-group">
                        <label for="nfValue">Nota Fiscal:</label>
                        <input type="text" id="nfValue" placeholder="0,00" step="0.01" min="0">
                    </div>
                    <div class="form-group">
                        <label for="additionalNfValue">Adicionar outra Nota Fiscal:</label>
                        <input type="text" id="additionalNfValue" placeholder="0,00" step="0.01" min="0">
                    </div>
                    <div class="form-group">
                        <label for="advaloremPercent">Advalorem (%):</label>
                        <input type="number" id="advaloremPercent" value="0.10" step="0.01" min="0">
                    </div>
                    <div class="form-group">
                        <label for="grissPercent">GRISS (%):</label>
                        <input type="number" id="grissPercent" value="0.05" step="0.01" min="0">
                    </div>
                    <div class="form-group">
                        <button id="addNfBtn">Adicionar NF</button>
                        <button id="calculateTributBtn">Calcular</button>
                    </div>
                </div>
                
                <div class="tribut-result">
                    <h3>Resultado</h3>
                    <div class="result-item">
                        <span class="result-label">Nota Fiscal:</span>
                        <span class="result-value" id="resultNfValue">R$ 0,00</span>
                    </div>
                    <div class="result-item">
                        <span class="result-label">Advalorem (<span id="advaloremPercentDisplay">0.10</span>%):</span>
                        <span class="result-value" id="resultAdvalorem">R$ 0,00</span>
                    </div>
                    <div class="result-item">
                        <span class="result-label">GRISS (<span id="grissPercentDisplay">0.05</span>%):</span>
                        <span class="result-value" id="resultGriss">R$ 0,00</span>
                    </div>
                    <div class="result-item total">
                        <span class="result-label">Total:</span>
                        <span class="result-value" id="resultTotalTribut">R$ 0,00</span>
                    </div>
                    
                    <button id="copyAdvaloremBtn" class="copy-btn">Copiar Advalorem</button>
                    <button id="copyGrissBtn" class="copy-btn">Copiar GRISS</button>
                    <button id="copyTributBtn" class="copy-btn">Copiar Tudo</button>
                    <div id="tributCopySuccess" class="success-message">Copiado!</div>
                </div>
            </div>
            
            <div class="frete-section">
                <h2>Cálculo de Frete</h2>
                <div class="frete-form">
                    <div class="form-group">
                        <label for="freteValue">Frete Base:</label>
                        <input type="text" id="freteValue" placeholder="0,00" step="0.01" min="0">
                    </div>
                    <div class="form-group">
                        <div class="button-group">
                            <button id="addFreteBtn">+30% (Químicos)</button>
                            <button id="subtractFreteBtn">-30% (Retorno)</button>
                        </div>
                    </div>
                </div>
                
                <div class="frete-result">
                    <h3>Resultado</h3>
                    <div class="result-item">
                        <span class="result-label">Base:</span>
                        <span class="result-value" id="resultFreteBase">R$ 0,00</span>
                    </div>
                    <div class="result-item">
                        <span class="result-label">Adicional Químicos (30%):</span>
                        <span class="result-value" id="resultFreteChemical">R$ 0,00</span>
                    </div>
                    <div class="result-item total">
                        <span class="result-label">Final:</span>
                        <span class="result-value" id="resultFreteTotal">R$ 0,00</span>
                    </div>
                    
                    <button id="copyFreteBtn" class="copy-btn">Copiar</button>
                    <div id="freteCopySuccess" class="success-message">Copiado!</div>
                </div>
            </div>
        </div>
        
        <div class="table-container">
            <h2>Tabela de Pedágios (Editável)</h2>
            <p>Valores incluem taxa de 15%</p>
            <div class="edit-buttons">
                <button id="editTableBtn" class="save-btn">Editar</button>
                <button id="saveTableBtn" class="save-btn" style="display:none;">Salvar</button>
                <button id="cancelEditBtn" class="reset-btn" style="display:none;">Cancelar</button>
                <button id="resetTableBtn" class="reset-btn">Restaurar</button>
                <button id="addColumnBtn" class="save-btn">Adicionar Coluna</button>
            </div>
            <table id="tollTable">
                <thead>
                    <tr>
                        <th>Veículo</th>
                        <th>Eixos</th>
                        <!-- Colunas serão populadas via JavaScript -->
                    </tr>
                </thead>
                <tbody>
                    <!-- Os dados serão preenchidos via JavaScript -->
                </tbody>
            </table>
            <div class="note">
                <p><strong>Instruções:</strong> Clique em "Editar" para alterar os valores dos pedágios. Após as alterações, clique em "Salvar". Use "Adicionar Coluna" para criar novas rotas extras. Use "Restaurar" para voltar aos valores originais (remove colunas extras).</p>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Dados originais dos pedágios (valores com taxa de 15%)
            const originalTollData = {
                'pickup': {
                    'name': 'PICK UP (2 eixos)',
                    'eixos': '2',
                    'values': {
                        'rjPonte': 16.12,
                        'rjMage': 47.29,
                        'niteroi': 8.82,
                        'rioOstras': 35.29,
                        'macae': 35.29,
                        'sjBarra': 52.94,
                        'caboFrio': 42.59,
                        'angraPonte': 37.76
                    }
                },
                'sprinter': {
                    'name': 'SPRINTER/F350 (2 eixos)',
                    'eixos': '2',
                    'values': {
                        'rjPonte': 16.12,
                        'rjMage': 47.29,
                        'niteroi': 8.82,
                        'rioOstras': 35.29,
                        'macae': 35.29,
                        'sjBarra': 52.94,
                        'caboFrio': 42.59,
                        'angraPonte': 37.76
                    }
                },
                'toco': {
                    'name': 'TOCO (2 eixos - Duplo)',
                    'eixos': '2 (Duplo)',
                    'values': {
                        'rjPonte': 32.24,
                        'rjMage': 94.59,
                        'niteroi': 17.65,
                        'rioOstras': 70.59,
                        'macae': 70.59,
                        'sjBarra': 105.88,
                        'caboFrio': 85.18,
                        'angraPonte': 75.53
                    }
                },
                'truck': {
                    'name': 'TRUCK (3 eixos - Duplo)',
                    'eixos': '3 (Duplo)',
                    'values': {
                        'rjPonte': 48.35,
                        'rjMage': 141.88,
                        'niteroi': 26.47,
                        'rioOstras': 105.88,
                        'macae': 105.88,
                        'sjBarra': 158.82,
                        'caboFrio': 127.76,
                        'angraPonte': 113.29
                    }
                },
                'carreta5': {
                    'name': 'CARRETA (5 eixos - Duplo)',
                    'eixos': '5 (Duplo)',
                    'values': {
                        'rjPonte': 80.59,
                        'rjMage': 236.47,
                        'niteroi': 44.12,
                        'rioOstras': 176.47,
                        'macae': 176.47,
                        'sjBarra': 264.71,
                        'caboFrio': 212.94,
                        'angraPonte': 188.82
                    }
                },
                'carreta6': {
                    'name': 'CARRETA (6 eixos - Duplo)',
                    'eixos': '6 (Duplo)',
                    'values': {
                        'rjPonte': 96.71,
                        'rjMage': 283.76,
                        'niteroi': 52.94,
                        'rioOstras': 211.76,
                        'macae': 211.76,
                        'sjBarra': 317.65,
                        'caboFrio': 255.53,
                        'angraPonte': 226.59
                    }
                },
                'carreta7': {
                    'name': 'CARRETA (7 eixos - Duplo)',
                    'eixos': '7 (Duplo)',
                    'values': {
                        'rjPonte': 112.82,
                        'rjMage': 331.06,
                        'niteroi': 61.76,
                        'rioOstras': 247.06,
                        'macae': 247.06,
                        'sjBarra': 370.59,
                        'caboFrio': 298.12,
                        'angraPonte': 264.35
                    }
                }
            };

            // Segmentos originais
            const originalSegments = [
                {key: 'rjPonte', name: 'RJ Ponte'},
                {key: 'rjMage', name: 'RJ Mage'},
                {key: 'niteroi', name: 'Niteroi'},
                {key: 'rioOstras', name: 'Rio das Ostras'},
                {key: 'macae', name: 'Macae'},
                {key: 'sjBarra', name: 'SJ da Barra'},
                {key: 'caboFrio', name: 'Cabo Frio'},
                {key: 'angraPonte', name: 'Angra via Ponte'}
            ];

            // Carregar segmentos
            let segments = loadData('segments', JSON.parse(JSON.stringify(originalSegments)));

            // Cópia dos dados para edição
            let tollData = loadData('tollData', JSON.parse(JSON.stringify(originalTollData)));

            // Garantir que tollData tenha todos os valores para os segmentos atuais
            segments.forEach(seg => {
                Object.keys(tollData).forEach(vk => {
                    if (!tollData[vk].values[seg.key]) {
                        tollData[vk].values[seg.key] = 0;
                    }
                });
            });

            // Mapeamento dinâmico dos nomes dos trechos
            let segmentNames = {};
            segments.forEach(s => {
                segmentNames[s.key] = s.name;
            });

            // Elementos da interface
            const calculateBtn = document.getElementById('calculateBtn');
            const selectAllBtn = document.getElementById('selectAllBtn');
            const clearAllBtn = document.getElementById('clearAllBtn');
            const editTableBtn = document.getElementById('editTableBtn');
            const saveTableBtn = document.getElementById('saveTableBtn');
            const cancelEditBtn = document.getElementById('cancelEditBtn');
            const resetTableBtn = document.getElementById('resetTableBtn');
            const addColumnBtn = document.getElementById('addColumnBtn');
            const tollTable = document.getElementById('tollTable');
            
            const calculateTributBtn = document.getElementById('calculateTributBtn');
            const addNfBtn = document.getElementById('addNfBtn');
            const copyTollBtn = document.getElementById('copyTollBtn');
            const copyAdvaloremBtn = document.getElementById('copyAdvaloremBtn');
            const copyGrissBtn = document.getElementById('copyGrissBtn');
            const copyTributBtn = document.getElementById('copyTributBtn');
            const addFreteBtn = document.getElementById('addFreteBtn');
            const subtractFreteBtn = document.getElementById('subtractFreteBtn');
            const copyFreteBtn = document.getElementById('copyFreteBtn');
            
            const nfValueInput = document.getElementById('nfValue');
            const additionalNfValueInput = document.getElementById('additionalNfValue');
            const advaloremPercentInput = document.getElementById('advaloremPercent');
            const grissPercentInput = document.getElementById('grissPercent');
            const freteValueInput = document.getElementById('freteValue');
            
            // Carregar valores salvos
            nfValueInput.value = loadData('nfValue', '') || '';
            advaloremPercentInput.value = loadData('advaloremPercent', '0.10');
            grissPercentInput.value = loadData('grissPercent', '0.05');
            freteValueInput.value = loadData('freteValue', '') || '';
            
            // Inicializar tema
            const savedTheme = loadData('theme', 'light');
            document.documentElement.setAttribute('data-theme', savedTheme);
            updateThemeToggle(savedTheme);
            
            // Listeners
            calculateBtn.addEventListener('click', calculateToll);
            selectAllBtn.addEventListener('click', selectAllSegments);
            clearAllBtn.addEventListener('click', clearAllSegments);
            editTableBtn.addEventListener('click', enableTableEditing);
            saveTableBtn.addEventListener('click', saveTableValues);
            cancelEditBtn.addEventListener('click', cancelTableEditing);
            resetTableBtn.addEventListener('click', resetTableValues);
            addColumnBtn.addEventListener('click', addNewColumn);
            
            calculateTributBtn.addEventListener('click', calculateTribut);
            addNfBtn.addEventListener('click', addAdditionalNf);
            copyTollBtn.addEventListener('click', copyTollValues);
            copyAdvaloremBtn.addEventListener('click', () => copySingleValue('advalorem'));
            copyGrissBtn.addEventListener('click', () => copySingleValue('griss'));
            copyTributBtn.addEventListener('click', copyTributValues);
            addFreteBtn.addEventListener('click', () => calculateFrete('add'));
            subtractFreteBtn.addEventListener('click', () => calculateFrete('subtract'));
            copyFreteBtn.addEventListener('click', copyFreteValue);
            
            advaloremPercentInput.addEventListener('input', function() {
                document.getElementById('advaloremPercentDisplay').textContent = this.value;
                saveData('advaloremPercent', this.value);
            });
            
            grissPercentInput.addEventListener('input', function() {
                document.getElementById('grissPercentDisplay').textContent = this.value;
                saveData('grissPercent', this.value);
            });
            
            nfValueInput.addEventListener('input', handleNfInput);
            nfValueInput.addEventListener('blur', handleNfBlur);
            
            additionalNfValueInput.addEventListener('input', handleNfInput);
            additionalNfValueInput.addEventListener('blur', handleAdditionalNfBlur);
            
            freteValueInput.addEventListener('input', handleFreteInput);
            freteValueInput.addEventListener('blur', handleFreteBlur);
            
            document.getElementById('themeToggle').addEventListener('click', toggleTheme);
            document.getElementById('vehicleType').addEventListener('change', calculateToll);
            
            // Inicializar
            populateCheckboxes();
            populateTable();
            calculateToll();
            calculateTribut();
            calculateFrete();
            
            function loadData(key, defaultValue) {
                const item = localStorage.getItem(key);
                if (item === null) return defaultValue;
                try {
                    return JSON.parse(item);
                } catch {
                    return item;
                }
            }
            
            function saveData(key, value) {
                localStorage.setItem(key, typeof value === 'string' ? value : JSON.stringify(value));
            }
            
            function populateCheckboxes() {
                const checkboxGroup = document.querySelector('.checkbox-group');
                checkboxGroup.innerHTML = '';
                
                segments.forEach(seg => {
                    const div = document.createElement('div');
                    div.className = 'checkbox-item';
                    div.innerHTML = `<input type="checkbox" id="${seg.key}" value="${seg.key}"><label for="${seg.key}">${seg.name}</label>`;
                    checkboxGroup.appendChild(div);
                });
                
                // Adicionar listeners para os checkboxes
                document.querySelectorAll('.checkbox-item input').forEach(cb => {
                    cb.addEventListener('change', calculateToll);
                });
            }
            
            function populateTable() {
                const thead = tollTable.querySelector('thead tr');
                
                // Manter as duas primeiras colunas fixas (Veículo e Eixos) e limpar as demais
                while (thead.children.length > 2) {
                    thead.removeChild(thead.lastChild);
                }
                
                // Adicionar th para cada segmento
                segments.forEach(seg => {
                    const th = document.createElement('th');
                    th.textContent = seg.name;
                    thead.appendChild(th);
                });
                
                const tbody = tollTable.querySelector('tbody');
                tbody.innerHTML = '';
                
                const rowOrder = ['pickup', 'sprinter', 'toco', 'truck', 'carreta5', 'carreta6', 'carreta7'];
                
                rowOrder.forEach(vehicleKey => {
                    const vehicle = tollData[vehicleKey];
                    const row = document.createElement('tr');
                    
                    const nameCell = document.createElement('td');
                    nameCell.textContent = vehicle.name;
                    row.appendChild(nameCell);
                    
                    const eixosCell = document.createElement('td');
                    eixosCell.textContent = vehicle.eixos;
                    row.appendChild(eixosCell);
                    
                    segments.forEach(segment => {
                        const valueCell = document.createElement('td');
                        valueCell.className = 'editable-cell';
                        valueCell.dataset.vehicle = vehicleKey;
                        valueCell.dataset.segment = segment.key;
                        
                        const input = document.createElement('input');
                        input.type = 'text';
                        const val = vehicle.values[segment.key] || 0;
                        input.value = formatCurrencyValue(val);
                        input.disabled = true;
                        
                        valueCell.appendChild(input);
                        row.appendChild(valueCell);
                    });
                    
                    tbody.appendChild(row);
                });
            }
            
            function addNewColumn() {
                const name = prompt('Nome da nova rota:');
                if (!name || name.trim() === '') return;
                
                const newKey = 'extra_' + Date.now();
                const newSeg = {key: newKey, name: name.trim()};
                
                segments.push(newSeg);
                
                // Adicionar valor inicial 0 para todos os veículos
                Object.keys(tollData).forEach(vk => {
                    tollData[vk].values[newKey] = 0;
                });
                
                segmentNames[newKey] = name.trim();
                
                // Repopular
                populateCheckboxes();
                populateTable();
                
                // Salvar
                saveData('segments', segments);
                saveData('tollData', tollData);
                
                alert('Nova coluna adicionada com sucesso!');
            }
            
            function handleNfInput(e) {
                let value = e.target.value.replace(/[^0-9,]/g, '');
                if (value.includes(',')) {
                    const parts = value.split(',');
                    if (parts[1].length > 2) {
                        parts[1] = parts[1].substring(0, 2);
                    }
                    value = parts.join(',');
                }
                e.target.value = value;
            }
            
            function handleNfBlur(e) {
                let value = e.target.value;
                if (value === '') {
                    e.target.value = '';
                    saveData('nfValue', '');
                    return;
                }
                let numValue = parseFloat(value.replace(',', '.')) || 0;
                e.target.value = numValue.toFixed(2).replace('.', ',');
                saveData('nfValue', e.target.value);
                calculateTribut();
            }
            
            function handleAdditionalNfBlur(e) {
                let value = e.target.value;
                if (value === '') {
                    e.target.value = '';
                    return;
                }
                let numValue = parseFloat(value.replace(',', '.')) || 0;
                e.target.value = numValue.toFixed(2).replace('.', ',');
            }
            
            function handleFreteInput(e) {
                let value = e.target.value.replace(/[^0-9,]/g, '');
                if (value.includes(',')) {
                    const parts = value.split(',');
                    if (parts[1].length > 2) {
                        parts[1] = parts[1].substring(0, 2);
                    }
                    value = parts.join(',');
                }
                e.target.value = value;
            }
            
            function handleFreteBlur(e) {
                let value = e.target.value;
                if (value === '') {
                    e.target.value = '';
                    saveData('freteValue', '');
                    return;
                }
                let numValue = parseFloat(value.replace(',', '.')) || 0;
                e.target.value = numValue.toFixed(2).replace('.', ',');
                saveData('freteValue', e.target.value);
                calculateFrete();
            }
            
            function addAdditionalNf() {
                let nfValue = parseFloat(nfValueInput.value.replace(',', '.')) || 0;
                let additionalNf = parseFloat(additionalNfValueInput.value.replace(',', '.')) || 0;
                nfValue += additionalNf;
                nfValueInput.value = nfValue.toFixed(2).replace('.', ',');
                saveData('nfValue', nfValueInput.value);
                additionalNfValueInput.value = '';
                calculateTribut();
            }
            
            function toggleTheme() {
                const currentTheme = document.documentElement.getAttribute('data-theme');
                const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
                document.documentElement.setAttribute('data-theme', newTheme);
                updateThemeToggle(newTheme);
                saveData('theme', newTheme);
            }
            
            function updateThemeToggle(theme) {
                const toggle = document.getElementById('themeToggle');
                toggle.textContent = theme === 'dark' ? '☀️' : '🌙';
                toggle.title = theme === 'dark' ? 'Modo claro' : 'Modo escuro';
            }
            
            function enableTableEditing() {
                const inputs = tollTable.querySelectorAll('input');
                inputs.forEach(input => {
                    input.disabled = false;
                    input.style.backgroundColor = '#fff';
                });
                
                editTableBtn.style.display = 'none';
                saveTableBtn.style.display = 'inline-block';
                cancelEditBtn.style.display = 'inline-block';
            }
            
            function saveTableValues() {
                const inputs = tollTable.querySelectorAll('input');
                inputs.forEach(input => {
                    input.disabled = true;
                    input.style.backgroundColor = '';
                    
                    const vehicleKey = input.parentElement.dataset.vehicle;
                    const segmentKey = input.parentElement.dataset.segment;
                    
                    const rawValue = input.value.replace('R$ ', '').trim();
                    const value = parseFloat(rawValue.replace(',', '.'));
                    
                    if (!isNaN(value)) {
                        tollData[vehicleKey].values[segmentKey] = value;
                        input.value = formatCurrencyValue(value);
                    }
                });
                
                saveData('tollData', tollData);
                
                editTableBtn.style.display = 'inline-block';
                saveTableBtn.style.display = 'none';
                cancelEditBtn.style.display = 'none';
                
                calculateToll();
                
                alert('Valores atualizados com sucesso!');
            }
            
            function cancelTableEditing() {
                populateTable();
                editTableBtn.style.display = 'inline-block';
                saveTableBtn.style.display = 'none';
                cancelEditBtn.style.display = 'none';
            }
            
            function resetTableValues() {
                if (confirm('Tem certeza que deseja restaurar os valores originais? Isso removerá colunas extras adicionadas.')) {
                    segments = JSON.parse(JSON.stringify(originalSegments));
                    tollData = JSON.parse(JSON.stringify(originalTollData));
                    segmentNames = {};
                    segments.forEach(s => segmentNames[s.key] = s.name);
                    saveData('segments', segments);
                    saveData('tollData', tollData);
                    populateCheckboxes();
                    populateTable();
                    calculateToll();
                    alert('Valores restaurados com sucesso!');
                }
            }
            
            function calculateToll() {
                const vehicleType = document.getElementById('vehicleType').value;
                const selectedSegments = [];
                
                const checkboxes = document.querySelectorAll('.checkbox-item input');
                checkboxes.forEach(checkbox => {
                    if (checkbox.checked) {
                        selectedSegments.push(checkbox.value);
                    }
                });
                
                let totalToll = 0;
                selectedSegments.forEach(segment => {
                    const value = tollData[vehicleType].values[segment];
                    if (typeof value === 'number' && !isNaN(value)) {
                        totalToll += value;
                    }
                });
                
                const baseValue = totalToll / 1.15;
                const administrativeFee = totalToll - baseValue;
                
                document.getElementById('resultVehicle').textContent = tollData[vehicleType].name;
                
                if (selectedSegments.length > 0) {
                    const segmentNamesList = selectedSegments.map(seg => segmentNames[seg]).join(', ');
                    document.getElementById('resultSegments').textContent = segmentNamesList;
                } else {
                    document.getElementById('resultSegments').textContent = 'Nenhum';
                }
                
                document.getElementById('resultToll').textContent = formatCurrency(totalToll);
                document.getElementById('resultFee').textContent = formatCurrency(administrativeFee);
                document.getElementById('resultTotal').textContent = formatCurrency(totalToll);
            }
            
            function calculateTribut() {
                let nfValueStr = nfValueInput.value.replace(',', '.');
                const nfValue = parseFloat(nfValueStr) || 0;
                const advaloremPercent = parseFloat(advaloremPercentInput.value) || 0;
                const grissPercent = parseFloat(grissPercentInput.value) || 0;
                
                const advaloremValue = nfValue * (advaloremPercent / 100);
                const grissValue = nfValue * (grissPercent / 100);
                const totalTribut = advaloremValue + grissValue;
                
                document.getElementById('resultNfValue').textContent = formatCurrency(nfValue);
                document.getElementById('resultAdvalorem').textContent = formatCurrency(advaloremValue);
                document.getElementById('resultGriss').textContent = formatCurrency(grissValue);
                document.getElementById('resultTotalTribut').textContent = formatCurrency(totalTribut);
            }
            
            function calculateFrete(type = null) {
                let freteValueStr = freteValueInput.value.replace(',', '.');
                const freteValue = parseFloat(freteValueStr) || 0;
                let freteTotal = freteValue;
                let chemicalAdd = 0;
                
                if (type === 'add') {
                    chemicalAdd = freteValue * 0.3;
                    freteTotal = freteValue * 1.3;
                } else if (type === 'subtract') {
                    freteTotal = freteValue * 0.7;
                }
                
                document.getElementById('resultFreteBase').textContent = formatCurrency(freteValue);
                document.getElementById('resultFreteChemical').textContent = formatCurrency(chemicalAdd);
                document.getElementById('resultFreteTotal').textContent = formatCurrency(freteTotal);
            }
            
            function copyTollValues() {
                const vehicleType = document.getElementById('vehicleType').value;
                const selectedSegments = [];
                
                const checkboxes = document.querySelectorAll('.checkbox-item input');
                checkboxes.forEach(checkbox => {
                    if (checkbox.checked) {
                        selectedSegments.push(checkbox.value);
                    }
                });
                
                let totalToll = 0;
                selectedSegments.forEach(segment => {
                    const value = tollData[vehicleType].values[segment];
                    if (typeof value === 'number' && !isNaN(value)) {
                        totalToll += value;
                    }
                });
                
                const textToCopy = totalToll.toFixed(2).replace('.', ',');
                
                copyToClipboard(textToCopy);
                showSuccess('tollCopySuccess');
            }
            
            function copySingleValue(type) {
                let nfValueStr = nfValueInput.value.replace(',', '.');
                const nfValue = parseFloat(nfValueStr) || 0;
                let value;
                if (type === 'advalorem') {
                    const percent = parseFloat(advaloremPercentInput.value) || 0;
                    value = nfValue * (percent / 100);
                } else if (type === 'griss') {
                    const percent = parseFloat(grissPercentInput.value) || 0;
                    value = nfValue * (percent / 100);
                }
                const textToCopy = value.toFixed(2).replace('.', ',');
                copyToClipboard(textToCopy);
                showSuccess('tributCopySuccess');
            }
            
            function copyTributValues() {
                let nfValueStr = nfValueInput.value.replace(',', '.');
                const nfValue = parseFloat(nfValueStr) || 0;
                const advaloremPercent = parseFloat(advaloremPercentInput.value) || 0;
                const grissPercent = parseFloat(grissPercentInput.value) || 0;
                
                const advaloremValue = nfValue * (advaloremPercent / 100);
                const grissValue = nfValue * (grissPercent / 100);
                const totalTribut = advaloremValue + grissValue;
                
                const textToCopy = `${nfValue.toFixed(2).replace('.', ',')}\n${advaloremValue.toFixed(2).replace('.', ',')}\n${grissValue.toFixed(2).replace('.', ',')}\n${totalTribut.toFixed(2).replace('.', ',')}`;
                
                copyToClipboard(textToCopy);
                showSuccess('tributCopySuccess');
            }
            
            function copyFreteValue() {
                const freteTotal = parseFloat(document.getElementById('resultFreteTotal').textContent.replace('R$ ', '').replace(',', '.')) || 0;
                const textToCopy = freteTotal.toFixed(2).replace('.', ',');
                copyToClipboard(textToCopy);
                showSuccess('freteCopySuccess');
            }
            
            function copyToClipboard(text) {
                navigator.clipboard.writeText(text).catch(() => {
                    const textarea = document.createElement('textarea');
                    textarea.value = text;
                    document.body.appendChild(textarea);
                    textarea.select();
                    document.execCommand('copy');
                    document.body.removeChild(textarea);
                });
            }
            
            function showSuccess(id) {
                const message = document.getElementById(id);
                message.style.display = 'block';
                setTimeout(() => {
                    message.style.display = 'none';
                }, 2000);
            }
            
            function selectAllSegments() {
                const checkboxes = document.querySelectorAll('.checkbox-item input');
                checkboxes.forEach(checkbox => checkbox.checked = true);
                calculateToll();
            }
            
            function clearAllSegments() {
                const checkboxes = document.querySelectorAll('.checkbox-item input');
                checkboxes.forEach(checkbox => checkbox.checked = false);
                calculateToll();
            }
            
            function formatCurrency(value) {
                return 'R$ ' + value.toFixed(2).replace('.', ',');
            }
            
            function formatCurrencyValue(value) {
                return value.toFixed(2).replace('.', ',');
            }
        });
    </script>
</body>
</html>
