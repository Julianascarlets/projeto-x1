const fs = require("fs");
const prompt = require("prompt-sync")();

const ARQUIVO = "clientes.json";
let clientes = [];

// Carregar clientes do arquivo
function carregarClientes() {
    if (fs.existsSync(ARQUIVO)) {
        const dados = fs.readFileSync(ARQUIVO, "utf-8");
        clientes = JSON.parse(dados);
    } else {
        clientes = [];
    }
}

// Salvar clientes no arquivo
function salvarClientes() {
    fs.writeFileSync(ARQUIVO, JSON.stringify(clientes, null, 4), "utf-8");
}

// Criar cliente
function adicionarCliente() {
    console.log("\n=== CADASTRO DE CLIENTE ===");
    const nome = prompt("Nome do cliente: ");
    const endereco = prompt("Endereço: ");
    const telefone = prompt("Telefone: ");
    const tipoAcesso = prompt("Tipo de acesso (admin/usuario/visitante): ");

    const objetivo = prompt("O que o cliente quer fazer (objetivo): ");
    const investimento = prompt("Quanto deseja investir: ");
    const perdas = prompt("Principais perdas esperadas: ");
    const ganhos = prompt("Principais ganhos esperados: ");

    const cliente = {
        nome,
        endereco,
        telefone,
        tipoAcesso,
        objetivo,
        investimento,
        perdas,
        ganhos
    };

    clientes.push(cliente);
    salvarClientes();
    console.log("\n✅ Cliente adicionado com sucesso!\n");
}

// Listar clientes
function listarClientes() {
    if (clientes.length === 0) {
        console.log("\n⚠ Nenhum cliente cadastrado!\n");
    } else {
        console.log("\n=== LISTA DE CLIENTES ===");
        clientes.forEach((c, i) => {
            console.log(`${i + 1}. ${c.nome} | ${c.telefone} | Investimento: ${c.investimento}`);
            console.log(`   Objetivo: ${c.objetivo}`);
            console.log(`   Perdas: ${c.perdas} | Ganhos: ${c.ganhos}`);
            console.log("-".repeat(40));
        });
    }
}

// Atualizar cliente
function atualizarCliente() {
    listarClientes();
    if (clientes.length === 0) return;

    const indice = parseInt(prompt("Digite o número do cliente para atualizar: ")) - 1;
    if (indice < 0 || indice >= clientes.length) {
        console.log("⚠ Cliente não encontrado!");
        return;
    }

    let cliente = clientes[indice];

    console.log("\n=== ATUALIZAR CLIENTE === (pressione Enter para manter o valor atual)");
    const nome = prompt(`Nome (${cliente.nome}): `) || cliente.nome;
    const endereco = prompt(`Endereço (${cliente.endereco}): `) || cliente.endereco;
    const telefone = prompt(`Telefone (${cliente.telefone}): `) || cliente.telefone;
    const tipoAcesso = prompt(`Tipo de acesso (${cliente.tipoAcesso}): `) || ("cliente.tipoAcesso");
    const objetivo = prompt(`Objetivo (${cliente.objetivo}): `) || cliente.objetivo;
    const investimento = prompt(`Investimento (${cliente.investimento}): `) || cliente.investimento;
    const perdas = prompt(`Perdas (${cliente.perdas}): `) || cliente.perdas;
    const ganhos = prompt(`Ganhos (${cliente.ganhos}): `) || cliente.ganhos;

    clientes[indice] = { nome, endereco, telefone, tipoAcesso, objetivo, investimento, perdas, ganhos };
    salvarClientes();
    console.log("\n✅ Cliente atualizado com sucesso!\n");
}

// Excluir cliente
function excluirCliente() {
    listarClientes();
    if (clientes.length === 0) return;

    const indice = parseInt(prompt("Digite o número do cliente para excluir: ")) - 1;
    if (indice < 0 || indice >= clientes.length) {
        console.log("⚠ Cliente não encontrado!");
        return;
    }

    const clienteRemovido = clientes.splice(indice, 1);
    salvarClientes();
    console.log(`\n🗑 Cliente "${clienteRemovido[0].nome}" excluído com sucesso!\n`);
}

// Menu principal
function menu() {
    carregarClientes();
    while (true) {
        console.log("\n===== MENU =====");
        console.log("1 - Adicionar cliente");
        console.log("2 - Listar clientes");
        console.log("3 - Atualizar cliente");
        console.log("4 - Excluir cliente

        console.log("5 - Sair");

        const opcao = prompt("Escolha uma opção: ");

        if (opcao === "1") {
            adicionarCliente();
        } else if (opcao === "2") {
            listarClientes();
        } else if (opcao === "3") {
            atualizarCliente();
        } else if (opcao === "4") {
            excluirCliente();
        } else if (opcao === "5") {
            console.log("Saindo do programa...");
            break;
        } else {
            console.log("⚠ Opção inválida! Tente novamente.\n");
        }
    }
}

// Executar programa
Menu();
