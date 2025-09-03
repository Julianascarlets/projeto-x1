const fs = require("fs");
const prompt = require("prompt-sync")();

const ARQUIVO = "clientes.json";
let clientes = [];

// Carregar clientes do arquivo
function carregarClientes() {
    if (fs.existsSync(ARQUIVO)) {
        const data = fs.readFileSync(ARQUIVO, "utf-8");
        clientes = JSON.parse(data);
    } else {
        clientes = [];
    }
}

// Salvar clientes no arquivo
function salvarClientes() {
    fs.writeFileSync(ARQUIVO, JSON.stringify(clientes, null, 4), "utf-8");
}

function adicionarCliente() {
    console.log("\n=== CADASTRO DE CLIENTE ===");
    const nome = prompt("Nome do cliente: ");
    const endereco = prompt("Endereço: ");
    const telefone = prompt("Telefone: ");
    const tipoAcesso = prompt("Tipo de acesso (admin/usuario/visitante): ");

    // Campos financeiros
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

function menu() {
    carregarClientes();
    while (true) {
        console.log("===== MENU =====");
        console.log("1 - Adicionar cliente");
        console.log("2 - Listar clientes");
        console.log("3 - Sair");
        const opcao = prompt("Escolha uma opção: ");

        if (opcao === "1") {
            adicionarCliente();
        } else if (opcao === "2") {
            listarClientes();
        } else if (opcao === "3") {
            console.log("Saindo do programa...");
            break;
        } else {
            console.log("⚠ Opção inválida! Tente novamente.\n");
        }
    }
}

// Executar programa
menu();
