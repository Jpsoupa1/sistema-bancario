# sistema-bancario
menu = """
=====================
    [d] Depositar
    [s] Sacar
    [e] Extrato
    [q] Sair
====================
==> """

saldo = 0
limite = 500
extrato = ""
numero_saques = 0
LIMITES_SAQUES = 3

def deposito():
    global saldo, extrato
    valor_deposito = float(input("Valor do depósito: "))
    if valor_deposito < 100:
         print("Valor inválido! Insira um valor acima de R$ 100,00.")
    else:
         saldo += valor_deposito
         extrato += f"Depósito: R$ {valor_deposito:.2f}\n"
         print(f"Depósito realizado com sucesso! O valor de R$ {valor_deposito:.2f} foi depositado na sua conta.")
         print(f"Saldo: R$ {saldo:.2f}")

def sacar():
    global saldo, extrato, numero_saques
    valor_saque = float(input("Valor do saque: "))
    if valor_saque > saldo:
         print("Saldo insuficiente para realizar o saque.")
    elif valor_saque > limite:
         print(f"Impossível realizar o saque. O limite de saque é de R$ {limite:.2f}.")
    elif numero_saques >= LIMITES_SAQUES:
         print("Limite de saques excedido.")
    else:
         saldo -= valor_saque
         numero_saques += 1
         extrato += f"Saque: R$ {valor_saque:.2f}\n"
         print(f"Saque no valor de R$ {valor_saque:.2f} realizado com sucesso.")
         print(f"Saldo atual: R$ {saldo:.2f}")

def exibir_extrato():
    print("""
    ------------- Extrato ------------""")
    print(extrato if extrato else "Nenhuma movimentação realizada.")
    print(f"Saldo atual: R$ {saldo:.2f}")
    print("---------------------------------\n")

while True:
    opcao = input(menu)

    if opcao == "d":
        print(""""
  ------------ Depósito ----------""")
        deposito()
    elif opcao == "s":
        print("""
  ------------ Saque ------------""")
        sacar()
    elif opcao == "e":
        exibir_extrato()
    elif opcao == "q":
        print("Saindo...")
        break
    else:
        print("Operação inválida, por favor selecione novamente a opção desejada.")
