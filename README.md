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

        #seletor-frete {
            background: var(--section-bg);
            padding: 15px;
            margin-top: 10px;
            border: 1px solid var(--border-color);
            border-radius: 8px;
        }

        #seletor-frete h4 {
            margin: 0 0 10px;
            color: var(--header-color);
            font-size: 14px;
        }

        #seletor-frete div {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        #seletor-frete select, #seletor-frete button {
            padding: 5px;
            border: 1px solid var(--border-color);
            border-radius: 4px;
        }

        #seletor-frete button {
            background: #9370DB;
            color: white;
            border: none;
            cursor: pointer;
            padding: 5px 10px;
        }

        #seletor-frete button:hover {
            background: #7B68EE;
        }

        #seletor-frete button:disabled {
            background: var(--border-color);
            cursor: not-allowed;
        }

        #info-frete {
            margin: 5px 0;
            color: green;
            font-size: 14px;
        }

        .new-client-btn {
            background: #17a2b8;
            margin-bottom: 10px;
        }

        .new-client-btn:hover {
            background: #138496;
        }

        .client-section {
            margin-bottom: 20px;
            padding: 15px;
            background-color: var(--section-bg);
            border-radius: 5px;
            border: 1px solid var(--border-color);
        }

        .client-section h3 {
            margin-bottom: 10px;
            color: var(--header-color);
        }

        .freteTable th:last-child,
        .freteTable td:last-child {
            width: 50px;
        }

        .delete-row-btn {
            background-color: var(--error-color);
            color: white;
            border: none;
            padding: 2px 6px;
            border-radius: 3px;
            cursor: pointer;
            font-size: 12px;
        }

        .delete-row-btn:hover {
            background-color: #c0392b;
        }

        .editing input {
            background-color: white !important;
            color: black !important;
        }

        .export-import-group {
            margin-top: 10px;
            text-align: center;
        }

        .toggle-mgmt-btn {
            background-color: #f39c12;
            margin-bottom: 10px;
        }

        .toggle-mgmt-btn:hover {
            background-color: #e67e22;
        }

        .mgmt-collapsed .clientFreightContainer,
        .mgmt-collapsed .edit-buttons:not(:first-of-type) {
            display: none;
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
                    <div id="seletor-frete">
                        <h4>Selecionar Frete por Cliente/Rota</h4>
                        <div>
                            <select id="cliente-select">
                                <option value="">Escolha um cliente...</option>
                            </select>
                            <select id="rota-select" disabled>
                                <option value="">Escolha uma rota...</option>
                            </select>
                            <select id="veiculo-select" disabled>
                                <option value="">Escolha o veículo...</option>
                            </select>
                            <button id="puxar-frete-btn" onclick="puxarFrete()" disabled>Puxar Frete Base</button>
                        </div>
                        <p id="info-frete"></p>
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

        <div class="table-container" id="frete-mgmt-container">
            <h2>Gerenciamento de Fretes por Cliente</h2>
            <button id="toggleFreteMgmt" class="toggle-mgmt-btn">Minimizar</button>
            <p>Adicione e edite rotas, veículos e valores de frete manualmente. Cada cliente tem sua tabela separada.</p>
            <div class="edit-buttons">
                <button class="new-client-btn" id="addNewClientBtn">Criar Novo Cliente</button>
                <div class="export-import-group">
                    <button id="exportDataBtn" class="save-btn">Exportar Dados</button>
                    <button id="importDataBtn" class="save-btn">Importar Dados</button>
                </div>
            </div>
            <input type="file" id="importFile" accept=".json" style="display:none;">
            <div id="clientFreightContainer" class="clientFreightContainer">
                <!-- As seções de clientes serão populadas via JavaScript -->
            </div>
            <div class="note">
                <p><strong>Instruções:</strong> Clique em "Criar Novo Cliente" para adicionar um cliente com tabela padrão. Para cada cliente, use "Adicionar Linha" para novas rotas/veículos, "Adicionar Coluna" para campos extras, "Deletar Coluna" (informe índice), e "X" nas linhas para deletar. Em "Editar", altere valores. "Salvar" persiste. "Restaurar Padrão" reseta para vazio. Use "Exportar Dados" para baixar um JSON com todos os dados salvos (tabelas, configurações). "Importar Dados" para carregar um JSON salvo.</p>
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

            // Dados iniciais de fretes (exemplos baseados na tabela Felka/Helix) - mantidos originais como array para seletor
            const originalFreteDataArray = [
                {cliente: 'Helix (Felka)', origem: 'Duque de Caxias', destino: 'Niterói', tipo: 'PICK-UP', capacidade: '500 kg', freteAtual: 538.20, estadia: 400.00, adv: 0.1},
                {cliente: 'Helix (Felka)', origem: 'Duque de Caxias', destino: 'Niterói', tipo: 'SPRINTER OU SIMILAR', capacidade: '1500 KG', freteAtual: 765.44, estadia: 450.00, adv: 0.1},
                {cliente: 'Helix (Felka)', origem: 'Duque de Caxias', destino: 'Niterói', tipo: 'TOCO', capacidade: '6 ton', freteAtual: 861.12, estadia: 550.00, adv: 0.1},
                {cliente: 'Helix (Felka)', origem: 'Duque de Caxias', destino: 'Niterói', tipo: 'TRUCK', capacidade: '12 ton', freteAtual: 980.72, estadia: 650.00, adv: 0.1},
                {cliente: 'Helix (Felka)', origem: 'Macaé', destino: 'Niterói', tipo: 'TRUCK', capacidade: '12 ton', freteAtual: 1913.60, estadia: 650.00, adv: 0.1}
            ];

            // Converter para formato por cliente apenas se não existir em localStorage
            let freteDataArray = loadData('freteDataArray', JSON.parse(JSON.stringify(originalFreteDataArray)));

            // Construir estrutura por cliente a partir do array para edição
            function buildClientDataFromArray() {
                const clientData = {};
                const standardColumnKeys = ['origem', 'destino', 'tipo', 'capacidade', 'freteAtual', 'estadia', 'adv'];
                const standardColumnHeaders = ['Origem', 'Destino', 'Veículo', 'Capacidade', 'Frete Atual', 'Estadia', 'ADV (%)'];

                freteDataArray.forEach(entry => {
                    const client = entry.cliente;
                    if (!clientData[client]) {
                        clientData[client] = {
                            columnKeys: [...standardColumnKeys],
                            columnHeaders: [...standardColumnHeaders],
                            rows: []
                        };
                    }
                    clientData[client].rows.push({
                        origem: entry.origem,
                        destino: entry.destino,
                        tipo: entry.tipo,
                        capacidade: entry.capacidade,
                        freteAtual: entry.freteAtual,
                        estadia: entry.estadia,
                        adv: entry.adv
                    });
                });

                return clientData;
            }

            let freteClients = loadData('freteClients', buildClientDataFromArray());

            // Carregar segmentos e tollData
            let segments = loadData('segments', JSON.parse(JSON.stringify(originalSegments)));
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

            // Elementos da interface (pedágios)
            const calculateBtn = document.getElementById('calculateBtn');
            const selectAllBtn = document.getElementById('selectAllBtn');
            const clearAllBtn = document.getElementById('clearAllBtn');
            const editTableBtn = document.getElementById('editTableBtn');
            const saveTableBtn = document.getElementById('saveTableBtn');
            const cancelEditBtn = document.getElementById('cancelEditBtn');
            const resetTableBtn = document.getElementById('resetTableBtn');
            const addColumnBtn = document.getElementById('addColumnBtn');
            const tollTable = document.getElementById('tollTable');
            
            // Elementos da interface (tributos e frete base)
            const calculateTributBtn = document.getElementById('calculateTributBtn');
            const addNfBtn = document.getElementById('addNfBtn');
            const copyTollBtn = document.getElementById('copyTollBtn');
            const copyAdvaloremBtn = document.getElementById('copyAdvaloremBtn');
            const copyGrissBtn = document.getElementById('copyGrissBtn');
            const copyTributBtn = document.getElementById('copyTributBtn');
            const addFreteBtn = document.getElementById('addFreteBtn');
            const subtractFreteBtn = document.getElementById('subtractFreteBtn');
            const copyFreteBtn = document.getElementById('copyFreteBtn');
            const addNewClientBtn = document.getElementById('addNewClientBtn');
            
            const nfValueInput = document.getElementById('nfValue');
            const additionalNfValueInput = document.getElementById('additionalNfValue');
            const advaloremPercentInput = document.getElementById('advaloremPercent');
            const grissPercentInput = document.getElementById('grissPercent');
            const freteValueInput = document.getElementById('freteValue');
            
            const clientFreightContainer = document.getElementById('clientFreightContainer');
            
            // Elementos para export/import
            const exportDataBtn = document.getElementById('exportDataBtn');
            const importDataBtn = document.getElementById('importDataBtn');
            const importFile = document.getElementById('importFile');
            
            // Elemento para toggle gerenciamento
            const toggleFreteMgmt = document.getElementById('toggleFreteMgmt');
            const freteMgmtContainer = document.getElementById('frete-mgmt-container');
            
            // Carregar valores salvos
            nfValueInput.value = loadData('nfValue', '') || '';
            advaloremPercentInput.value = loadData('advaloremPercent', '0.10');
            grissPercentInput.value = loadData('grissPercent', '0.05');
            freteValueInput.value = loadData('freteValue', '') || '';
            
            // Carregar estado do toggle
            const isCollapsed = loadData('freteMgmtCollapsed', false);
            if (isCollapsed) {
                freteMgmtContainer.classList.add('mgmt-collapsed');
                toggleFreteMgmt.textContent = 'Expandir';
            }
            
            // Inicializar tema
            const savedTheme = loadData('theme', 'light');
            document.documentElement.setAttribute('data-theme', savedTheme);
            updateThemeToggle(savedTheme);
            
            // Listeners (pedágios)
            calculateBtn.addEventListener('click', calculateToll);
            selectAllBtn.addEventListener('click', selectAllSegments);
            clearAllBtn.addEventListener('click', clearAllSegments);
            editTableBtn.addEventListener('click', enableTableEditing);
            saveTableBtn.addEventListener('click', saveTableValues);
            cancelEditBtn.addEventListener('click', cancelTableEditing);
            resetTableBtn.addEventListener('click', resetTableValues);
            addColumnBtn.addEventListener('click', addNewColumn);
            
            // Listeners (tributos e frete)
            calculateTributBtn.addEventListener('click', calculateTribut);
            addNfBtn.addEventListener('click', addAdditionalNf);
            copyTollBtn.addEventListener('click', copyTollValues);
            copyAdvaloremBtn.addEventListener('click', () => copySingleValue('advalorem'));
            copyGrissBtn.addEventListener('click', () => copySingleValue('griss'));
            copyTributBtn.addEventListener('click', copyTributValues);
            addFreteBtn.addEventListener('click', () => calculateFrete('add'));
            subtractFreteBtn.addEventListener('click', () => calculateFrete('subtract'));
            copyFreteBtn.addEventListener('click', copyFreteValue);
            
            // Listener para novo cliente
            addNewClientBtn.addEventListener('click', addNewClient);
            
            // Listeners para export/import
            exportDataBtn.addEventListener('click', exportData);
            importDataBtn.addEventListener('click', () => importFile.click());
            importFile.addEventListener('change', handleImportFile);
            
            // Listener para toggle gerenciamento
            toggleFreteMgmt.addEventListener('click', function() {
                freteMgmtContainer.classList.toggle('mgmt-collapsed');
                const collapsed = freteMgmtContainer.classList.contains('mgmt-collapsed');
                this.textContent = collapsed ? 'Expandir' : 'Minimizar';
                saveData('freteMgmtCollapsed', collapsed);
            });
            
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
            
            // Listener para seletor de frete
            document.getElementById('cliente-select').addEventListener('change', handleClienteChange);
            document.getElementById('rota-select').addEventListener('change', handleRotaChange);
            document.getElementById('veiculo-select').addEventListener('change', handleVeiculoChange);
            
            // Inicializar
            populateCheckboxes();
            populateTable();
            populateFreightTables();
            popularClientes();
            calculateToll();
            calculateTribut();
            calculateFrete();
            
            function loadData(key, defaultValue) {
                const item = localStorage.getItem(key);
                if (item === null) return defaultValue;
                try {
                    return JSON.parse(item);
                } catch {
                    return defaultValue;
                }
            }
            
            function saveData(key, value) {
                localStorage.setItem(key, typeof value === 'string' ? value : JSON.stringify(value));
            }
            
            // Função para sincronizar array e clients
            function syncFreteData() {
                freteDataArray = [];
                Object.keys(freteClients).forEach(clientName => {
                    freteClients[clientName].rows.forEach(row => {
                        const entry = {
                            cliente: clientName,
                            origem: row.origem,
                            destino: row.destino,
                            tipo: row.tipo,
                            capacidade: row.capacidade,
                            freteAtual: row.freteAtual,
                            estadia: row.estadia,
                            adv: row.adv
                        };
                        freteDataArray.push(entry);
                    });
                });
                saveData('freteDataArray', freteDataArray);
                saveData('freteClients', freteClients);
            }
            
            // Função para exportar dados
            function exportData() {
                const data = {
                    freteClients: localStorage.getItem('freteClients'),
                    freteDataArray: localStorage.getItem('freteDataArray'),
                    tollData: localStorage.getItem('tollData'),
                    segments: localStorage.getItem('segments'),
                    theme: localStorage.getItem('theme'),
                    nfValue: localStorage.getItem('nfValue'),
                    advaloremPercent: localStorage.getItem('advaloremPercent'),
                    grissPercent: localStorage.getItem('grissPercent'),
                    freteValue: localStorage.getItem('freteValue')
                };
                const blob = new Blob([JSON.stringify(data, null, 2)], {type: 'application/json'});
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                a.download = 'dados-calculadora.json';
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                URL.revokeObjectURL(url);
                alert('Dados exportados com sucesso! Baixe o arquivo JSON.');
            }
            
            // Função para importar dados
            function handleImportFile(e) {
                const file = e.target.files[0];
                if (!file) return;
                const reader = new FileReader();
                reader.onload = function(event) {
                    try {
                        const data = JSON.parse(event.target.result);
                        Object.keys(data).forEach(key => {
                            if (data[key] !== null) {
                                localStorage.setItem(key, data[key]);
                            }
                        });
                        alert('Dados importados com sucesso! Recarregando a página...');
                        location.reload();
                    } catch (err) {
                        alert('Erro ao importar dados: ' + err.message + '. Verifique se o arquivo é um JSON válido.');
                    }
                };
                reader.readAsText(file);
            }
            
            // Funções para pedágios (mantidas iguais)
            function populateCheckboxes() {
                const checkboxGroup = document.querySelector('.checkbox-group');
                checkboxGroup.innerHTML = '';
                
                segments.forEach(seg => {
                    const div = document.createElement('div');
                    div.className = 'checkbox-item';
                    div.innerHTML = `<input type="checkbox" id="${seg.key}" value="${seg.key}"><label for="${seg.key}">${seg.name}</label>`;
                    checkboxGroup.appendChild(div);
                });
                
                document.querySelectorAll('.checkbox-item input').forEach(cb => {
                    cb.addEventListener('change', calculateToll);
                });
            }
            
            function populateTable() {
                const thead = tollTable.querySelector('thead tr');
                while (thead.children.length > 2) {
                    thead.removeChild(thead.lastChild);
                }
                
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
                
                Object.keys(tollData).forEach(vk => {
                    tollData[vk].values[newKey] = 0;
                });
                
                segmentNames[newKey] = name.trim();
                
                populateCheckboxes();
                populateTable();
                
                saveData('segments', segments);
                saveData('tollData', tollData);
                
                alert('Nova coluna adicionada com sucesso!');
            }
            
            function enableTableEditing() {
                const inputs = tollTable.querySelectorAll('input');
                inputs.forEach(input => {
                    input.disabled = false;
                    input.parentElement.classList.add('editing');
                });
                
                editTableBtn.style.display = 'none';
                saveTableBtn.style.display = 'inline-block';
                cancelEditBtn.style.display = 'inline-block';
            }
            
            function saveTableValues() {
                const inputs = tollTable.querySelectorAll('input');
                inputs.forEach(input => {
                    input.disabled = true;
                    input.parentElement.classList.remove('editing');
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
            
            // Funções para fretes por cliente
            function populateFreightTables() {
                clientFreightContainer.innerHTML = '';
                
                Object.keys(freteClients).forEach(clientName => {
                    const section = createClientSection(clientName, freteClients[clientName]);
                    clientFreightContainer.appendChild(section);
                });
            }

            function createClientSection(clientName, clientData) {
                const section = document.createElement('div');
                section.className = 'client-section';
                section.dataset.client = clientName;

                const title = document.createElement('h3');
                title.textContent = clientName;
                section.appendChild(title);

                const buttonsDiv = document.createElement('div');
                buttonsDiv.className = 'edit-buttons';

                const buttonConfigs = [
                    {type: 'edit', class: 'save-btn', text: 'Editar'},
                    {type: 'save', class: 'save-btn', text: 'Salvar', style: 'display:none;'},
                    {type: 'cancel', class: 'reset-btn', text: 'Cancelar', style: 'display:none;'},
                    {type: 'reset', class: 'reset-btn', text: 'Restaurar Padrão'},
                    {type: 'addRow', class: 'save-btn', text: 'Adicionar Linha'},
                    {type: 'addColumn', class: 'save-btn', text: 'Adicionar Coluna'},
                    {type: 'deleteColumn', class: 'reset-btn', text: 'Deletar Coluna'},
                    {type: 'deleteClient', class: 'reset-btn', text: 'Deletar Cliente'}
                ];

                buttonConfigs.forEach(config => {
                    const btn = document.createElement('button');
                    btn.className = config.class;
                    btn.textContent = config.text;
                    if (config.style) btn.style.display = config.style;
                    btn.dataset.client = clientName;
                    btn.dataset.type = config.type;
                    buttonsDiv.appendChild(btn);
                });

                section.appendChild(buttonsDiv);

                const table = document.createElement('table');
                table.className = 'freteTable';
                table.dataset.client = clientName;

                const thead = document.createElement('thead');
                const headerRow = document.createElement('tr');
                clientData.columnHeaders.forEach(header => {
                    const th = document.createElement('th');
                    th.textContent = header;
                    headerRow.appendChild(th);
                });
                // Coluna para deletar linha
                const deleteHeader = document.createElement('th');
                deleteHeader.textContent = 'Ações';
                headerRow.appendChild(deleteHeader);
                thead.appendChild(headerRow);
                table.appendChild(thead);

                const tbody = document.createElement('tbody');
                clientData.rows.forEach((row, rowIndex) => {
                    const tr = document.createElement('tr');
                    tr.dataset.rowIndex = rowIndex;

                    clientData.columnKeys.forEach(key => {
                        const td = document.createElement('td');
                        td.className = 'editable-cell';
                        const input = document.createElement('input');
                        input.type = 'text';
                        let val = row[key];
                        if (key === 'freteAtual' || key === 'estadia') {
                            input.value = formatCurrencyValue(val);
                        } else if (key === 'adv') {
                            input.value = parseFloat(val).toFixed(2).replace('.', ',');
                        } else {
                            input.value = val || '';
                        }
                        input.disabled = true;
                        td.appendChild(input);
                        tr.appendChild(td);
                    });

                    // Botão deletar linha
                    const actionTd = document.createElement('td');
                    const deleteBtn = document.createElement('button');
                    deleteBtn.textContent = 'X';
                    deleteBtn.className = 'delete-row-btn';
                    deleteBtn.dataset.client = clientName;
                    deleteBtn.dataset.rowIndex = rowIndex;
                    actionTd.appendChild(deleteBtn);
                    tr.appendChild(actionTd);

                    tbody.appendChild(tr);
                });

                table.appendChild(tbody);
                section.appendChild(table);

                // Adicionar listeners para botões deste cliente
                buttonsDiv.querySelectorAll('button').forEach(btn => {
                    btn.addEventListener('click', (e) => {
                        const type = e.target.dataset.type;
                        const cName = e.target.dataset.client;
                        switch (type) {
                            case 'edit': enableFreteEditing(cName); break;
                            case 'save': saveFreteValues(cName); break;
                            case 'cancel': cancelFreteEditing(cName); break;
                            case 'reset': resetClientFrete(cName); break;
                            case 'addRow': addFreteRow(cName); break;
                            case 'addColumn': addFreteColumn(cName); break;
                            case 'deleteColumn': deleteFreteColumn(cName); break;
                            case 'deleteClient': deleteClient(cName); break;
                        }
                    });
                });

                // Listeners para deletar linhas
                table.querySelectorAll('.delete-row-btn').forEach(btn => {
                    btn.addEventListener('click', (e) => {
                        const cName = e.target.dataset.client;
                        const rIndex = parseInt(e.target.dataset.rowIndex);
                        deleteFreteRow(cName, rIndex);
                    });
                });

                return section;
            }

            function enableFreteEditing(clientName) {
                const table = document.querySelector(`table[data-client="${clientName}"]`);
                const inputs = table.querySelectorAll('input:not(.delete-row-btn)');
                inputs.forEach(input => {
                    input.disabled = false;
                    input.parentElement.classList.add('editing');
                });

                const buttonsDiv = document.querySelector(`.client-section[data-client="${clientName}"] .edit-buttons`);
                buttonsDiv.querySelector('[data-type="edit"]').style.display = 'none';
                buttonsDiv.querySelector('[data-type="save"]').style.display = 'inline-block';
                buttonsDiv.querySelector('[data-type="cancel"]').style.display = 'inline-block';
            }

            function saveFreteValues(clientName) {
                const table = document.querySelector(`table[data-client="${clientName}"]`);
                const tbody = table.querySelector('tbody');
                const rows = tbody.querySelectorAll('tr');
                const clientData = freteClients[clientName];
                clientData.rows = [];

                rows.forEach(tr => {
                    const rowData = {};
                    const cells = tr.querySelectorAll('td:not(:last-child)');
                    clientData.columnKeys.forEach((key, colIndex) => {
                        const input = cells[colIndex].querySelector('input');
                        let val = input.value.trim();
                        if (key === 'freteAtual' || key === 'estadia' || key === 'adv') {
                            val = parseFloat(val.replace(',', '.')) || 0;
                        }
                        rowData[key] = val;
                        // Atualizar input para exibição
                        if (key === 'freteAtual' || key === 'estadia') {
                            input.value = formatCurrencyValue(val);
                        } else if (key === 'adv') {
                            input.value = val.toFixed(2).replace('.', ',');
                        }
                    });

                    // Adicionar apenas se não vazia
                    if (clientData.columnKeys.some(key => rowData[key] !== '' && rowData[key] != 0)) {
                        clientData.rows.push(rowData);
                    }
                });

                syncFreteData();
                populateFreightTables();
                popularClientes();
                alert('Valores salvos com sucesso!');
            }

            function cancelFreteEditing(clientName) {
                populateFreightTables();
            }

            function resetClientFrete(clientName) {
                if (confirm('Restaurar para padrão vazio?')) {
                    freteClients[clientName] = {
                        columnKeys: ['origem', 'destino', 'tipo', 'capacidade', 'freteAtual', 'estadia', 'adv'],
                        columnHeaders: ['Origem', 'Destino', 'Veículo', 'Capacidade', 'Frete Atual', 'Estadia', 'ADV (%)'],
                        rows: [{
                            origem: '', destino: '', tipo: '', capacidade: '', freteAtual: 0, estadia: 0, adv: 0.1
                        }]
                    };
                    syncFreteData();
                    populateFreightTables();
                    popularClientes();
                    alert('Restaurado!');
                }
            }

            function addFreteRow(clientName) {
                const clientData = freteClients[clientName];
                const emptyRow = {
                    origem: '', destino: '', tipo: '', capacidade: '', freteAtual: 0, estadia: 0, adv: 0.1
                };
                clientData.rows.push(emptyRow);
                syncFreteData();
                populateFreightTables();
            }

            function addFreteColumn(clientName) {
                const newHeader = prompt('Nome da nova coluna:');
                if (!newHeader || newHeader.trim() === '') return;
                const newKey = newHeader.toLowerCase().replace(/\s+/g, '_').replace(/[^a-z0-9_]/g, '');
                const clientData = freteClients[clientName];
                clientData.columnHeaders.push(newHeader.trim());
                clientData.columnKeys.push(newKey);
                clientData.rows.forEach(row => {
                    row[newKey] = '';
                });
                syncFreteData();
                populateFreightTables();
                alert('Coluna adicionada!');
            }

            function deleteFreteColumn(clientName) {
                const clientData = freteClients[clientName];
                const colIndexStr = prompt(`Índice da coluna a deletar (0 a ${clientData.columnHeaders.length - 1}):`);
                const colIndex = parseInt(colIndexStr);
                if (isNaN(colIndex) || colIndex < 0 || colIndex >= clientData.columnHeaders.length) {
                    alert('Índice inválido!');
                    return;
                }
                const colToDelete = clientData.columnHeaders[colIndex];
                if (!confirm(`Deletar coluna "${colToDelete}"?`)) return;
                const keyToDelete = clientData.columnKeys[colIndex];
                clientData.columnKeys.splice(colIndex, 1);
                clientData.columnHeaders.splice(colIndex, 1);
                clientData.rows.forEach(row => delete row[keyToDelete]);
                syncFreteData();
                populateFreightTables();
                alert('Coluna deletada!');
            }

            function deleteFreteRow(clientName, rowIndex) {
                if (confirm('Deletar esta linha?')) {
                    freteClients[clientName].rows.splice(rowIndex, 1);
                    syncFreteData();
                    populateFreightTables();
                    popularClientes();
                }
            }

            function deleteClient(clientName) {
                if (confirm(`Deletar cliente "${clientName}" e sua tabela?`)) {
                    delete freteClients[clientName];
                    syncFreteData();
                    populateFreightTables();
                    popularClientes();
                    alert('Cliente deletado!');
                }
            }

            function addNewClient() {
                const nomeCliente = prompt('Nome do novo cliente:');
                if (!nomeCliente || nomeCliente.trim() === '') {
                    alert('Nome obrigatório.');
                    return;
                }
                if (freteClients[nomeCliente.trim()]) {
                    alert('Cliente já existe.');
                    return;
                }
                freteClients[nomeCliente.trim()] = {
                    columnKeys: ['origem', 'destino', 'tipo', 'capacidade', 'freteAtual', 'estadia', 'adv'],
                    columnHeaders: ['Origem', 'Destino', 'Veículo', 'Capacidade', 'Frete Atual', 'Estadia', 'ADV (%)'],
                    rows: [{
                        origem: 'Nova Origem', destino: 'Novo Destino', tipo: 'Novo Veículo', capacidade: 'Nova Capacidade', freteAtual: 0, estadia: 0, adv: 0.1
                    }]
                };
                syncFreteData();
                populateFreightTables();
                popularClientes();
                alert(`Cliente "${nomeCliente}" criado! Edite a tabela.`);
            }
            
            // Funções para seletor de frete (usando array)
            function popularClientes() {
                const selectCliente = document.getElementById('cliente-select');
                const uniqueClientes = [...new Set(freteDataArray.map(entry => entry.cliente))];
                selectCliente.innerHTML = '<option value="">Escolha um cliente...</option>';
                
                uniqueClientes.forEach(cliente => {
                    const option = document.createElement('option');
                    option.value = cliente;
                    option.textContent = cliente;
                    selectCliente.appendChild(option);
                });
            }
            
            function handleClienteChange() {
                const nomeCliente = this.value;
                const selectRota = document.getElementById('rota-select');
                const selectVeiculo = document.getElementById('veiculo-select');
                const btnPuxar = document.getElementById('puxar-frete-btn');
                
                selectRota.innerHTML = '<option value="">Escolha uma rota...</option>';
                selectVeiculo.innerHTML = '<option value="">Escolha o veículo...</option>';
                selectRota.disabled = !nomeCliente;
                selectVeiculo.disabled = true;
                btnPuxar.disabled = true;
                
                if (nomeCliente) {
                    const rotasCliente = freteDataArray
                        .filter(entry => entry.cliente === nomeCliente)
                        .map(entry => ({origem: entry.origem, destino: entry.destino}))
                        .filter((rota, index, self) => index === self.findIndex(r => r.origem === rota.origem && r.destino === rota.destino));
                    
                    rotasCliente.forEach(rota => {
                        const option = document.createElement('option');
                        option.value = JSON.stringify(rota);
                        option.textContent = `${rota.origem} x ${rota.destino}`;
                        selectRota.appendChild(option);
                    });
                }
            }
            
            function handleRotaChange() {
                const dadosRota = JSON.parse(this.value || '{}');
                const selectVeiculo = document.getElementById('veiculo-select');
                const btnPuxar = document.getElementById('puxar-frete-btn');
                const nomeCliente = document.getElementById('cliente-select').value;
                
                selectVeiculo.innerHTML = '<option value="">Escolha o veículo...</option>';
                selectVeiculo.disabled = !dadosRota.origem;
                btnPuxar.disabled = true;
                
                if (dadosRota.origem && nomeCliente) {
                    const veiculosRota = freteDataArray.filter(entry => 
                        entry.cliente === nomeCliente && 
                        entry.origem === dadosRota.origem && 
                        entry.destino === dadosRota.destino
                    );
                    
                    veiculosRota.forEach(veiculo => {
                        const option = document.createElement('option');
                        option.value = JSON.stringify({tipo: veiculo.tipo, frete: veiculo.freteAtual, adv: veiculo.adv});
                        option.textContent = `${veiculo.tipo} (${veiculo.capacidade}) - ADV: ${(veiculo.adv * 100).toFixed(2)}%`;
                        selectVeiculo.appendChild(option);
                    });
                }
            }
            
            function handleVeiculoChange() {
                document.getElementById('puxar-frete-btn').disabled = !this.value;
            }
            
            window.puxarFrete = function() {
                const dadosVeiculoStr = document.getElementById('veiculo-select').value;
                const dadosVeiculo = JSON.parse(dadosVeiculoStr || '{}');
                if (!dadosVeiculo.frete) return;
                
                const freteValue = dadosVeiculo.frete.toFixed(2).replace('.', ',');
                freteValueInput.value = freteValue;
                saveData('freteValue', freteValue);
                
                // Puxar ADV para Advalorem
                const advPercent = (dadosVeiculo.adv * 100).toFixed(2).replace('.', ',');
                advaloremPercentInput.value = advPercent;
                saveData('advaloremPercent', advPercent);
                document.getElementById('advaloremPercentDisplay').textContent = advPercent;
                
                calculateFrete();
                calculateTribut();
                
                document.getElementById('info-frete').textContent = `Frete base puxado: R$ ${dadosVeiculo.frete.toFixed(2)} | ADV puxado: ${advPercent}% (${dadosVeiculo.tipo})`;
                document.getElementById('puxar-frete-btn').disabled = true;
            };
            
            // Funções para tributos e frete (mantidas iguais)
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
                // Re-aplicar classes editing se necessário
                document.querySelectorAll('.editing input').forEach(input => {
                    input.style.backgroundColor = newTheme === 'dark' ? '#444' : 'white';
                    input.style.color = newTheme === 'dark' ? '#fff' : 'black';
                });
            }
            
            function updateThemeToggle(theme) {
                const toggle = document.getElementById('themeToggle');
                toggle.textContent = theme === 'dark' ? '☀️' : '🌙';
                toggle.title = theme === 'dark' ? 'Modo claro' : 'Modo escuro';
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
