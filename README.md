clientes = []

def adicionar_cliente():
    nome = input("Digite o nome do cliente: ")
    endereco = input("Digite o endereço: ")
    telefone = input("Digite o telefone: ")
    tipo_acesso = input("Digite o tipo de acesso (admin/usuario/visitante): ")

    cliente = {
        "nome": nome,
        "endereco": endereco,
        "telefone": telefone,
        "tipo_acesso": tipo_acesso
    }

    clientes.append(cliente)
    print("\n✅ Cliente adicionado com sucesso!\n")

def listar_clientes():
    if not clientes:
        print("\n⚠ Nenhum cliente cadastrado!\n")
    else:
        for i, c in enumerate(clientes, start=1):
            print(f"{i}. {c['nome']} | {c['endereco']} | {c['telefone']} | {c['tipo_acesso']}")
        print()

def menu():
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
            print("Opção inválida! Tente novamente.\n")

menu()
