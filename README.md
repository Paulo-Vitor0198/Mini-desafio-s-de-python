# Mini-desafio-s-de-python

# Jogo de luta injusta
from random import randint
from time import sleep

life_player = 500
ataques = []
ataquesb = []
dados = []


def CarregarProgresso(carregando):
    global ataques
    print("CARREGANDO......")
    barra()
    clear()
    sleep(1.5)
    print(f"{carregando}arregando o jogo salvo ")
    somac = contc = vidac = 0
    inteiros = []
    asave = open('salvo.txt', 'r')
    r = asave.readlines()
    for loading in r:
        dados.append(loading)

    asave.close()
    for c in dados:
        r = int(c)
        inteiros.append(r)
    for n in range(len(inteiros)):
        if inteiros[0]:
            life_save = inteiros[0]
        if inteiros[1]:
            n_inimigos = inteiros[1]
        if inteiros[2]:
            it_cura = inteiros[2]
    clear()
    sleep(1.5)
    print("NO JOGO QUE FOI CARREGADO: ")
    while True:
        barra()
        print(f"\nVida:  {life_save}"
              f"\nitens de cura: {it_cura}")
        opc = input("vai querer atacar(a), curar(c), salvar e sair(ss), (sc)salvar e continuar ou desistir(d)?  ").upper().strip()
        clear()
        barra()
        if opc == "C":
            it_cura -= 10
            life_save += randint(0, 16)
            print(f"\n NAO DISPERDICE SUA POÇÃO DE CURA!, USE QUANDO NECESSARIO"
                  f"\nvida: {life_save}"
                  f"\npoção de cura: {it_cura} ")
        if opc == "A":
            print(f"vida: {life_save}"
                  f"\npoção de cura: {it_cura} ")
            barra()
            print(f"INICIO DO COMBATE, ROUND {contc + 1}, FIGHT!!!")
            barra()
            dano = randint(0, 20)
            atk = randint(0, n_inimigos)
            ataques.append(dano)
            if contc > 0:
                somac = sum(ataques)
            if somac >= 50:
                n_inimigos -= 1
                ataques.clear()
            print(f"Voce causou ao inimigo {atk + 1} voce causou {dano} de dano")
            print("---" * 5)
            for ataque in range(n_inimigos):
                print()
                danoa = randint(0, 7)
                if danoa == 0:
                    print(f"o inimigo {ataque + 1} errou!!")
                    barra()
                else:
                    print(f"o inimigo {ataque + 1} causou {danoa} de dano")
                    barra()
                    danoa += vidac
                life_save = life_save - dano
            contc += 1
        if n_inimigos < 0:
            print("VOCE VENCEU A BATALHA NA ARENA, VOCE É UM GUERREIRO DIGNO DE TODAS AS HONRAS!!")

        if life_save < 0:
            barra()
            print("VOCE FOI ANIQUILADO...MUAHMUAHMUAHMUAHMUAH"
                  "\nGAME OVER! SEU INCOPETENTE, AO MENOS NAO DESISTIU")
            return
        if opc == 'D':
            print("MUAHMUAHMUAHMUAHMUHA....."
                  "\nDESISTIR?..HM\n FRACOTE, SUMA DAQUI!!!! ")
            Entrada()
            print()
            return
        if opc == 'SS':
            return save(life_save, n_inimigos, it_cura)
        if opc == "SC":
            asave = open('salvo.txt', 'w')
            asave.writelines(f"{life_save}\n")
            asave.writelines(f"{n_inimigos}\n")
            asave.writelines(f"{it_cura}\n")

            asave.close()

def save(qvida, qinimigos, qcura):
    asave = open('salvo.txt', 'w')
    asave.writelines(f"{qvida}\n")
    asave.writelines(f"{qinimigos}\n")
    asave.writelines(f"{qcura}\n")

    asave.close()


    Entrada()




def clear(times=50):
    if isinstance(times, int):
        for i in range(times):
            print()


def barra():
    print("-=-=-" * 15)


def JogoNovo(novo):
    global life_player
    vida = cont = soma = 0
    cura = 100
    print(f"---={novo}OVO JOGO=---")
    print()
    barra()
    inimigos = int(input("Quantos inimigos vai querer enfrentar? "))
    print("Jogo em carregamento............")
    sleep(1.5)
    clear()
    sleep(0.5)
    if inimigos == 1:
        print("VOCE É UM FRACO, DIGNO DE PENA AO MENOS ESCOLHA DOIS INIMIGOS OU TRES OPONENTES SEU FRACOTE!!!!!"
              "\n ASSIM NA MINHA ARENA VOCE NAO LUTA, SEU VIRJAO DO CARALHOOO!!"
              "\n -=-=-=-=-=-=-=-=-=-=-=-==-==-=-=-=-=-=-==-=-=-=-=-=-=-=-")
        return JogoNovo(novo)
    while True:
        opc = input("vai querer atacar(a), curar(c), salvar e sair(sp), Salvar e continuar (sp) ou desistir(d)?  ").upper().strip()

        print()
        if opc == "C":
            cura -= 10
            life_player += randint(0, 16)
            print(f"\n NAO DISPERDICE SUA POÇÃO DE CURA!, USE QUANDO NECESSARIO"
                  f"\nvida: {life_player}"
                  f"\npoção de cura: {cura} ")
        if opc == "A":
            print(f"vida: {life_player}"
                  f"\npoção de cura: {cura} ")
            barra()
            print(f"INICIO DO COMBATE, ROUND {cont + 1}, FIGHT!!!")
            barra()
            danoini = randint(0, 20)
            atkop = randint(0, inimigos)
            ataques.append(danoini)
            if cont > 0:
                soma = sum(ataques)
            if soma >= 50:
                inimigos -= 1
                ataques.clear()
            print(f"Voce causou ao inimigo {atkop + 1} voce causou {danoini} de dano")
            print("---" * 5)
            for ataque in range(inimigos):
                print()
                dano = randint(0, 7)
                if dano == 0:
                    print(f"o inimigo {ataque + 1} errou!!")
                    barra()
                else:
                    print(f"o inimigo {ataque + 1} causou {dano} de dano")
                    barra()
                    dano += vida
                life_player = life_player - dano
            cont += 1
        if inimigos < 0:
            print("VOCE VENCEU A BATALHA NA ARENA, VOCE É UM GUERREIRO DIGNO DE TODAS AS HONRAS!!")

        if life_player < 0:
            barra()
            print("VOCE FOI ANIQUILADO...MUAHMUAHMUAHMUAHMUAH"
                  "\nGAME OVER! SEU INCOPETENTE, AO MENOS NAO DESISTIU")
            return
        if opc == 'D':
            print("MUAHMUAHMUAHMUAHMUHA....."
                  "\nDESISTIR?..HM\n FRACOTE, SUMA DAQUI!!!! ")
            Entrada()
            print()
            return
        if opc == 'SS':
            return save(life_player, inimigos, cura)
        if opc == "SC":
            asave = open('salvo.txt', 'w')
            asave.writelines(f"{vida}\n")
            asave.writelines(f"{inimigos}\n")
            asave.writelines(f"{cura}\n")

            asave.close()


def Entrada():
    while True:
        barra()
        print("JOGO DA BATALHA INJUSTA")
        barra()
        inicio = str(input("Vai querer carregar sua ultima campanha(c), iniciar um jogo novo(n) ou vai querer sair(e)? ")).upper().strip()
        barra()
        if inicio == "N":
            return JogoNovo(inicio)
        if inicio == "C":
            return CarregarProgresso(inicio)
        if inicio == "E":
            print("FIM DO GAME!")



Entrada()
