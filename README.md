
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DataUnify - Sistema de Unificação de Dados</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #2563eb;
            --primary-dark: #1d4ed8;
            --secondary: #1e293b;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
            --light: #f8fafc;
            --dark: #0f172a;
            --gray: #64748b;
            --border: #e2e8f0;
        }

        body {
            font-family: 'Segoe UI', system-ui, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: var(--dark);
            line-height: 1.6;
        }

        .app-container {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        /* Header */
        .header {
            background: var(--secondary);
            color: white;
            padding: 1rem 2rem;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            font-size: 1.5rem;
            font-weight: 700;
        }

        .user-menu {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        /* Main Layout */
        .main-layout {
            display: flex;
            flex: 1;
        }

        /* Sidebar */
        .sidebar {
            width: 250px;
            background: white;
            border-right: 1px solid var(--border);
            padding: 1.5rem 0;
        }

        .nav-item {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            padding: 0.75rem 1.5rem;
            color: var(--gray);
            text-decoration: none;
            transition: all 0.2s;
            border-left: 3px solid transparent;
        }

        .nav-item:hover, .nav-item.active {
            background: var(--light);
            color: var(--primary);
            border-left-color: var(--primary);
        }

        .nav-item.active {
            font-weight: 600;
        }

        /* Main Content */
        .main-content {
            flex: 1;
            padding: 2rem;
            background: var(--light);
            overflow-y: auto;
        }

        /* Dashboard Grid */
        .dashboard {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2rem;
        }

        .stat-card {
            background: white;
            padding: 1.5rem;
            border-radius: 12px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            border-left: 4px solid var(--primary);
        }

        .stat-number {
            font-size: 2.5rem;
            font-weight: 700;
            color: var(--primary);
            display: block;
            line-height: 1;
        }

        .stat-label {
            color: var(--gray);
            font-size: 0.9rem;
            margin-top: 0.5rem;
        }

        /* Modules Grid */
        .modules-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2rem;
        }

        .module-card {
            background: white;
            border-radius: 12px;
            padding: 1.5rem;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            border: 1px solid var(--border);
            transition: all 0.3s ease;
        }

        .module-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 15px rgba(0,0,0,0.1);
        }

        .module-card h3 {
            color: var(--secondary);
            margin-bottom: 0.5rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .module-card p {
            color: var(--gray);
            margin-bottom: 1rem;
            font-size: 0.9rem;
        }

        /* Buttons */
        .btn {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            padding: 0.75rem 1.5rem;
            border: none;
            border-radius: 8px;
            font-size: 0.9rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            text-decoration: none;
        }

        .btn-primary {
            background: var(--primary);
            color: white;
        }

        .btn-primary:hover {
            background: var(--primary-dark);
            transform: translateY(-1px);
        }

        .btn-success {
            background: var(--success);
            color: white;
        }

        .btn-warning {
            background: var(--warning);
            color: white;
        }

        .btn-danger {
            background: var(--danger);
            color: white;
        }

        .btn-outline {
            background: transparent;
            border: 2px solid var(--primary);
            color: var(--primary);
        }

        /* Data Table */
        .data-section {
            background: white;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            margin-bottom: 2rem;
        }

        .section-header {
            background: var(--secondary);
            color: white;
            padding: 1.5rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .search-box {
            background: white;
            padding: 1rem;
            border-bottom: 1px solid var(--border);
            display: flex;
            gap: 1rem;
        }

        .search-input {
            flex: 1;
            padding: 0.75rem;
            border: 1px solid var(--border);
            border-radius: 6px;
            font-size: 1rem;
        }

        .table-container {
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        th, td {
            padding: 1rem;
            text-align: left;
            border-bottom: 1px solid var(--border);
        }

        th {
            background: var(--light);
            font-weight: 600;
            color: var(--secondary);
            position: sticky;
            top: 0;
        }

        tr:hover {
            background: var(--light);
        }

        .status-badge {
            padding: 0.25rem 0.75rem;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 500;
        }

        .status-active {
            background: #d1fae5;
            color: #065f46;
        }

        .status-pending {
            background: #fef3c7;
            color: #92400e;
        }

        .status-inactive {
            background: #f1f5f9;
            color: #475569;
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }

        .modal-content {
            background: white;
            border-radius: 12px;
            padding: 2rem;
            max-width: 500px;
            width: 100%;
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }

        .close-btn {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--gray);
        }

        /* Forms */
        .form-group {
            margin-bottom: 1rem;
        }

        .form-label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
            color: var(--secondary);
        }

        .form-control {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid var(--border);
            border-radius: 6px;
            font-size: 1rem;
            transition: border-color 0.2s;
        }

        .form-control:focus {
            outline: none;
            border-color: var(--primary);
        }

        /* Footer */
        .footer {
            background: var(--secondary);
            color: white;
            text-align: center;
            padding: 1.5rem;
            margin-top: auto;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .main-layout {
                flex-direction: column;
            }
            
            .sidebar {
                width: 100%;
                order: 2;
            }
            
            .main-content {
                order: 1;
            }
            
            .dashboard {
                grid-template-columns: 1fr;
            }
            
            .modules-grid {
                grid-template-columns: 1fr;
            }
            
            .section-header {
                flex-direction: column;
                gap: 1rem;
                align-items: stretch;
            }
        }

        /* Loading */
        .loading {
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 2rem;
            color: var(--gray);
        }

        /* Export Options */
        .export-options {
            display: flex;
            gap: 0.5rem;
            flex-wrap: wrap;
        }
    </style>
</head>
<body>
    <div class="app-container">
        <!-- Header -->
        <header class="header">
            <div class="logo">
                <span>🏢</span>
                <span>DataUnify</span>
            </div>
            <div class="user-menu">
                <span>👤 Administrador</span>
            </div>
        </header>

        <!-- Main Layout -->
        <div class="main-layout">
            <!-- Sidebar -->
            <nav class="sidebar">
                <a href="#" class="nav-item active">
                    <span>📊</span>
                    <span>Dashboard</span>
                </a>
                <a href="#" class="nav-item">
                    <span>👥</span>
                    <span>Funcionários</span>
                </a>
                <a href="#" class="nav-item">
                    <span>🏢</span>
                    <span>Empresas</span>
                </a>
                <a href="#" class="nav-item">
                    <span>📋</span>
                    <span>Projetos</span>
                </a>
                <a href="#" class="nav-item">
                    <span>💰</span>
                    <span>Financeiro</span>
                </a>
                <a href="#" class="nav-item">
                    <span>📈</span>
                    <span>Relatórios</span>
                </a>
                <a href="#" class="nav-item">
                    <span>⚙️</span>
                    <span>Configurações</span>
                </a>
            </nav>

            <!-- Main Content -->
            <main class="main-content">
                <!-- Dashboard -->
                <section>
                    <h1 style="margin-bottom: 1.5rem; color: var(--secondary);">Dashboard de Unificação</h1>
                    
                    <div class="dashboard">
                        <div class="stat-card">
                            <span class="stat-number" id="totalCompanies">0</span>
                            <span class="stat-label">Empresas Unificadas</span>
                        </div>
                        <div class="stat-card">
                            <span class="stat-number" id="totalEmployees">0</span>
                            <span class="stat-label">Funcionários</span>
                        </div>
                        <div class="stat-card">
                            <span class="stat-number" id="totalProjects">0</span>
                            <span class="stat-label">Projetos Ativos</span>
                        </div>
                        <div class="stat-card">
                            <span class="stat-number" id="dataAccuracy">0%</span>
                            <span class="stat-label">Precisão dos Dados</span>
                        </div>
                    </div>
                </section>

                <!-- Quick Actions -->
                <section style="margin-bottom: 2rem;">
                    <h2 style="margin-bottom: 1rem; color: var(--secondary);">Ações Rápidas</h2>
                    <div class="modules-grid">
                        <div class="module-card">
                            <h3>👥 Adicionar Funcionário</h3>
                            <p>Cadastre novos colaboradores no sistema unificado</p>
                            <button class="btn btn-primary" onclick="openModal('employee')">
                                ➕ Novo Funcionário
                            </button>
                        </div>
                        <div class="module-card">
                            <h3>🏢 Cadastrar Empresa</h3>
                            <p>Adicione uma nova empresa ao sistema de gestão</p>
                            <button class="btn btn-primary" onclick="openModal('company')">
                                ➕ Nova Empresa
                            </button>
                        </div>
                        <div class="module-card">
                            <h3>📊 Gerar Relatório</h3>
                            <p>Crie relatórios unificados de todos os dados</p>
                            <button class="btn btn-success" onclick="generateReport()">
                                📈 Gerar Relatório
                            </button>
                        </div>
                    </div>
                </section>

                <!-- Unified Data Table -->
                <section class="data-section">
                    <div class="section-header">
                        <h2 style="color: white;">📋 Dados Unificados</h2>
                        <div class="export-options">
                            <button class="btn btn-success" onclick="exportData('csv')">
                                📥 Exportar CSV
                            </button>
                            <button class="btn btn-warning" onclick="exportData('json')">
                                📥 Exportar JSON
                            </button>
                        </div>
                    </div>
                    
                    <div class="search-box">
                        <input type="text" class="search-input" id="searchInput" 
                               placeholder="🔍 Buscar em todos os dados..." 
                               onkeyup="filterData()">
                        <button class="btn btn-outline" onclick="clearFilters()">
                            🗑️ Limpar Filtros
                        </button>
                    </div>

                    <div class="table-container">
                        <table>
                            <thead>
                                <tr>
                                    <th>ID</th>
                                    <th>Tipo</th>
                                    <th>Nome</th>
                                    <th>Departamento</th>
                                    <th>Status</th>
                                    <th>Última Atualização</th>
                                    <th>Ações</th>
                                </tr>
                            </thead>
                            <tbody id="dataTableBody">
                                <!-- Dados serão carregados aqui -->
                            </tbody>
                        </table>
                    </div>
                </section>
            </main>
        </div>

        <!-- Footer -->
        <footer class="footer">
            <p>DataUnify &copy; 2024 - Sistema de Unificação de Dados Empresariais</p>
        </footer>
    </div>

    <!-- Modal para Adicionar Funcionário -->
    <div id="employeeModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>👥 Adicionar Funcionário</h3>
                <button class="close-btn" onclick="closeModal('employee')">×</button>
            </div>
            <form id="employeeForm" onsubmit="saveEmployee(event)">
                <div class="form-group">
                    <label class="form-label">Nome Completo</label>
                    <input type="text" class="form-control" name="name" required>
                </div>
                <div class="form-group">
                    <label class="form-label">Email</label>
                    <input type="email" class="form-control" name="email" required>
                </div>
                <div class="form-group">
                    <label class="form-label">Cargo</label>
                    <input type="text" class="form-control" name="position" required>
                </div>
                <div class="form-group">
                    <label class="form-label">Departamento</label>
                    <select class="form-control" name="department" required>
                        <option value="">Selecione...</option>
                        <option value="TI">Tecnologia da Informação</option>
                        <option value="RH">Recursos Humanos</option>
                        <option value="Financeiro">Financeiro</option>
                        <option value="Marketing">Marketing</option>
                        <option value="Vendas">Vendas</option>
                    </select>
                </div>
                <div class="form-group">
                    <label class="form-label">Salário</label>
                    <input type="number" class="form-control" name="salary" step="0.01" required>
                </div>
                <button type="submit" class="btn btn-success" style="width: 100%;">
                    💾 Salvar Funcionário
                </button>
            </form>
        </div>
    </div>

    <!-- Modal para Adicionar Empresa -->
    <div id="companyModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>🏢 Cadastrar Empresa</h3>
                <button class="close-btn" onclick="closeModal('company')">×</button>
            </div>
            <form id="companyForm" onsubmit="saveCompany(event)">
                <div class="form-group">
                    <label class="form-label">Nome da Empresa</label>
                    <input type="text" class="form-control" name="name" required>
                </div>
                <div class="form-group">
                    <label class="form-label">CNPJ</label>
                    <input type="text" class="form-control" name="cnpj" required>
                </div>
                <div class="form-group">
                    <label class="form-label">Segmento</label>
                    <select class="form-control" name="segment" required>
                        <option value="">Selecione...</option>
                        <option value="Tecnologia">Tecnologia</option>
                        <option value="Comércio">Comércio</option>
                        <option value="Indústria">