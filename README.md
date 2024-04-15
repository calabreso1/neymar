# neymar
repositório das aulas de poo.
# Definindo a classe Produto
class Produto:
    # Método de inicialização
    def __init__(self, nome, preco, descricao, disponibilidade):
        self.nome = nome  # Atributo nome do produto
        self.preco = preco  # Atributo preço do produto
        self.descricao = descricao  # Atributo descrição do produto
        self.disponibilidade = disponibilidade  # Atributo de disponibilidade do produto

    # Método para atualizar a disponibilidade do produto
    def atualizar_disponibilidade(self, disponibilidade):
        self.disponibilidade = disponibilidade

    # Método para representar o produto como uma string
    def __str__(self):
        return f"{self.nome} - R${self.preco:.2f}"

# Definindo a classe Pagamento
class Pagamento:
    # Método de inicialização
    def __init__(self, metodo, valor):
        self.metodo = metodo  # Atributo método de pagamento
        self.valor = valor  # Atributo valor do pagamento

    # Método para processar o pagamento
    def processar_pagamento(self):
        # Lógica para processar o pagamento
        print(f"Processando pagamento de R${self.valor:.2f} via {self.metodo}")

# Definindo a classe Entrega
class Entrega:
    # Método de inicialização
    def __init__(self, endereco, custo, data_prevista):
        self.endereco = endereco  # Atributo endereço de entrega
        self.custo = custo  # Atributo custo de entrega
        self.data_prevista = data_prevista  # Atributo data prevista de entrega

    # Método para agendar a entrega
    def agendar_entrega(self):
        # Lógica para agendar a entrega
        print(f"Entrega agendada para {self.data_prevista} no endereço {self.endereco}")

# Definindo a classe Usuario
class Usuario:
    # Método de inicialização
    def __init__(self, nome, email, senha):
        self.nome = nome  # Atributo nome do usuário
        self.email = email  # Atributo email do usuário
        self.senha = senha  # Atributo senha do usuário

    # Método para fazer login
    def fazer_login(self):
        # Lógica para fazer login
        print(f"Bem-vindo, {self.nome}!")

# Definindo a classe Cliente, que herda de Usuario
class Cliente(Usuario):
    # Método de inicialização
    def __init__(self, nome, email, senha, endereco, cpf):
        super().__init__(nome, email, senha)  # Chamada ao método de inicialização da classe pai
        self.endereco = endereco  # Atributo endereço do cliente
        self.cpf = cpf  # Atributo CPF do cliente

    # Método para realizar uma compra
    def realizar_compra(self, produtos, pagamento, entrega):
        compra = Compra(self, produtos, pagamento, entrega)  # Criando uma nova compra
        # Lógica para finalizar a compra
        print("Compra realizada com sucesso!")
        return compra

# Definindo a classe Funcionario, que herda de Usuario
class Funcionario(Usuario):
    # Método de inicialização
    def __init__(self, nome, email, senha, cargo, salario):
        super().__init__(nome, email, senha)  # Chamada ao método de inicialização da classe pai
        self.cargo = cargo  # Atributo cargo do funcionário
        self.salario = salario  # Atributo salário do funcionário

    # Método para processar uma compra
    def processar_compra(self, compra):
        # Lógica para processar a compra
        print(f"Compra de {compra.cliente.nome} processada por {self.nome}")

# Definindo a classe Compra
class Compra:
    # Método de inicialização
    def __init__(self, cliente, produtos, pagamento, entrega):
        self.cliente = cliente  # Atributo cliente da compra
        self.produtos = produtos  # Atributo lista de produtos da compra
        self.pagamento = pagamento  # Atributo pagamento da compra
        self.entrega = entrega  # Atributo entrega da compra

    # Método para imprimir um resumo da compra
    def resumo_compra(self):
        print("Resumo da compra:")
        print("Produtos:")
        for produto in self.produtos:
            print(f"- {produto}")  # Imprime cada produto da compra
        print(f"Total: R${sum(produto.preco for produto in self.produtos):.2f}")  # Calcula e imprime o total
        print("Pagamento:")
        print(f"- Método: {self.pagamento.metodo}")  # Imprime o método de pagamento
        print(f"- Valor: R${self.pagamento.valor:.2f}")  # Imprime o valor do pagamento
        print("Entrega:")
        print(f"- Endereço: {self.entrega.endereco}")  # Imprime o endereço de entrega
        print(f"- Data prevista: {self.entrega.data_prevista}")  # Imprime a data prevista de entrega

# Exemplo de utilização:

# Criando alguns produtos
produto1 = Produto("Camiseta", 29.99, "Camiseta de algodão", True)
produto2 = Produto("Calça Jeans", 49.99, "Calça jeans slim", True)

# Criando um cliente
cliente1 = Cliente("João", "joao@email.com", "senha123", "Rua A, 123", "123.456.789-00")

# Criando um pagamento
pagamento1 = Pagamento("Cartão de Crédito", 79.98)

# Criando uma entrega
entrega1 = Entrega("Rua B, 456", 10.0, "15/04/2024")

# Realizando uma compra
compra1 = cliente1.realizar_compra([produto1, produto2], pagamento1, entrega1)
compra1.resumo_compra()
