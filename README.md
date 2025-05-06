
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Conection Acessórios - Sistema de Cobrança</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/signature_pad/1.5.3/signature_pad.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/html2canvas@1.4.1/dist/html2canvas.min.js"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" rel="stylesheet">
    
    <!-- Firebase App (core Firebase SDK) -->
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <!-- Firebase Auth -->
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-auth-compat.js"></script>
    <!-- Firebase Database -->
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        primary: '#5D5CDE',
                        secondary: '#3D3DC3',
                        accent: '#FF7A00',
                    },
                    fontFamily: {
                        title: ['Georgia', 'serif'],
                        sans: ['Inter', 'sans-serif']
                    }
                }
            }
        }
    </script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&display=swap');
        
        .font-title {
            font-family: 'Playfair Display', serif;
        }
        
        .bg-pattern {
            background-image: url('data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSI1IiBoZWlnaHQ9IjUiPgo8cmVjdCB3aWR0aD0iNSIgaGVpZ2h0PSI1IiBmaWxsPSIjZmZmIj48L3JlY3Q+CjxyZWN0IHdpZHRoPSIxIiBoZWlnaHQ9IjEiIGZpbGw9IiNmNWY1ZjUiPjwvcmVjdD4KPC9zdmc+');
        }
        
        .signature-pad {
            border: 1px solid #ccc;
            border-radius: 0.5rem;
            width: 100%;
            height: 200px;
        }
        
        .dark .signature-pad {
            border-color: #555;
            background-color: #333;
        }
        
        body {
            min-height: 100vh;
            background: linear-gradient(rgba(255, 255, 255, 0.95), rgba(255, 255, 255, 0.95)), url('data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA4MDAgODAwIj48ZyBvcGFjaXR5PSIwLjA1Ij48cGF0aCBkPSJNNDAwIDIwMGMtNTUuMjI4IDAtMTAwIDQ0Ljc3Mi0xMDAgMTAwczQ0Ljc3MiAxMDAgMTAwIDEwMCAxMDAtNDQuNzcyIDEwMC0xMDAtNDQuNzcyLTEwMC0xMDAtMTAwem0wIDE3MGMtMzguNjYgMC03MC0zMS4zNC03MC03MHMzMS4zNC03MCA3MC03MCA3MCAzMS4zNCA3MCA3MC0zMS4zNCA3MC03MCA3MHoiLz48cGF0aCBkPSJNNjMwIDIwMGMtNTUuMjI4IDAtMTAwIDQ0Ljc3Mi0xMDAgMTAwczQ0Ljc3MiAxMDAgMTAwIDEwMCAxMDAtNDQuNzcyIDEwMC0xMDAtNDQuNzcyLTEwMC0xMDAtMTAwem0wIDE3MGMtMzguNjYgMC03MC0zMS4zNC03MC03MHMzMS4zNC03MCA3MC03MCA3MCAzMS4zNCA3MCA3MC0zMS4zNCA3MCA3MCA3MHoiLz48cGF0aCBkPSJNMTcwIDIwMGMtNTUuMjI4IDAtMTAwIDQ0Ljc3Mi0xMDAgMTAwczQ0Ljc3MiAxMDAgMTAwIDEwMCAxMDAtNDQuNzcyIDEwMC0xMDAtNDQuNzcyLTEwMC0xMDAtMTAwem0wIDE3MGMtMzguNjYgMC03MC0zMS4zNC03MC03MHMzMS4zNC03MCA3MC03MCA3MCAzMS4zNCA3MCA3MC0zMS4zNCA3MCA3MCA3MHoiLz48cGF0aCBkPSJNNDAwIDQzMGMtNTUuMjI4IDAtMTAwIDQ0Ljc3Mi0xMDAgMTAwczQ0Ljc3MiAxMDAgMTAwIDEwMCAxMDAtNDQuNzcyIDEwMC0xMDAtNDQuNzcyLTEwMC0xMDAtMTAwem0wIDE3MGMtMzguNjYgMC03MC0zMS4zNC03MC03MHMzMS4zNC03MCA3MC03MCA3MCAzMS4zNCA3MCA3MC0zMS4zNCA3MCA3MCA3MHoiLz48cGF0aCBkPSJNMTcwIDQzMGMtNTUuMjI4IDAtMTAwIDQ0Ljc3Mi0xMDAgMTAwczQ0Ljc3MiAxMDAgMTAwIDEwMCAxMDAtNDQuNzcyIDEwMC0xMDAtNDQuNzcyLTEwMC0xMDAtMTAwem0wIDE3MGMtMzguNjYgMC03MC0zMS4zNC03MC03MHMzMS4zNC03MCA3MC03MCA3MCAzMS4zNCA3MCA3MC0zMS4zNCA3MCA3MCA3MHoiLz48cGF0aCBkPSJNNjMwIDQzMGMtNTUuMjI4IDAtMTAwIDQ0Ljc3Mi0xMDAgMTAwczQ0Ljc3MiAxMDAgMTAwIDEwMCAxMDAtNDQuNzcyIDEwMC0xMDAtNDQuNzcyLTEwMC0xMDAtMTAwem0wIDE3MGMtMzguNjYgMC03MC0zMS4zNC03MC03MHMzMS4zNC03MCA3MC03MCA3MCAzMS4zNCA3MCA3MC0zMS4zNCA3MCA3MCA3MHoiLz48L2c+PC9zdmc+');
            background-size: cover;
        }
        
        .dark body {
            background: linear-gradient(rgba(24, 24, 24, 0.95), rgba(24, 24, 24, 0.95)), url('data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA4MDAgODAwIj48ZyBvcGFjaXR5PSIwLjA1Ij48cGF0aCBkPSJNNDAwIDIwMGMtNTUuMjI4IDAtMTAwIDQ0Ljc3Mi0xMDAgMTAwczQ0Ljc3MiAxMDAgMTAwIDEwMCAxMDAtNDQuNzcyIDEwMC0xMDAtNDQuNzcyLTEwMC0xMDAtMTAwem0wIDE3MGMtMzguNjYgMC03MC0zMS4zNC03MC03MHMzMS4zNC03MCA3MC03MCA3MCAzMS4zNCA3MCA3MC0zMS4zNCA3MCA3MCA3MHoiLz48cGF0aCBkPSJNNjMwIDIwMGMtNTUuMjI4IDAtMTAwIDQ0Ljc3Mi0xMDAgMTAwczQ0Ljc3MiAxMDAgMTAwIDEwMCAxMDAtNDQuNzcyIDEwMC0xMDAtNDQuNzcyLTEwMC0xMDAtMTAwem0wIDE3MGMtMzguNjYgMC03MC0zMS4zNC03MC03MHMzMS4zNC03MCA3MC03MCA3MCAzMS4zNCA3MCA3MC0zMS4zNCA3MCA3MCA3MHoiLz48cGF0aCBkPSJNMTcwIDIwMGMtNTUuMjI4IDAtMTAwIDQ0Ljc3Mi0xMDAgMTAwczQ0Ljc3MiAxMDAgMTAwIDEwMCAxMDAtNDQuNzcyIDEwMC0xMDAtNDQuNzcyLTEwMC0xMDAtMTAwem0wIDE3MGMtMzguNjYgMC03MC0zMS4zNC03MC03MHMzMS4zNC03MCA3MC03MCA3MCAzMS4zNCA3MCA3MC0zMS4zNCA3MCA3MCA3MHoiLz48cGF0aCBkPSJNNDAwIDQzMGMtNTUuMjI4IDAtMTAwIDQ0Ljc3Mi0xMDAgMTAwczQ0Ljc3MiAxMDAgMTAwIDEwMCAxMDAtNDQuNzcyIDEwMC0xMDAtNDQuNzcyLTEwMC0xMDAtMTAwem0wIDE3MGMtMzguNjYgMC03MC0zMS4zNC03MC03MHMzMS4zNC03MCA3MC03MCA3MCAzMS4zNCA3MCA3MC0zMS4zNCA3MCA3MCA3MHoiLz48cGF0aCBkPSJNMTcwIDQzMGMtNTUuMjI4IDAtMTAwIDQ0Ljc3Mi0xMDAgMTAwczQ0Ljc3MiAxMDAgMTAwIDEwMCAxMDAtNDQuNzcyIDEwMC0xMDAtNDQuNzcyLTEwMC0xMDAtMTAwem0wIDE3MGMtMzguNjYgMC03MC0zMS4zNC03MC03MHMzMS4zNC03MCA3MC03MCA3MCAzMS4zNCA3MCA3MC0zMS4zNCA3MCA3MCA3MHoiLz48cGF0aCBkPSJNNjMwIDQzMGMtNTUuMjI4IDAtMTAwIDQ0Ljc3Mi0xMDAgMTAwczQ0Ljc3MiAxMDAgMTAwIDEwMCAxMDAtNDQuNzcyIDEwMC0xMDAtNDQuNzcyLTEwMC0xMDAtMTAwem0wIDE3MGMtMzguNjYgMC03MC0zMS4zNC03MC03MHMzMS4zNC03MCA3MC03MCA3MCAzMS4zNCA3MCA3MC0zMS4zNCA3MCA3MCA3MHoiLz48L2c+PC9zdmc+');
        }

        /* Loading spinner */
        .loader {
            border: 3px solid rgba(0, 0, 0, 0.1);
            border-radius: 50%;
            border-top: 3px solid #5D5CDE;
            width: 24px;
            height: 24px;
            animation: spin 1s linear infinite;
            margin: 0 auto;
        }

        .dark .loader {
            border-color: rgba(255, 255, 255, 0.1);
            border-top-color: #5D5CDE;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Toast notifications */
        .toast {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 12px 20px;
            border-radius: 4px;
            z-index: 100;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            animation: slideIn 0.3s ease-out, fadeOut 0.5s ease-out 4s forwards;
            max-width: 350px;
        }

        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        @keyframes fadeOut {
            from { opacity: 1; }
            to { opacity: 0; visibility: hidden; }
        }
    </style>
</head>
<body class="bg-white dark:bg-gray-900 text-gray-800 dark:text-gray-200">
    <div id="toast-container"></div>

    <div id="loading-overlay" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
        <div class="bg-white dark:bg-gray-800 p-6 rounded-lg shadow-xl text-center">
            <div class="loader mb-4"></div>
            <p class="text-lg">Carregando sistema...</p>
        </div>
    </div>

    <header class="bg-white dark:bg-gray-800 shadow-md py-2 px-4 flex justify-between items-center sticky top-0 z-30">
        <div class="text-xs text-gray-500 dark:text-gray-400">
            Moura Tech Soluções em Tecnologia
        </div>
        <h1 class="text-3xl text-center font-title text-primary dark:text-primary font-bold">
            Conection Acessórios
        </h1>
        <div class="flex gap-2">
            <button id="syncBtn" class="p-2 rounded-full hover:bg-gray-200 dark:hover:bg-gray-700 relative">
                <i class="fas fa-sync"></i>
                <span id="sync-status" class="absolute top-0 right-0 h-3 w-3 rounded-full bg-green-500 hidden"></span>
            </button>
            <button id="darkModeToggle" class="p-2 rounded-full hover:bg-gray-200 dark:hover:bg-gray-700">
                <i class="fas fa-moon dark:hidden"></i>
                <i class="fas fa-sun hidden dark:block"></i>
            </button>
        </div>
    </header>

    <nav class="bg-white dark:bg-gray-800 shadow-md p-2 flex justify-center space-x-2 overflow-x-auto">
        <button data-target="venda" class="tab-btn px-4 py-2 rounded-md bg-primary text-white font-medium">
            <i class="fas fa-receipt mr-1"></i> Venda/Cobrança
        </button>
        <button data-target="clientes" class="tab-btn px-4 py-2 rounded-md hover:bg-gray-200 dark:hover:bg-gray-700 font-medium">
            <i class="fas fa-users mr-1"></i> Clientes
        </button>
        <button data-target="caixa" class="tab-btn px-4 py-2 rounded-md hover:bg-gray-200 dark:hover:bg-gray-700 font-medium">
            <i class="fas fa-cash-register mr-1"></i> Caixa
        </button>
        <button data-target="produtos" class="tab-btn px-4 py-2 rounded-md hover:bg-gray-200 dark:hover:bg-gray-700 font-medium">
            <i class="fas fa-box mr-1"></i> Produtos
        </button>
    </nav>

    <main class="container mx-auto p-4 max-w-5xl">
        <!-- Tela de Venda/Cobrança -->
        <section id="venda" class="tab-content">
            <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-4 mb-6">
                <h2 class="text-xl font-semibold mb-4">Selecionar Cliente</h2>
                
                <div class="mb-4 flex flex-col md:flex-row gap-2">
                    <div class="flex-grow">
                        <div class="relative">
                            <input type="text" id="clienteSearch" placeholder="Buscar cliente..." 
                                class="w-full px-4 py-2 rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-700 text-base">
                            <div class="absolute right-2 top-2 text-gray-400">
                                <i class="fas fa-search"></i>
                            </div>
                        </div>
                        <div id="clientesDropdown" class="hidden absolute z-10 bg-white dark:bg-gray-700 border border-gray-300 dark:border-gray-600 rounded-md mt-1 max-h-60 overflow-y-auto w-64 shadow-lg">
                            <!-- Clientes serão adicionados aqui dinamicamente -->
                        </div>
                    </div>
                    <button id="novoClienteBtn" class="bg-accent hover:bg-amber-500 text-white px-4 py-2 rounded-md">
                        <i class="fas fa-user-plus mr-1"></i> Novo Cliente
                    </button>
                </div>
                
                <div id="clienteSelecionado" class="hidden bg-gray-100 dark:bg-gray-700 p-3 rounded-md mb-4">
                    <h3 class="font-bold text-lg" id="clienteNome">Nome do Cliente</h3>
                    <p class="text-sm" id="clienteDetalhes">CPF/CNPJ: 000.000.000-00</p>
                    <p class="text-sm" id="clienteContato">Telefone: (00) 00000-0000</p>
                    <div class="mt-2">
                        <button id="verHistoricoBtn" class="text-sm text-primary hover:underline">
                            <i class="fas fa-history mr-1"></i> Ver Histórico de Cobrança
                        </button>
                    </div>
                </div>
            </div>

            <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-4 mb-6">
                <h2 class="text-xl font-semibold mb-4">Itens da Venda</h2>
                
                <div class="overflow-x-auto">
                    <table class="w-full text-left">
                        <thead class="bg-gray-100 dark:bg-gray-700">
                            <tr>
                                <th class="px-4 py-2 rounded-l-md">Produto</th>
                                <th class="px-4 py-2 text-center">Preço Unit.</th>
                                <th class="px-4 py-2 text-center">Qtd</th>
                                <th class="px-4 py-2 text-center">Subtotal</th>
                                <th class="px-4 py-2 rounded-r-md text-center">Ações</th>
                            </tr>
                        </thead>
                        <tbody id="itensVenda">
                            <!-- Produtos serão adicionados aqui -->
                        </tbody>
                    </table>
                </div>
                
                <div class="flex justify-between items-center mt-4">
                    <div>
                        <select id="produtoSelect" class="px-4 py-2 rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-700 text-base">
                            <option value="" disabled selected>Selecione um produto</option>
                            <!-- Produtos serão carregados do Firebase -->
                        </select>
                        <button id="adicionarProdutoBtn" class="ml-2 bg-primary hover:bg-secondary text-white px-4 py-2 rounded-md">
                            <i class="fas fa-plus mr-1"></i> Adicionar
                        </button>
                    </div>
                    <div class="text-right">
                        <p class="text-lg mb-1">Total: <span id="totalVenda" class="font-bold">R$ 0,00</span></p>
                    </div>
                </div>
            </div>
            
            <div class="flex justify-end gap-2 mb-6">
                <button id="limparVendaBtn" class="px-4 py-2 bg-gray-300 dark:bg-gray-700 hover:bg-gray-400 dark:hover:bg-gray-600 rounded-md">
                    <i class="fas fa-trash mr-1"></i> Limpar
                </button>
                <button id="finalizarVendaBtn" class="px-4 py-2 bg-green-600 hover:bg-green-700 text-white rounded-md">
                    <i class="fas fa-check mr-1"></i> Finalizar Venda
                </button>
            </div>
        </section>

        <!-- Tela de Clientes -->
        <section id="clientes" class="tab-content hidden">
            <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-4 mb-6">
                <div class="flex justify-between items-center mb-4">
                    <h2 class="text-xl font-semibold">Gerenciar Clientes</h2>
                    <button id="adicionarClienteBtn" class="bg-primary hover:bg-secondary text-white px-4 py-2 rounded-md">
                        <i class="fas fa-user-plus mr-1"></i> Novo Cliente
                    </button>
                </div>
                
                <div class="mb-4">
                    <input type="text" id="clienteSearchList" placeholder="Buscar clientes..." 
                        class="w-full px-4 py-2 rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-700 text-base">
                </div>
                
                <div class="overflow-x-auto">
                    <table class="w-full text-left">
                        <thead class="bg-gray-100 dark:bg-gray-700">
                            <tr>
                                <th class="px-4 py-2 rounded-l-md">Nome</th>
                                <th class="px-4 py-2">CPF/CNPJ</th>
                                <th class="px-4 py-2">Telefone</th>
                                <th class="px-4 py-2 rounded-r-md text-center">Ações</th>
                            </tr>
                        </thead>
                        <tbody id="clientesList">
                            <!-- Clientes serão adicionados aqui -->
                        </tbody>
                    </table>
                </div>
            </div>
        </section>
        
        <!-- Tela de Histórico do Cliente -->
        <section id="historicoCliente" class="tab-content hidden">
            <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-4 mb-6">
                <div class="flex justify-between items-center mb-4">
                    <div>
                        <h2 class="text-xl font-semibold">Histórico de Cobrança</h2>
                        <h3 id="historicoClienteNome" class="text-lg text-primary">Cliente: Nome do Cliente</h3>
                    </div>
                    <button id="voltarClientesBtn" class="bg-gray-300 dark:bg-gray-700 hover:bg-gray-400 dark:hover:bg-gray-600 px-4 py-2 rounded-md">
                        <i class="fas fa-arrow-left mr-1"></i> Voltar
                    </button>
                </div>
                
                <div class="overflow-x-auto">
                    <table class="w-full text-left">
                        <thead class="bg-gray-100 dark:bg-gray-700">
                            <tr>
                                <th class="px-4 py-2 rounded-l-md">Data</th>
                                <th class="px-4 py-2">Itens</th>
                                <th class="px-4 py-2 text-right">Valor</th>
                                <th class="px-4 py-2 rounded-r-md text-center">Ações</th>
                            </tr>
                        </thead>
                        <tbody id="historicoClienteList">
                            <!-- Histórico de cobranças será adicionado aqui -->
                        </tbody>
                    </table>
                </div>
                
                <div id="semHistorico" class="text-center p-8 hidden">
                    <p class="text-gray-500 dark:text-gray-400">Este cliente ainda não possui histórico de cobranças.</p>
                </div>
            </div>
        </section>

        <!-- Tela de Caixa -->
        <section id="caixa" class="tab-content hidden">
            <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-4 mb-6">
                <h2 class="text-xl font-semibold mb-4">Controle de Caixa</h2>
                
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                    <div class="bg-green-100 dark:bg-green-900 p-4 rounded-md">
                        <h3 class="text-lg font-semibold text-green-800 dark:text-green-200">Entradas</h3>
                        <p class="text-2xl font-bold text-green-600 dark:text-green-300" id="totalEntradas">R$ 0,00</p>
                    </div>
                    <div class="bg-red-100 dark:bg-red-900 p-4 rounded-md">
                        <h3 class="text-lg font-semibold text-red-800 dark:text-red-200">Saídas</h3>
                        <p class="text-2xl font-bold text-red-600 dark:text-red-300" id="totalSaidas">R$ 0,00</p>
                    </div>
                    <div class="bg-blue-100 dark:bg-blue-900 p-4 rounded-md">
                        <h3 class="text-lg font-semibold text-blue-800 dark:text-blue-200">Saldo</h3>
                        <p class="text-2xl font-bold text-blue-600 dark:text-blue-300" id="saldoCaixa">R$ 0,00</p>
                    </div>
                </div>
                
                <div class="mb-4">
                    <h3 class="text-lg font-semibold mb-2">Registrar Movimentação</h3>
                    <div class="flex flex-col md:flex-row gap-2">
                        <select id="tipoMovimentacao" class="px-4 py-2 rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-700 text-base">
                            <option value="entrada">Entrada</option>
                            <option value="saida">Saída</option>
                        </select>
                        <input type="text" id="descricaoMovimentacao" placeholder="Descrição" 
                            class="flex-grow px-4 py-2 rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-700 text-base">
                        <input type="number" id="valorMovimentacao" placeholder="Valor" 
                            class="px-4 py-2 rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-700 text-base" min="0" step="0.01">
                        <button id="registrarMovimentacaoBtn" class="bg-primary hover:bg-secondary text-white px-4 py-2 rounded-md">
                            <i class="fas fa-plus mr-1"></i> Registrar
                        </button>
                    </div>
                </div>
                
                <div>
                    <h3 class="text-lg font-semibold mb-2">Histórico de Movimentações</h3>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left">
                            <thead class="bg-gray-100 dark:bg-gray-700">
                                <tr>
                                    <th class="px-4 py-2 rounded-l-md">Data</th>
                                    <th class="px-4 py-2">Tipo</th>
                                    <th class="px-4 py-2">Descrição</th>
                                    <th class="px-4 py-2 text-right rounded-r-md">Valor</th>
                                </tr>
                            </thead>
                            <tbody id="movimentacoesList">
                                <!-- Movimentações serão adicionadas aqui -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </section>

        <!-- Tela de Produtos -->
        <section id="produtos" class="tab-content hidden">
            <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-4 mb-6">
                <div class="flex justify-between items-center mb-4">
                    <h2 class="text-xl font-semibold">Gerenciar Produtos</h2>
                    <button id="adicionarProdutoGerenciarBtn" class="bg-primary hover:bg-secondary text-white px-4 py-2 rounded-md">
                        <i class="fas fa-plus mr-1"></i> Novo Produto
                    </button>
                </div>
                
                <div class="overflow-x-auto">
                    <table class="w-full text-left">
                        <thead class="bg-gray-100 dark:bg-gray-700">
                            <tr>
                                <th class="px-4 py-2 rounded-l-md">Produto</th>
                                <th class="px-4 py-2 text-right">Preço</th>
                                <th class="px-4 py-2 text-center rounded-r-md">Ações</th>
                            </tr>
                        </thead>
                        <tbody id="produtosList">
                            <!-- Produtos serão adicionados aqui -->
                        </tbody>
                    </table>
                </div>
            </div>
        </section>
    </main>

    <!-- Modal de cadastro de cliente -->
    <div id="clienteModal" class="fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center hidden">
        <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6 w-full max-w-md mx-4">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl font-semibold" id="clienteModalTitle">Cadastrar Novo Cliente</h2>
                <button class="modal-close text-gray-500 hover:text-gray-700 dark:hover:text-gray-300">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            
            <form id="clienteForm">
                <input type="hidden" id="clienteId">
                
                <div class="mb-4">
                    <label for="nomeCliente" class="block mb-1 font-medium">Nome Completo</label>
                    <input type="text" id="nomeCliente" required 
                        class="w-full px-4 py-2 rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-700 text-base">
                </div>
                
                <div class="mb-4">
                    <label for="tipoDocumento" class="block mb-1 font-medium">Tipo de Documento</label>
                    <select id="tipoDocumento" 
                        class="w-full px-4 py-2 rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-700 text-base">
                        <option value="cpf">CPF</option>
                        <option value="cnpj">CNPJ</option>
                    </select>
                </div>
                
                <div class="mb-4">
                    <label for="numeroDocumento" class="block mb-1 font-medium">Número do Documento</label>
                    <input type="text" id="numeroDocumento" required 
                        class="w-full px-4 py-2 rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-700 text-base">
                </div>
                
                <div class="mb-4">
                    <label for="telefoneCliente" class="block mb-1 font-medium">Telefone (WhatsApp)</label>
                    <input type="text" id="telefoneCliente" required 
                        class="w-full px-4 py-2 rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-700 text-base">
                </div>
                
                <div class="mb-4">
                    <label for="enderecoCliente" class="block mb-1 font-medium">Endereço</label>
                    <input type="text" id="enderecoCliente" 
                        class="w-full px-4 py-2 rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-700 text-base">
                </div>
                
                <div class="flex justify-end gap-2">
                    <button type="button" class="modal-close px-4 py-2 bg-gray-300 dark:bg-gray-700 hover:bg-gray-400 dark:hover:bg-gray-600 rounded-md">
                        Cancelar
                    </button>
                    <button type="submit" class="px-4 py-2 bg-primary hover:bg-secondary text-white rounded-md">
                        Salvar
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal de cadastro de produto -->
    <div id="produtoModal" class="fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center hidden">
        <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6 w-full max-w-md mx-4">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl font-semibold" id="produtoModalTitle">Cadastrar Novo Produto</h2>
                <button class="modal-close text-gray-500 hover:text-gray-700 dark:hover:text-gray-300">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            
            <form id="produtoForm">
                <input type="hidden" id="produtoId">
                
                <div class="mb-4">
                    <label for="nomeProduto" class="block mb-1 font-medium">Nome do Produto</label>
                    <input type="text" id="nomeProduto" required 
                        class="w-full px-4 py-2 rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-700 text-base">
                </div>
                
                <div class="mb-4">
                    <label for="precoProduto" class="block mb-1 font-medium">Preço (R$)</label>
                    <input type="number" id="precoProduto" required min="0" step="0.01"
                        class="w-full px-4 py-2 rounded-md border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-700 text-base">
                </div>
                
                <div class="flex justify-end gap-2">
                    <button type="button" class="modal-close px-4 py-2 bg-gray-300 dark:bg-gray-700 hover:bg-gray-400 dark:hover:bg-gray-600 rounded-md">
                        Cancelar
                    </button>
                    <button type="submit" class="px-4 py-2 bg-primary hover:bg-secondary text-white rounded-md">
                        Salvar
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal de finalização de venda -->
    <div id="finalizarVendaModal" class="fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center hidden">
        <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6 w-full max-w-lg mx-4">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl font-semibold">Finalizar Venda</h2>
                <button class="modal-close text-gray-500 hover:text-gray-700 dark:hover:text-gray-300">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            
            <div class="mb-4">
                <h3 class="font-bold">Resumo da Venda</h3>
                <div id="resumoVenda" class="mt-2 border border-gray-300 dark:border-gray-600 rounded-md p-3">
                    <!-- Resumo será preenchido dinamicamente -->
                </div>
            </div>
            
            <div class="mb-4">
                <h3 class="font-bold mb-2">Assinatura do Cliente</h3>
                <div class="signature-container">
                    <canvas id="assinaturaCliente" class="signature-pad"></canvas>
                </div>
                <div class="flex justify-end mt-1">
                    <button id="limparAssinaturaBtn" class="text-sm text-primary">Limpar assinatura</button>
                </div>
            </div>
            
            <div class="flex justify-end gap-2">
                <button class="modal-close px-4 py-2 bg-gray-300 dark:bg-gray-700 hover:bg-gray-400 dark:hover:bg-gray-600 rounded-md">
                    Cancelar
                </button>
                <button id="enviarWhatsAppBtn" class="px-4 py-2 bg-green-600 hover:bg-green-700 text-white rounded-md">
                    <i class="fab fa-whatsapp mr-1"></i> Enviar para WhatsApp
                </button>
            </div>
        </div>
    </div>

    <!-- Modal de detalhes da venda -->
    <div id="detalheVendaModal" class="fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center hidden">
        <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6 w-full max-w-lg mx-4">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl font-semibold">Detalhes da Venda</h2>
                <button class="modal-close text-gray-500 hover:text-gray-700 dark:hover:text-gray-300">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            
            <div class="mb-4">
                <div id="detalheVendaConteudo" class="border border-gray-300 dark:border-gray-600 rounded-md p-3">
                    <!-- Detalhes serão preenchidos dinamicamente -->
                </div>
            </div>
            
            <div class="flex justify-end gap-2">
                <button class="modal-close px-4 py-2 bg-gray-300 dark:bg-gray-700 hover:bg-gray-400 dark:hover:bg-gray-600 rounded-md">
                    Fechar
                </button>
                <button id="reenviarWhatsAppBtn" class="px-4 py-2 bg-green-600 hover:bg-green-700 text-white rounded-md">
                    <i class="fab fa-whatsapp mr-1"></i> Reenviar para WhatsApp
                </button>
            </div>
        </div>
    </div>

    <!-- Modal de contrato -->
    <div id="contratoModal" class="fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center hidden">
        <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6 w-full max-w-2xl mx-4">
            <div class="flex justify-between items-center mb-4">
                <h2 class="text-xl font-semibold">Contrato de Consignação</h2>
                <button class="modal-close text-gray-500 hover:text-gray-700 dark:hover:text-gray-300">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            
            <div class="mb-4 max-h-96 overflow-y-auto">
                <div id="contratoTexto" class="text-sm">
                    <!-- Texto do contrato será preenchido dinamicamente -->
                </div>
            </div>
            
            <div class="mb-4">
                <h3 class="font-bold mb-2">Assinatura do Cliente</h3>
                <div class="signature-container">
                    <canvas id="assinaturaContrato" class="signature-pad"></canvas>
                </div>
                <div class="flex justify-end mt-1">
                    <button id="limparAssinaturaContratoBtn" class="text-sm text-primary">Limpar assinatura</button>
                </div>
            </div>
            
            <div class="flex justify-end gap-2">
                <button class="modal-close px-4 py-2 bg-gray-300 dark:bg-gray-700 hover:bg-gray-400 dark:hover:bg-gray-600 rounded-md">
                    Cancelar
                </button>
                <button id="enviarContratoBtn" class="px-4 py-2 bg-green-600 hover:bg-green-700 text-white rounded-md">
                    <i class="fab fa-whatsapp mr-1"></i> Enviar Contrato
                </button>
            </div>
        </div>
    </div>

    <script>
        // Config do Firebase
        const firebaseConfig = {
            apiKey: "AIzaSyAgVn4j0KwKh6kh8ZlmbMHDnaMJN8djWsU",
            authDomain: "conection-acessorios.firebaseapp.com",
            databaseURL: "https://conection-acessorios-default-rtdb.firebaseio.com",
            projectId: "conection-acessorios",
            storageBucket: "conection-acessorios.appspot.com",
            messagingSenderId: "289569375328",
            appId: "1:289569375328:web:8cb68977c5868d27eb9cbd"
        };

        // Inicializar Firebase
        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();

        // Status de conexão e sincronização
        let isOnline = false;
        let pendingChanges = {};

        // Monitorar status de conexão com o Firebase
        const connectedRef = firebase.database().ref(".info/connected");
        connectedRef.on("value", (snap) => {
            isOnline = snap.val() === true;
            updateConnectionStatus();
        });

        // Verificar modo escuro
        if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
            document.documentElement.classList.add('dark');
        }
        
        window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', event => {
            if (event.matches) {
                document.documentElement.classList.add('dark');
            } else {
                document.documentElement.classList.remove('dark');
            }
        });

        // Variáveis globais
        let clientes = [];
        let produtos = [];
        let vendas = [];
        let movimentacoes = [];
        
        // Dados da venda atual
        let vendaAtual = {
            cliente: null,
            itens: [],
            total: 0,
            data: null
        };

        // Cliente selecionado para visualizar histórico
        let clienteHistoricoAtual = null;

        // Inicialização do sistema
        document.addEventListener('DOMContentLoaded', function() {
            // Inicializar Firebase e carregar dados
            initDatabase();
            
            // Inicializar abas
            const tabBtns = document.querySelectorAll('.tab-btn');
            tabBtns.forEach(btn => {
                btn.addEventListener('click', () => {
                    const target = btn.getAttribute('data-target');
                    switchTab(target);
                });
            });
            
            // Inicializar assinatura
            const canvasAssinatura = document.getElementById('assinaturaCliente');
            const signaturePad = new SignaturePad(canvasAssinatura);
            
            const canvasContrato = document.getElementById('assinaturaContrato');
            const signaturePadContrato = new SignaturePad(canvasContrato);
            
            // Botão de modo escuro
            document.getElementById('darkModeToggle').addEventListener('click', () => {
                document.documentElement.classList.toggle('dark');
            });

            // Botão de sincronização
            document.getElementById('syncBtn').addEventListener('click', () => {
                if (Object.keys(pendingChanges).length > 0) {
                    syncChangesToServer();
                } else {
                    showToast("Todos os dados já estão sincronizados.", "success");
                }
            });
            
            // Botões para fechar modais
            document.querySelectorAll('.modal-close').forEach(btn => {
                btn.addEventListener('click', () => {
                    document.querySelectorAll('.fixed').forEach(modal => {
                        if (!modal.id.startsWith('loading')) {
                            modal.classList.add('hidden');
                        }
                    });
                });
            });
            
            // Botão para novo cliente na tela de venda
            document.getElementById('novoClienteBtn').addEventListener('click', () => {
                openClienteModal();
            });
            
            // Botão para adicionar cliente na tela de clientes
            document.getElementById('adicionarClienteBtn').addEventListener('click', () => {
                openClienteModal();
            });
            
            // Botão para adicionar produto
            document.getElementById('adicionarProdutoGerenciarBtn').addEventListener('click', () => {
                openProdutoModal();
            });
            
            // Formulário de cliente
            document.getElementById('clienteForm').addEventListener('submit', (e) => {
                e.preventDefault();
                saveCliente();
            });
            
            // Formulário de produto
            document.getElementById('produtoForm').addEventListener('submit', (e) => {
                e.preventDefault();
                saveProduto();
            });
            
            // Campo de busca de clientes
            document.getElementById('clienteSearch').addEventListener('input', (e) => {
                const search = e.target.value.toLowerCase();
                if (search.length > 1) {
                    const filtered = clientes.filter(cliente => 
                        cliente.nome.toLowerCase().includes(search) || 
                        cliente.numeroDocumento.toLowerCase().includes(search)
                    );
                    showClientesDropdown(filtered);
                } else {
                    document.getElementById('clientesDropdown').classList.add('hidden');
                }
            });
            
            // Campo de busca na lista de clientes
            document.getElementById('clienteSearchList').addEventListener('input', (e) => {
                const search = e.target.value.toLowerCase();
                renderClientesList(search);
            });
            
            // Botão para adicionar produto à venda
            document.getElementById('adicionarProdutoBtn').addEventListener('click', () => {
                const produtoSelect = document.getElementById('produtoSelect');
                const produtoId = produtoSelect.value;
                
                if (produtoId) {
                    const produto = produtos.find(p => p.id === produtoId);
                    if (produto) {
                        addProdutoToVenda(produto);
                        produtoSelect.value = '';
                    }
                }
            });
            
            // Botão para limpar venda
            document.getElementById('limparVendaBtn').addEventListener('click', () => {
                resetVenda();
            });
            
            // Botão para finalizar venda
            document.getElementById('finalizarVendaBtn').addEventListener('click', () => {
                if (vendaAtual.cliente && vendaAtual.itens.length > 0) {
                    openFinalizarVendaModal();
                } else {
                    showToast('Selecione um cliente e adicione itens à venda.', 'error');
                }
            });
            
            // Botão para limpar assinatura
            document.getElementById('limparAssinaturaBtn').addEventListener('click', () => {
                signaturePad.clear();
            });
            
            // Botão para limpar assinatura do contrato
            document.getElementById('limparAssinaturaContratoBtn').addEventListener('click', () => {
                signaturePadContrato.clear();
            });
            
            // Botão para enviar WhatsApp
            document.getElementById('enviarWhatsAppBtn').addEventListener('click', () => {
                if (signaturePad.isEmpty()) {
                    showToast('Por favor, assine antes de continuar.', 'error');
                    return;
                }
                
                enviarResumoWhatsApp();
            });
            
            // Botão para reenviar WhatsApp
            document.getElementById('reenviarWhatsAppBtn').addEventListener('click', () => {
                const vendaId = document.getElementById('reenviarWhatsAppBtn').getAttribute('data-venda-id');
                if (vendaId) {
                    const venda = vendas.find(v => v.id === vendaId);
                    if (venda) {
                        reenviarVendaWhatsApp(venda);
                    }
                }
            });
            
            // Botão para enviar contrato
            document.getElementById('enviarContratoBtn').addEventListener('click', () => {
                if (signaturePadContrato.isEmpty()) {
                    showToast('Por favor, assine antes de continuar.', 'error');
                    return;
                }
                
                enviarContratoWhatsApp();
            });
            
            // Botão para registrar movimentação
            document.getElementById('registrarMovimentacaoBtn').addEventListener('click', () => {
                registrarMovimentacao();
            });
            
            // Botão para ver histórico de cliente
            document.getElementById('verHistoricoBtn').addEventListener('click', () => {
                if (vendaAtual.cliente) {
                    verHistoricoCliente(vendaAtual.cliente);
                }
            });
            
            // Botão para voltar para a lista de clientes
            document.getElementById('voltarClientesBtn').addEventListener('click', () => {
                // Se veio da tela de vendas, volta para vendas
                if (document.querySelector('[data-target="venda"]').classList.contains('bg-primary')) {
                    switchTab('venda');
                } else {
                    // Senão volta para a lista de clientes
                    switchTab('clientes');
                }
            });
        });

        // Inicializar banco de dados e carregar dados iniciais
        function initDatabase() {
            // Carregar produtos
            db.ref('produtos').on('value', (snapshot) => {
                const data = snapshot.val() || {};
                produtos = Object.keys(data).map(key => {
                    return {
                        id: key,
                        ...data[key]
                    };
                });
                
                // Preencher select de produtos
                const produtoSelect = document.getElementById('produtoSelect');
                produtoSelect.innerHTML = '<option value="" disabled selected>Selecione um produto</option>';
                
                produtos.forEach(produto => {
                    const option = document.createElement('option');
                    option.value = produto.id;
                    option.textContent = `${produto.nome} - R$${parseFloat(produto.preco).toFixed(2)}`;
                    produtoSelect.appendChild(option);
                });
                
                renderProdutosList();
                
                // Se não tiver produtos, criar produtos padrão
                if (produtos.length === 0) {
                    const produtosPadrao = [
                        { nome: 'CABO V8', preco: 25.00 },
                        { nome: 'CABO TIPO C', preco: 25.00 },
                        { nome: 'CABO IPHONE', preco: 25.00 },
                        { nome: 'FONTE VEICULAR', preco: 25.00 },
                        { nome: 'FONTE PAREDE', preco: 25.00 },
                        { nome: 'FONE DE OUVIDO UNIV.', preco: 25.00 },
                        { nome: 'FONE DE OUVIDO BLUETOOTH', preco: 50.00 }
                    ];
                    
                    produtosPadrao.forEach(produto => {
                        db.ref('produtos').push(produto);
                    });
                }
            });
            
            // Carregar clientes
            db.ref('clientes').on('value', (snapshot) => {
                const data = snapshot.val() || {};
                clientes = Object.keys(data).map(key => {
                    return {
                        id: key,
                        ...data[key]
                    };
                });
                
                renderClientesList();
            });
            
            // Carregar vendas
            db.ref('vendas').on('value', (snapshot) => {
                const data = snapshot.val() || {};
                vendas = Object.keys(data).map(key => {
                    const venda = data[key];
                    
                    // Converter data de string para objeto Date
                    if (venda.data && typeof venda.data === 'string') {
                        venda.data = new Date(venda.data);
                    }
                    
                    return {
                        id: key,
                        ...venda
                    };
                });
                
                // Se cliente atual estiver com histórico aberto, atualizar
                if (clienteHistoricoAtual) {
                    const vendasCliente = vendas.filter(v => v.cliente.id === clienteHistoricoAtual.id);
                    renderHistoricoCliente(vendasCliente);
                }
            });
            
            // Carregar movimentações
            db.ref('movimentacoes').on('value', (snapshot) => {
                const data = snapshot.val() || {};
                movimentacoes = Object.keys(data).map(key => {
                    const movimentacao = data[key];
                    
                    // Converter data de string para objeto Date
                    if (movimentacao.data && typeof movimentacao.data === 'string') {
                        movimentacao.data = new Date(movimentacao.data);
                    }
                    
                    return {
                        id: key,
                        ...movimentacao
                    };
                });
                
                renderMovimentacoesList();
                updateCaixaTotal();
            });
            
            // Remover overlay de carregamento quando terminar
            setTimeout(() => {
                document.getElementById('loading-overlay').classList.add('hidden');
            }, 1500);
        }

        // Atualizar status de conexão
        function updateConnectionStatus() {
            const syncStatus = document.getElementById('sync-status');
            const syncBtn = document.getElementById('syncBtn');
            
            if (isOnline) {
                syncStatus.classList.remove('bg-red-500');
                syncStatus.classList.add('bg-green-500');
                syncBtn.title = "Sincronizado com o servidor";
            } else {
                syncStatus.classList.remove('bg-green-500');
                syncStatus.classList.add('bg-red-500');
                syncBtn.title = "Offline - Alterações serão sincronizadas quando conectado";
            }
            
            // Mostrar indicador de status apenas se tiver alterações ou estiver offline
            if (!isOnline || Object.keys(pendingChanges).length > 0) {
                syncStatus.classList.remove('hidden');
            } else {
                syncStatus.classList.add('hidden');
            }
        }

        // Sincronizar mudanças com o servidor
        function syncChangesToServer() {
            if (!isOnline) {
                showToast("Você está offline. As alterações serão sincronizadas automaticamente quando a conexão for restabelecida.", "error");
                return;
            }
            
            // Atualizar cada entidade com mudanças pendentes
            Object.keys(pendingChanges).forEach(path => {
                db.ref(path).update(pendingChanges[path])
                    .then(() => {
                        delete pendingChanges[path];
                        updateConnectionStatus();
                        showToast("Dados sincronizados com sucesso!", "success");
                    })
                    .catch(error => {
                        showToast(`Erro ao sincronizar: ${error.message}`, "error");
                    });
            });
        }

        // Mostrar toast de notificação
        function showToast(message, type = 'info') {
            const toastContainer = document.getElementById('toast-container');
            
            const toast = document.createElement('div');
            toast.className = 'toast';
            
            switch(type) {
                case 'success':
                    toast.classList.add('bg-green-500', 'text-white');
                    break;
                case 'error':
                    toast.classList.add('bg-red-500', 'text-white');
                    break;
                case 'warning':
                    toast.classList.add('bg-yellow-500', 'text-white');
                    break;
                default:
                    toast.classList.add('bg-blue-500', 'text-white');
            }
            
            toast.textContent = message;
            toastContainer.appendChild(toast);
            
            // Remover o toast após 5 segundos
            setTimeout(() => {
                toast.remove();
            }, 5000);
        }

        // Função para trocar de aba
        function switchTab(target) {
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.add('hidden');
            });
            
            // Se for aba de histórico não muda os botões da navegação
            if (target !== 'historicoCliente') {
                document.querySelectorAll('.tab-btn').forEach(btn => {
                    if (btn.getAttribute('data-target') === target) {
                        btn.classList.add('bg-primary', 'text-white');
                        btn.classList.remove('hover:bg-gray-200', 'dark:hover:bg-gray-700');
                    } else {
                        btn.classList.remove('bg-primary', 'text-white');
                        btn.classList.add('hover:bg-gray-200', 'dark:hover:bg-gray-700');
                    }
                });
            }
            
            document.getElementById(target).classList.remove('hidden');
        }

        // Função para mostrar dropdown de clientes
        function showClientesDropdown(clientesList) {
            const dropdown = document.getElementById('clientesDropdown');
            dropdown.innerHTML = '';
            
            if (clientesList.length === 0) {
                const item = document.createElement('div');
                item.textContent = 'Nenhum cliente encontrado';
                item.className = 'px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 cursor-default';
                dropdown.appendChild(item);
            } else {
                clientesList.forEach(cliente => {
                    const item = document.createElement('div');
                    item.textContent = `${cliente.nome} - ${cliente.numeroDocumento}`;
                    item.className = 'px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 cursor-pointer';
                    item.addEventListener('click', () => {
                        selectCliente(cliente);
                        dropdown.classList.add('hidden');
                        document.getElementById('clienteSearch').value = '';
                    });
                    dropdown.appendChild(item);
                });
            }
            
            dropdown.classList.remove('hidden');
        }

        // Função para selecionar cliente
        function selectCliente(cliente) {
            vendaAtual.cliente = cliente;
            
            document.getElementById('clienteSelecionado').classList.remove('hidden');
            document.getElementById('clienteNome').textContent = cliente.nome;
            document.getElementById('clienteDetalhes').textContent = `${cliente.tipoDocumento.toUpperCase()}: ${cliente.numeroDocumento}`;
            document.getElementById('clienteContato').textContent = `Telefone: ${cliente.telefone}`;
        }

        // Função para adicionar produto à venda
        function addProdutoToVenda(produto) {
            const existente = vendaAtual.itens.findIndex(item => item.produto.id === produto.id);
            
            if (existente !== -1) {
                vendaAtual.itens[existente].quantidade += 1;
                vendaAtual.itens[existente].subtotal = produto.preco * vendaAtual.itens[existente].quantidade;
            } else {
                vendaAtual.itens.push({
                    produto: produto,
                    quantidade: 1,
                    subtotal: produto.preco
                });
            }
            
            updateVendaTotal();
            renderItensVenda();
        }

        // Função para atualizar o total da venda
        function updateVendaTotal() {
            vendaAtual.total = vendaAtual.itens.reduce((total, item) => {
                return total + (parseFloat(item.produto.preco) * item.quantidade);
            }, 0);
            
            document.getElementById('totalVenda').textContent = `R$ ${vendaAtual.total.toFixed(2)}`;
        }

        // Função para renderizar itens da venda
        function renderItensVenda() {
            const tbody = document.getElementById('itensVenda');
            tbody.innerHTML = '';
            
            vendaAtual.itens.forEach((item, index) => {
                const tr = document.createElement('tr');
                
                const tdProduto = document.createElement('td');
                tdProduto.className = 'px-4 py-2 border-b dark:border-gray-700';
                tdProduto.textContent = item.produto.nome;
                
                const tdPreco = document.createElement('td');
                tdPreco.className = 'px-4 py-2 border-b dark:border-gray-700 text-center';
                tdPreco.textContent = `R$ ${parseFloat(item.produto.preco).toFixed(2)}`;
                
                const tdQuantidade = document.createElement('td');
                tdQuantidade.className = 'px-4 py-2 border-b dark:border-gray-700 text-center';
                
                const qtyContainer = document.createElement('div');
                qtyContainer.className = 'inline-flex items-center';
                
                const btnMinus = document.createElement('button');
                btnMinus.className = 'bg-gray-200 dark:bg-gray-700 px-2 py-1 rounded-l-md';
                btnMinus.innerHTML = '<i class="fas fa-minus"></i>';
                btnMinus.addEventListener('click', () => {
                    changeQuantidade(index, -1);
                });
                
                const qtySpan = document.createElement('span');
                qtySpan.className = 'px-3';
                qtySpan.textContent = item.quantidade;
                
                const btnPlus = document.createElement('button');
                btnPlus.className = 'bg-gray-200 dark:bg-gray-700 px-2 py-1 rounded-r-md';
                btnPlus.innerHTML = '<i class="fas fa-plus"></i>';
                btnPlus.addEventListener('click', () => {
                    changeQuantidade(index, 1);
                });
                
                qtyContainer.appendChild(btnMinus);
                qtyContainer.appendChild(qtySpan);
                qtyContainer.appendChild(btnPlus);
                tdQuantidade.appendChild(qtyContainer);
                
                const tdSubtotal = document.createElement('td');
                tdSubtotal.className = 'px-4 py-2 border-b dark:border-gray-700 text-center';
                tdSubtotal.textContent = `R$ ${(parseFloat(item.produto.preco) * item.quantidade).toFixed(2)}`;
                
                const tdAcoes = document.createElement('td');
                tdAcoes.className = 'px-4 py-2 border-b dark:border-gray-700 text-center';
                
                const btnRemove = document.createElement('button');
                btnRemove.className = 'text-red-500 hover:text-red-700';
                btnRemove.innerHTML = '<i class="fas fa-trash"></i>';
                btnRemove.addEventListener('click', () => {
                    removeItem(index);
                });
                
                tdAcoes.appendChild(btnRemove);
                
                tr.appendChild(tdProduto);
                tr.appendChild(tdPreco);
                tr.appendChild(tdQuantidade);
                tr.appendChild(tdSubtotal);
                tr.appendChild(tdAcoes);
                
                tbody.appendChild(tr);
            });
        }

        // Função para alterar quantidade
        function changeQuantidade(index, delta) {
            const item = vendaAtual.itens[index];
            item.quantidade += delta;
            
            if (item.quantidade < 1) {
                item.quantidade = 1;
            }
            
            item.subtotal = item.produto.preco * item.quantidade;
            
            updateVendaTotal();
            renderItensVenda();
        }

        // Função para remover item
        function removeItem(index) {
            vendaAtual.itens.splice(index, 1);
            updateVendaTotal();
            renderItensVenda();
        }

        // Função para resetar venda
        function resetVenda() {
            vendaAtual = {
                cliente: null,
                itens: [],
                total: 0,
                data: null
            };
            
            document.getElementById('clienteSelecionado').classList.add('hidden');
            document.getElementById('totalVenda').textContent = 'R$ 0,00';
            document.getElementById('itensVenda').innerHTML = '';
        }

        // Função para abrir modal de finalizar venda
        function openFinalizarVendaModal() {
            const modal = document.getElementById('finalizarVendaModal');
            const resumo = document.getElementById('resumoVenda');
            
            let resumoHtml = `
                <p class="font-bold">Cliente: ${vendaAtual.cliente.nome}</p>
                <p>Data: ${new Date().toLocaleDateString('pt-BR')}</p>
                <hr class="my-2 border-gray-300 dark:border-gray-600">
                <table class="w-full text-sm">
                    <thead>
                        <tr>
                            <th class="text-left">Produto</th>
                            <th class="text-center">Qtd</th>
                            <th class="text-right">Subtotal</th>
                        </tr>
                    </thead>
                    <tbody>
            `;
            
            vendaAtual.itens.forEach(item => {
                resumoHtml += `
                    <tr>
                        <td>${item.produto.nome}</td>
                        <td class="text-center">${item.quantidade}</td>
                        <td class="text-right">R$ ${(parseFloat(item.produto.preco) * item.quantidade).toFixed(2)}</td>
                    </tr>
                `;
            });
            
            resumoHtml += `
                    </tbody>
                    <tfoot>
                        <tr>
                            <td colspan="2" class="text-right font-bold">Total:</td>
                            <td class="text-right font-bold">R$ ${vendaAtual.total.toFixed(2)}</td>
                        </tr>
                    </tfoot>
                </table>
            `;
            
            resumo.innerHTML = resumoHtml;
            modal.classList.remove('hidden');
            
            // Reiniciar a assinatura
            const canvasAssinatura = document.getElementById('assinaturaCliente');
            const signaturePad = new SignaturePad(canvasAssinatura);
            signaturePad.clear();
        }

        // Função para enviar resumo para WhatsApp
        function enviarResumoWhatsApp() {
            vendaAtual.data = new Date();
            
            // Adicionar à lista de vendas
            const novaVenda = {
                cliente: vendaAtual.cliente,
                itens: [...vendaAtual.itens],
                total: vendaAtual.total,
                data: vendaAtual.data.toISOString()  // Armazenar como string ISO
            };
            
            // Salvar no Firebase
            const vendaRef = db.ref('vendas').push();
            vendaRef.set(novaVenda)
                .then(() => {
                    showToast("Venda registrada com sucesso!", "success");
                    
                    // Adicionar ao caixa
                    const movimentacao = {
                        tipo: 'entrada',
                        descricao: `Venda - Cliente: ${novaVenda.cliente.nome}`,
                        valor: novaVenda.total,
                        data: new Date().toISOString()  // Armazenar como string ISO
                    };
                    
                    return db.ref('movimentacoes').push(movimentacao);
                })
                .then(() => {
                    showToast("Movimentação de caixa registrada!", "success");
                    
                    // Enviar para o WhatsApp
                    const venda = {
                        id: vendaRef.key,
                        ...novaVenda,
                        data: new Date(novaVenda.data)  // Converter de volta para Date para exibição
                    };
                    
                    enviarVendaWhatsApp(venda);
                    
                    // Fechar modal e resetar venda
                    document.getElementById('finalizarVendaModal').classList.add('hidden');
                    resetVenda();
                })
                .catch(error => {
                    showToast(`Erro ao salvar: ${error.message}`, "error");
                    
                    // Se estiver offline, armazenar para sincronização posterior
                    if (!isOnline) {
                        const vendaKey = `venda_temp_${Date.now()}`;
                        pendingChanges[`vendas/${vendaKey}`] = novaVenda;
                        updateConnectionStatus();
                        
                        showToast("Venda armazenada localmente e será sincronizada quando houver conexão.", "warning");
                    }
                });
        }

        // Função para reenviar resumo da venda para WhatsApp
        function reenviarVendaWhatsApp(venda) {
            enviarVendaWhatsApp(venda);
            document.getElementById('detalheVendaModal').classList.add('hidden');
        }

        // Função para enviar venda para WhatsApp
        function enviarVendaWhatsApp(venda) {
            // Gerar mensagem de WhatsApp
            let mensagem = `*RESUMO DE VENDA - CONECTION ACESSÓRIOS*\n\n`;
            mensagem += `*Cliente:* ${venda.cliente.nome}\n`;
            mensagem += `*Data:* ${venda.data instanceof Date ? venda.data.toLocaleDateString('pt-BR') : new Date(venda.data).toLocaleDateString('pt-BR')}\n\n`;
            mensagem += `*ITENS:*\n`;
            
            venda.itens.forEach(item => {
                mensagem += `${item.produto.nome} - ${item.quantidade}x - R$ ${(parseFloat(item.produto.preco) * item.quantidade).toFixed(2)}\n`;
            });
            
            mensagem += `\n*TOTAL: R$ ${parseFloat(venda.total).toFixed(2)}*\n\n`;
            mensagem += `Para realizar o pagamento, por favor, faça um PIX para:\ndanielgoncalvesdemoura011@gmail.com\n\nObrigado pela preferência!`;
            
            // Codificar mensagem para URL
            const mensagemCodificada = encodeURIComponent(mensagem);
            const telefone = venda.cliente.telefone.replace(/\D/g, ''); // Remove não-números
            
            // Abrir WhatsApp
            const whatsappURL = `https://wa.me/55${telefone}?text=${mensagemCodificada}`;
            window.open(whatsappURL, '_blank');
        }

        // Função para enviar contrato para WhatsApp
        function enviarContratoWhatsApp() {
            // Codificar mensagem para URL
            const mensagemCodificada = encodeURIComponent(document.getElementById('contratoTexto').textContent);
            const telefone = vendaAtual.cliente.telefone.replace(/\D/g, ''); // Remove não-números
            
            // Abrir WhatsApp
            const whatsappURL = `https://wa.me/55${telefone}?text=${mensagemCodificada}`;
            window.open(whatsappURL, '_blank');
            
            // Fechar modal
            document.getElementById('contratoModal').classList.add('hidden');
        }

        // Função para registrar movimentação no caixa
        function registrarMovimentacao() {
            const tipo = document.getElementById('tipoMovimentacao').value;
            const descricao = document.getElementById('descricaoMovimentacao').value;
            const valor = parseFloat(document.getElementById('valorMovimentacao').value);
            
            if (!descricao || isNaN(valor) || valor <= 0) {
                showToast('Preencha todos os campos corretamente.', 'error');
                return;
            }
            
            const movimentacao = {
                tipo: tipo,
                descricao: descricao,
                valor: valor,
                data: new Date().toISOString()  // Armazenar como string ISO
            };
            
            // Salvar no Firebase
            db.ref('movimentacoes').push(movimentacao)
                .then(() => {
                    showToast("Movimentação registrada com sucesso!", "success");
                    document.getElementById('descricaoMovimentacao').value = '';
                    document.getElementById('valorMovimentacao').value = '';
                })
                .catch(error => {
                    showToast(`Erro ao salvar: ${error.message}`, "error");
                    
                    // Se estiver offline, armazenar para sincronização posterior
                    if (!isOnline) {
                        const movKey = `mov_temp_${Date.now()}`;
                        pendingChanges[`movimentacoes/${movKey}`] = movimentacao;
                        updateConnectionStatus();
                        
                        showToast("Movimentação armazenada localmente e será sincronizada quando houver conexão.", "warning");
                    }
                });
        }

        // Função para atualizar totais do caixa
        function updateCaixaTotal() {
            const entradas = movimentacoes
                .filter(m => m.tipo === 'entrada')
                .reduce((total, m) => total + parseFloat(m.valor), 0);
                
            const saidas = movimentacoes
                .filter(m => m.tipo === 'saida')
                .reduce((total, m) => total + parseFloat(m.valor), 0);
                
            const saldo = entradas - saidas;
            
            document.getElementById('totalEntradas').textContent = `R$ ${entradas.toFixed(2)}`;
            document.getElementById('totalSaidas').textContent = `R$ ${saidas.toFixed(2)}`;
            document.getElementById('saldoCaixa').textContent = `R$ ${saldo.toFixed(2)}`;
        }

        // Função para renderizar lista de movimentações
        function renderMovimentacoesList() {
            const tbody = document.getElementById('movimentacoesList');
            tbody.innerHTML = '';
            
            // Ordenar por data decrescente
            const sorted = [...movimentacoes].sort((a, b) => {
                const dateA = a.data instanceof Date ? a.data : new Date(a.data);
                const dateB = b.data instanceof Date ? b.data : new Date(b.data);
                return dateB - dateA;
            });
            
            sorted.forEach(movimentacao => {
                const tr = document.createElement('tr');
                
                const tdData = document.createElement('td');
                tdData.className = 'px-4 py-2 border-b dark:border-gray-700';
                tdData.textContent = movimentacao.data instanceof Date 
                    ? movimentacao.data.toLocaleDateString('pt-BR') 
                    : new Date(movimentacao.data).toLocaleDateString('pt-BR');
                
                const tdTipo = document.createElement('td');
                tdTipo.className = 'px-4 py-2 border-b dark:border-gray-700';
                if (movimentacao.tipo === 'entrada') {
                    tdTipo.innerHTML = '<span class="text-green-600 dark:text-green-400">Entrada</span>';
                } else {
                    tdTipo.innerHTML = '<span class="text-red-600 dark:text-red-400">Saída</span>';
                }
                
                const tdDescricao = document.createElement('td');
                tdDescricao.className = 'px-4 py-2 border-b dark:border-gray-700';
                tdDescricao.textContent = movimentacao.descricao;
                
                const tdValor = document.createElement('td');
                tdValor.className = 'px-4 py-2 border-b dark:border-gray-700 text-right';
                tdValor.textContent = `R$ ${parseFloat(movimentacao.valor).toFixed(2)}`;
                
                tr.appendChild(tdData);
                tr.appendChild(tdTipo);
                tr.appendChild(tdDescricao);
                tr.appendChild(tdValor);
                
                tbody.appendChild(tr);
            });
        }

        // Função para abrir modal de cliente
        function openClienteModal(cliente = null) {
            const modal = document.getElementById('clienteModal');
            const form = document.getElementById('clienteForm');
            const title = document.getElementById('clienteModalTitle');
            
            if (cliente) {
                title.textContent = 'Editar Cliente';
                document.getElementById('clienteId').value = cliente.id;
                document.getElementById('nomeCliente').value = cliente.nome;
                document.getElementById('tipoDocumento').value = cliente.tipoDocumento;
                document.getElementById('numeroDocumento').value = cliente.numeroDocumento;
                document.getElementById('telefoneCliente').value = cliente.telefone;
                document.getElementById('enderecoCliente').value = cliente.endereco || '';
            } else {
                title.textContent = 'Cadastrar Novo Cliente';
                form.reset();
                document.getElementById('clienteId').value = '';
            }
            
            modal.classList.remove('hidden');
        }

        // Função para salvar cliente
        function saveCliente() {
            const id = document.getElementById('clienteId').value;
            const nome = document.getElementById('nomeCliente').value;
            const tipoDocumento = document.getElementById('tipoDocumento').value;
            const numeroDocumento = document.getElementById('numeroDocumento').value;
            const telefone = document.getElementById('telefoneCliente').value;
            const endereco = document.getElementById('enderecoCliente').value;
            
            if (!nome || !numeroDocumento || !telefone) {
                showToast('Preencha os campos obrigatórios.', 'error');
                return;
            }
            
            const clienteData = {
                nome,
                tipoDocumento,
                numeroDocumento,
                telefone,
                endereco
            };
            
            if (id) {
                // Editar cliente existente
                db.ref(`clientes/${id}`).update(clienteData)
                    .then(() => {
                        showToast("Cliente atualizado com sucesso!", "success");
                        document.getElementById('clienteModal').classList.add('hidden');
                    })
                    .catch(error => {
                        showToast(`Erro ao atualizar: ${error.message}`, "error");
                        
                        // Se estiver offline, armazenar para sincronização posterior
                        if (!isOnline) {
                            pendingChanges[`clientes/${id}`] = clienteData;
                            updateConnectionStatus();
                            
                            showToast("Alterações armazenadas localmente e serão sincronizadas quando houver conexão.", "warning");
                            document.getElementById('clienteModal').classList.add('hidden');
                        }
                    });
            } else {
                // Novo cliente
                db.ref('clientes').push(clienteData)
                    .then((ref) => {
                        showToast("Cliente cadastrado com sucesso!", "success");
                        document.getElementById('clienteModal').classList.add('hidden');
                        
                        // Após cadastrar, abrir modal de contrato
                        openContratoModal({
                            id: ref.key,
                            ...clienteData
                        });
                    })
                    .catch(error => {
                        showToast(`Erro ao cadastrar: ${error.message}`, "error");
                        
                        // Se estiver offline, armazenar para sincronização posterior
                        if (!isOnline) {
                            const clienteKey = `cliente_temp_${Date.now()}`;
                            pendingChanges[`clientes/${clienteKey}`] = clienteData;
                            updateConnectionStatus();
                            
                            showToast("Cliente armazenado localmente e será sincronizado quando houver conexão.", "warning");
                            document.getElementById('clienteModal').classList.add('hidden');
                            
                            // Ainda permitir abrir o contrato
                            openContratoModal({
                                id: clienteKey,
                                ...clienteData
                            });
                        }
                    });
            }
        }

        // Função para abrir modal de contrato
        function openContratoModal(cliente) {
            const modal = document.getElementById('contratoModal');
            const contratoTexto = document.getElementById('contratoTexto');
            
            const dataAtual = new Date().toLocaleDateString('pt-BR');
            
            let textoContrato = `
                <h2 class="text-center font-bold text-lg mb-4">CONTRATO DE CONSIGNAÇÃO</h2>
                
                <p class="mb-2"><strong>CONSIGNANTE:</strong> Conection Acessórios, empresa estabelecida conforme as leis brasileiras.</p>
                
                <p class="mb-2"><strong>CONSIGNATÁRIO:</strong> ${cliente.nome}, portador do ${cliente.tipoDocumento.toUpperCase()} nº ${cliente.numeroDocumento}, residente/estabelecido em ${cliente.endereco}.</p>
                
                <p class="mb-4">Firmam o presente contrato de consignação mediante as seguintes cláusulas e condições:</p>
                
                <p class="mb-2"><strong>CLÁUSULA 1ª - OBJETO</strong></p>
                <p class="mb-4">O CONSIGNANTE entrega ao CONSIGNATÁRIO produtos para revenda, mantendo a propriedade dos mesmos até que sejam efetivamente vendidos a terceiros ou devolvidos ao CONSIGNANTE.</p>
                
                <p class="mb-2"><strong>CLÁUSULA 2ª - RESPONSABILIDADES DO CONSIGNATÁRIO</strong></p>
                <p class="mb-4">O CONSIGNATÁRIO compromete-se a zelar pelos produtos consignados, sendo responsável por sua guarda e conservação. Em caso de perda, extravio ou dano, o CONSIGNATÁRIO deverá pagar ao CONSIGNANTE o valor de venda integral dos produtos.</p>
                
                <p class="mb-2"><strong>CLÁUSULA 3ª - PAGAMENTOS</strong></p>
                <p class="mb-4">O CONSIGNATÁRIO deverá efetuar pagamentos semanais referentes às vendas realizadas. O atraso nos pagamentos acarretará multa de R$30,00 (trinta reais) mais 10% (dez por cento) do valor em atraso, por dia de atraso.</p>
                
                <p class="mb-2"><strong>CLÁUSULA 4ª - PRAZO</strong></p>
                <p class="mb-4">Este contrato tem prazo indeterminado, podendo ser rescindido por qualquer das partes mediante comunicação prévia de 15 (quinze) dias.</p>
                
                <p class="mb-4">E por estarem justos e contratados, firmam o presente contrato em duas vias de igual teor.</p>
                
                <p class="mb-2">Data: ${dataAtual}</p>
                
                <p class="mb-4 mt-8 text-center">
                    ______________________________________<br>
                    ${cliente.nome}<br>
                    CONSIGNATÁRIO
                </p>
            `;
            
            contratoTexto.innerHTML = textoContrato;
            
            // Guardar cliente para usar no envio de WhatsApp
            vendaAtual.cliente = cliente;
            
            // Reiniciar a assinatura
            const canvasContrato = document.getElementById('assinaturaContrato');
            const signaturePadContrato = new SignaturePad(canvasContrato);
            signaturePadContrato.clear();
            
            modal.classList.remove('hidden');
        }

        // Função para renderizar lista de clientes
        function renderClientesList(search = '') {
            const tbody = document.getElementById('clientesList');
            tbody.innerHTML = '';
            
            let filteredClientes = clientes;
            
            if (search) {
                filteredClientes = clientes.filter(cliente => 
                    cliente.nome.toLowerCase().includes(search.toLowerCase()) || 
                    cliente.numeroDocumento.toLowerCase().includes(search.toLowerCase())
                );
            }
            
            filteredClientes.forEach(cliente => {
                const tr = document.createElement('tr');
                
                const tdNome = document.createElement('td');
                tdNome.className = 'px-4 py-2 border-b dark:border-gray-700';
                tdNome.textContent = cliente.nome;
                
                const tdDocumento = document.createElement('td');
                tdDocumento.className = 'px-4 py-2 border-b dark:border-gray-700';
                tdDocumento.textContent = cliente.numeroDocumento;
                
                const tdTelefone = document.createElement('td');
                tdTelefone.className = 'px-4 py-2 border-b dark:border-gray-700';
                tdTelefone.textContent = cliente.telefone;
                
                const tdAcoes = document.createElement('td');
                tdAcoes.className = 'px-4 py-2 border-b dark:border-gray-700 text-center';
                
                const btnEdit = document.createElement('button');
                btnEdit.className = 'text-blue-500 hover:text-blue-700 mr-2';
                btnEdit.innerHTML = '<i class="fas fa-edit"></i>';
                btnEdit.title = 'Editar cliente';
                btnEdit.addEventListener('click', () => {
                    openClienteModal(cliente);
                });
                
                const btnContrato = document.createElement('button');
                btnContrato.className = 'text-green-500 hover:text-green-700 mr-2';
                btnContrato.innerHTML = '<i class="fas fa-file-contract"></i>';
                btnContrato.title = 'Gerar contrato';
                btnContrato.addEventListener('click', () => {
                    openContratoModal(cliente);
                });
                
                const btnHistorico = document.createElement('button');
                btnHistorico.className = 'text-primary hover:text-secondary mr-2';
                btnHistorico.innerHTML = '<i class="fas fa-history"></i>';
                btnHistorico.title = 'Ver histórico';
                btnHistorico.addEventListener('click', () => {
                    verHistoricoCliente(cliente);
                });
                
                const btnDelete = document.createElement('button');
                btnDelete.className = 'text-red-500 hover:text-red-700';
                btnDelete.innerHTML = '<i class="fas fa-trash"></i>';
                btnDelete.title = 'Excluir cliente';
                btnDelete.addEventListener('click', () => {
                    if (confirm(`Deseja realmente excluir o cliente ${cliente.nome}?`)) {
                        deleteCliente(cliente.id);
                    }
                });
                
                tdAcoes.appendChild(btnEdit);
                tdAcoes.appendChild(btnContrato);
                tdAcoes.appendChild(btnHistorico);
                tdAcoes.appendChild(btnDelete);
                
                tr.appendChild(tdNome);
                tr.appendChild(tdDocumento);
                tr.appendChild(tdTelefone);
                tr.appendChild(tdAcoes);
                
                tbody.appendChild(tr);
            });
        }

        // Função para visualizar histórico de cobrança do cliente
        function verHistoricoCliente(cliente) {
            clienteHistoricoAtual = cliente;
            
            document.getElementById('historicoClienteNome').textContent = `Cliente: ${cliente.nome}`;
            
            const vendasCliente = vendas.filter(v => v.cliente.id === cliente.id);
            
            if (vendasCliente.length === 0) {
                document.getElementById('historicoClienteList').innerHTML = '';
                document.getElementById('semHistorico').classList.remove('hidden');
            } else {
                document.getElementById('semHistorico').classList.add('hidden');
                renderHistoricoCliente(vendasCliente);
            }
            
            switchTab('historicoCliente');
        }

        // Função para renderizar histórico de cliente
        function renderHistoricoCliente(vendasCliente) {
            const tbody = document.getElementById('historicoClienteList');
            tbody.innerHTML = '';
            
            // Ordenar por data decrescente
            const sorted = [...vendasCliente].sort((a, b) => {
                const dateA = a.data instanceof Date ? a.data : new Date(a.data);
                const dateB = b.data instanceof Date ? b.data : new Date(b.data);
                return dateB - dateA;
            });
            
            sorted.forEach(venda => {
                const tr = document.createElement('tr');
                
                const tdData = document.createElement('td');
                tdData.className = 'px-4 py-2 border-b dark:border-gray-700';
                tdData.textContent = venda.data instanceof Date 
                    ? venda.data.toLocaleDateString('pt-BR') 
                    : new Date(venda.data).toLocaleDateString('pt-BR');
                
                const tdItens = document.createElement('td');
                tdItens.className = 'px-4 py-2 border-b dark:border-gray-700';
                
                const totalItens = venda.itens.reduce((total, item) => total + item.quantidade, 0);
                tdItens.textContent = `${totalItens} itens`;
                
                const tdValor = document.createElement('td');
                tdValor.className = 'px-4 py-2 border-b dark:border-gray-700 text-right';
                tdValor.textContent = `R$ ${parseFloat(venda.total).toFixed(2)}`;
                
                const tdAcoes = document.createElement('td');
                tdAcoes.className = 'px-4 py-2 border-b dark:border-gray-700 text-center';
                
                const btnView = document.createElement('button');
                btnView.className = 'text-blue-500 hover:text-blue-700 mr-2';
                btnView.innerHTML = '<i class="fas fa-eye"></i>';
                btnView.title = 'Ver detalhes';
                btnView.addEventListener('click', () => {
                    verDetalheVenda(venda);
                });
                
                const btnResend = document.createElement('button');
                btnResend.className = 'text-green-500 hover:text-green-700';
                btnResend.innerHTML = '<i class="fab fa-whatsapp"></i>';
                btnResend.title = 'Reenviar por WhatsApp';
                btnResend.addEventListener('click', () => {
                    reenviarVendaWhatsApp(venda);
                });
                
                tdAcoes.appendChild(btnView);
                tdAcoes.appendChild(btnResend);
                
                tr.appendChild(tdData);
                tr.appendChild(tdItens);
                tr.appendChild(tdValor);
                tr.appendChild(tdAcoes);
                
                tbody.appendChild(tr);
            });
        }

        // Função para ver detalhe da venda
        function verDetalheVenda(venda) {
            const modal = document.getElementById('detalheVendaModal');
            const conteudo = document.getElementById('detalheVendaConteudo');
            
            let detalheHtml = `
                <p class="font-bold">Cliente: ${venda.cliente.nome}</p>
                <p>Data: ${venda.data instanceof Date ? venda.data.toLocaleDateString('pt-BR') : new Date(venda.data).toLocaleDateString('pt-BR')}</p>
                <hr class="my-2 border-gray-300 dark:border-gray-600">
                <table class="w-full text-sm">
                    <thead>
                        <tr>
                            <th class="text-left">Produto</th>
                            <th class="text-center">Qtd</th>
                            <th class="text-right">Subtotal</th>
                        </tr>
                    </thead>
                    <tbody>
            `;
            
            venda.itens.forEach(item => {
                detalheHtml += `
                    <tr>
                        <td>${item.produto.nome}</td>
                        <td class="text-center">${item.quantidade}</td>
                        <td class="text-right">R$ ${(parseFloat(item.produto.preco) * item.quantidade).toFixed(2)}</td>
                    </tr>
                `;
            });
            
            detalheHtml += `
                    </tbody>
                    <tfoot>
                        <tr>
                            <td colspan="2" class="text-right font-bold">Total:</td>
                            <td class="text-right font-bold">R$ ${parseFloat(venda.total).toFixed(2)}</td>
                        </tr>
                    </tfoot>
                </table>
            `;
            
            conteudo.innerHTML = detalheHtml;
            document.getElementById('reenviarWhatsAppBtn').setAttribute('data-venda-id', venda.id);
            modal.classList.remove('hidden');
        }

        // Função para deletar cliente
        function deleteCliente(id) {
            db.ref(`clientes/${id}`).remove()
                .then(() => {
                    showToast("Cliente excluído com sucesso!", "success");
                })
                .catch(error => {
                    showToast(`Erro ao excluir: ${error.message}`, "error");
                    
                    // Se estiver offline, armazenar para sincronização posterior
                    if (!isOnline) {
                        pendingChanges[`clientes/${id}`] = null; // null marca para remoção
                        updateConnectionStatus();
                        
                        showToast("Exclusão armazenada localmente e será sincronizada quando houver conexão.", "warning");
                        
                        // Remover localmente da array de clientes para atualização da UI
                        clientes = clientes.filter(c => c.id !== id);
                        renderClientesList();
                    }
                });
        }

        // Função para abrir modal de produto
        function openProdutoModal(produto = null) {
            const modal = document.getElementById('produtoModal');
            const form = document.getElementById('produtoForm');
            const title = document.getElementById('produtoModalTitle');
            
            if (produto) {
                title.textContent = 'Editar Produto';
                document.getElementById('produtoId').value = produto.id;
                document.getElementById('nomeProduto').value = produto.nome;
                document.getElementById('precoProduto').value = produto.preco;
            } else {
                title.textContent = 'Cadastrar Novo Produto';
                form.reset();
                document.getElementById('produtoId').value = '';
            }
            
            modal.classList.remove('hidden');
        }

        // Função para salvar produto
        function saveProduto() {
            const id = document.getElementById('produtoId').value;
            const nome = document.getElementById('nomeProduto').value;
            const preco = parseFloat(document.getElementById('precoProduto').value);
            
            if (!nome || isNaN(preco) || preco <= 0) {
                showToast('Preencha os campos corretamente.', 'error');
                return;
            }
            
            const produtoData = {
                nome,
                preco
            };
            
            if (id) {
                // Editar produto existente
                db.ref(`produtos/${id}`).update(produtoData)
                    .then(() => {
                        showToast("Produto atualizado com sucesso!", "success");
                        document.getElementById('produtoModal').classList.add('hidden');
                    })
                    .catch(error => {
                        showToast(`Erro ao atualizar: ${error.message}`, "error");
                        
                        if (!isOnline) {
                            pendingChanges[`produtos/${id}`] = produtoData;
                            updateConnectionStatus();
                            
                            showToast("Alterações armazenadas localmente e serão sincronizadas quando houver conexão.", "warning");
                            document.getElementById('produtoModal').classList.add('hidden');
                        }
                    });
            } else {
                // Novo produto
                db.ref('produtos').push(produtoData)
                    .then(() => {
                        showToast("Produto cadastrado com sucesso!", "success");
                        document.getElementById('produtoModal').classList.add('hidden');
                    })
                    .catch(error => {
                        showToast(`Erro ao cadastrar: ${error.message}`, "error");
                        
                        if (!isOnline) {
                            const produtoKey = `produto_temp_${Date.now()}`;
                            pendingChanges[`produtos/${produtoKey}`] = produtoData;
                            updateConnectionStatus();
                            
                            showToast("Produto armazenado localmente e será sincronizado quando houver conexão.", "warning");
                            document.getElementById('produtoModal').classList.add('hidden');
                        }
                    });
            }
        }

        // Função para renderizar lista de produtos
        function renderProdutosList() {
            const tbody = document.getElementById('produtosList');
            tbody.innerHTML = '';
            
            produtos.forEach(produto => {
                const tr = document.createElement('tr');
                
                const tdNome = document.createElement('td');
                tdNome.className = 'px-4 py-2 border-b dark:border-gray-700';
                tdNome.textContent = produto.nome;
                
                const tdPreco = document.createElement('td');
                tdPreco.className = 'px-4 py-2 border-b dark:border-gray-700 text-right';
                tdPreco.textContent = `R$ ${parseFloat(produto.preco).toFixed(2)}`;
                
                const tdAcoes = document.createElement('td');
                tdAcoes.className = 'px-4 py-2 border-b dark:border-gray-700 text-center';
                
                const btnEdit = document.createElement('button');
                btnEdit.className = 'text-blue-500 hover:text-blue-700 mr-2';
                btnEdit.innerHTML = '<i class="fas fa-edit"></i>';
                btnEdit.title = 'Editar produto';
                btnEdit.addEventListener('click', () => {
                    openProdutoModal(produto);
                });
                
                const btnDelete = document.createElement('button');
                btnDelete.className = 'text-red-500 hover:text-red-700';
                btnDelete.innerHTML = '<i class="fas fa-trash"></i>';
                btnDelete.title = 'Excluir produto';
                btnDelete.addEventListener('click', () => {
                    if (confirm(`Deseja realmente excluir o produto ${produto.nome}?`)) {
                        deleteProduto(produto.id);
                    }
                });
                
                tdAcoes.appendChild(btnEdit);
                tdAcoes.appendChild(btnDelete);
                
                tr.appendChild(tdNome);
                tr.appendChild(tdPreco);
                tr.appendChild(tdAcoes);
                
                tbody.appendChild(tr);
            });
        }

        // Função para deletar produto
        function deleteProduto(id) {
            db.ref(`produtos/${id}`).remove()
                .then(() => {
                    showToast("Produto excluído com sucesso!", "success");
                })
                .catch(error => {
                    showToast(`Erro ao excluir: ${error.message}`, "error");
                    
                    if (!isOnline) {
                        pendingChanges[`produtos/${id}`] = null; // null marca para remoção
                        updateConnectionStatus();
                        
                        showToast("Exclusão armazenada localmente e será sincronizada quando houver conexão.", "warning");
                        
                        // Remover localmente da array de produtos para atualização da UI
                        produtos = produtos.filter(p => p.id !== id);
                        renderProdutosList();
                    }
                });
        }

        // Detectar quando a aplicação fica online/offline
        window.addEventListener('online', () => {
            isOnline = true;
            updateConnectionStatus();
            
            // Tentar sincronizar alterações pendentes
            if (Object.keys(pendingChanges).length > 0) {
                showToast("Conexão restabelecida. Sincronizando alterações pendentes...", "info");
                syncChangesToServer();
            }
        });

        window.addEventListener('offline', () => {
            isOnline = false;
            updateConnectionStatus();
            showToast("Você está offline. As alterações serão armazenadas localmente.", "warning");
        });
    </script>
</body>
</html>
