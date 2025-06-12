class GrafoRotas:
    def __init__(self):
        self.grafo = {} # Dicionário: {cidade: [(destino, peso), ...]}

    def adicionar_cidade(self, cidade):
        if cidade not in self.grafo:
            self.grafo[cidade] = []
            print(f"Cidade '{cidade}' adicionada.")
        else:
            print(f"Cidade '{cidade}' já existe.")

    def adicionar_rota(self, origem, destino, peso):
        if origem not in self.grafo:
            print(f"Erro: Cidade de origem '{origem}' não existe.")
            return
        if destino not in self.grafo:
            print(f"Erro: Cidade de destino '{destino}' não existe.")
            return

        # Adiciona rota bidirecional
        self.grafo[origem].append((destino, peso))
        self.grafo[destino].append((origem, peso)) # Se a rota é bidirecional
        print(f"Rota de '{origem}' para '{destino}' (peso: {peso}) adicionada.")

    def listar_cidades(self):
        if not self.grafo:
            print("Nenhuma cidade cadastrada.")
            return
        print("\nCidades Cadastradas:")
        for cidade in self.grafo:
            print(f"- {cidade}")

    def listar_rotas_de_cidade(self, cidade):
        if cidade not in self.grafo:
            print(f"Cidade '{cidade}' não encontrada.")
            return
        
        rotas = self.grafo[cidade]
        if not rotas:
            print(f"Nenhuma rota saindo de '{cidade}'.")
            return
        
        print(f"\nRotas saindo de '{cidade}':")
        for destino, peso in rotas:
            print(f"  -> {destino} (Peso: {peso})")

    def encontrar_caminho_simples(self, inicio, fim):
        # Implementar BFS/DFS aqui para encontrar um caminho
        # Retorna True/False e o caminho se encontrado
        pass

    def encontrar_melhor_rota_dijkstra(self, inicio, fim):
        # Implementar algoritmo de Dijkstra aqui
        # Retorna a distância total e o caminho mais curto
        pass

    def remover_cidade(self, cidade):
        if cidade not in self.grafo:
            print(f"Cidade '{cidade}' não encontrada.")
            return
        
        del self.grafo[cidade] # Remove a cidade

        # Remove todas as rotas que levam à cidade removida
        for c in self.grafo:
            self.grafo[c] = [(d, p) for d, p in self.grafo[c] if d != cidade]
        
        print(f"Cidade '{cidade}' e suas rotas associadas removidas.")

    def remover_rota(self, origem, destino):
        if origem not in self.grafo or destino not in self.grafo:
            print("Erro: Cidade de origem ou destino não encontrada.")
            return
        
        # Remove a rota de origem para destino
        self.grafo[origem] = [(d, p) for d, p in self.grafo[origem] if d != destino]
        # Remove a rota de destino para origem (se bidirecional)
        self.grafo[destino] = [(d, p) for d, p in self.grafo[destino] if d != origem]
        print(f"Rota entre '{origem}' e '{destino}' removida.")

def exibir_menu():
    print("\n--- Gerenciador de Rotas ---")
    print("1. Adicionar Cidade")
    print("2. Adicionar Rota")
    print("3. Listar Cidades")
    print("4. Listar Rotas de uma Cidade")
    print("5. Encontrar Melhor Rota (Dijkstra)") # Ou Caminho Simples
    print("6. Remover Cidade")
    print("7. Remover Rota")
    print("8. Sair")
    print("--------------------------")

def main():
    gerenciador = GrafoRotas()

    while True:
        exibir_menu()
        escolha = input("Escolha uma opção: ")

        if escolha == '1':
            cidade = input("Digite o nome da cidade: ")
            gerenciador.adicionar_cidade(cidade)
        elif escolha == '2':
            origem = input("Cidade de origem: ")
            destino = input("Cidade de destino: ")
            try:
                peso = float(input("Peso da rota (distância/tempo): "))
                gerenciador.adicionar_rota(origem, destino, peso)
            except ValueError:
                print("Peso inválido. Digite um número.")
        elif escolha == '3':
            gerenciador.listar_cidades()
        elif escolha == '4':
            cidade = input("Digite o nome da cidade para listar as rotas: ")
            gerenciador.listar_rotas_de_cidade(cidade)
        elif escolha == '5':
            origem = input("Cidade de partida: ")
            destino = input("Cidade de chegada: ")
            # gerenciador.encontrar_melhor_rota_dijkstra(origem, destino)
            # Ou gerenciador.encontrar_caminho_simples(origem, destino)
            print("Funcionalidade de busca de rota a ser implementada.") # Placeholder
        elif escolha == '6':
            cidade = input("Digite o nome da cidade a ser removida: ")
            gerenciador.remover_cidade(cidade)
        elif escolha == '7':
            origem = input("Cidade de origem da rota a ser removida: ")
            destino = input("Cidade de destino da rota a ser removida: ")
            gerenciador.remover_rota(origem, destino)
        elif escolha == '8':
            print("Saindo da aplicação.")
            break
        else:
            print("Opção inválida. Tente novamente.")

if __name__ == "__main__":
    main()
