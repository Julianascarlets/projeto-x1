import json
import os

ARQUIVO = "clientes.json"
clientes = []

# Função para carregar clientes do arquivo
def carregar_clientes():
    global clientes
    if os.path.exists(ARQUIVO):
        with open(ARQUIVO, "r", encoding="utf-8") as f:
            clientes = json.load(f)
    else:
        clientes = []

# Função para salvar clientes no arquivo
def salvar_clientes():
    with open(ARQUIVO, "w", encoding="utf-8") as f:
        json.dump(clientes, f, indent=4, ensure_ascii=False)

def adicionar_cliente():
    print("\n=== CADASTRO DE CLIENTE ===")
    nome = input("Nome do cliente: ")
    endereco = input("Endereço: ")
    telefone = input("Telefone: ")
    tipo_acesso = input("Tipo de acesso (admin/usuario/visitante): ")

    # Campos financeiros
    objetivo = input("O que o cliente quer fazer (objetivo): ")
    investimento = input("Quanto deseja investir: ")
    perdas = input("Principais perdas esperadas: ")
    ganhos = input("Principais ganhos esperados: ")

    cliente = {
        "nome": nome,
        "endereco": endereco,
        "telefone": telefone,
        "tipo_acesso": tipo_acesso,
        "objetivo": objetivo,
        "investimento": investimento,
        "perdas": perdas,
        "ganhos": ganhos
    }

    clientes.append(cliente)
    salvar_clientes()
    print("\n✅ Cliente adicionado com sucesso!\n")

def listar_clientes():
    if not clientes:
        print("\n⚠ Nenhum cliente cadastrado!\n")
    else:
        print("\n=== LISTA DE CLIENTES ===")
        for i, c in enumerate(clientes, start=1):
            print(f"{i}. {c['nome']} | {c['telefone']} | Investimento: {c['investimento']}")
            print(f"   Objetivo: {c['objetivo']}")
            print(f"   Perdas: {c['perdas']} | Ganhos: {c['ganhos']}")
            print("-" * 40)
        print()

def menu():
    carregar_clientes()
    while True:
        print("===== MENU =====")
        print("1 - Adicionar cliente")
        print("2 - Listar clientes")
        print("3 - Sair")
        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            adicionar_cliente()
        elif opcao == "2":
            listar_clientes()
        elif opcao == "3":
            print("Saindo do programa...")
            break
        else:
            print("⚠ Opção inválida! Tente novamente.\n")

# Executa o programa
menu()
