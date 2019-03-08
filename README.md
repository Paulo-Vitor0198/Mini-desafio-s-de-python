# Mini-desafio-s-de-python, Refeito com coisas novas que aprendi 

import dbm
import random


class Game:
    def __init__(self):
        self.dados = {}
        self.file = dbm.open("Game", "c")
        self.nome = " "
        self.SPplayer = 100
        self.seif = 20
        self.fortaleza = 20
        self.player = 500
        self.ogro = 100
        self.ogroSP = 5
        self.goblin = 70
        self.goblinSP = 10
        self.esqueleto = 80
        self.esqueletoSP = 20
        self.bruxo = 80
        self.bruxoSP = 20
        self.pontuaçao = 0
        self.MainMenu()

    def MainMenu(self):

        while True:
            try:
                menu = input("Menu: carregar jogo(C), criar um novo jogo(N) ou sair(S): ").upper().strip()
                if menu.startswith("N"):
                    self.nome = input("Seu nome jogador: ")

                    self.dados["nome"] = self.nome
                    print(f"Bom {self.nome}, o Jogo funciona assim, O inimigo é escolhido automaticamente\n"
                          f" se tu ganhar uma batalha tem direito de aumentar atributos de força ou sp, ou voce poder restaurar toda a vida\n"
                          f"existem 4 inimigos em potencial")
                    print("-=--= " * 15)
                    return self.NovoJogo()
                elif menu.startswith("C"):
                    return self.carregarGame()
            except IndexError as E:
                print(E)
            else:
                print("Opçao Invalida, tente novamente.")

    def NovoJogo(self):
        """Metodo responsavel por levar o usurio a batalha, a escolha do inimigo ,de forma random, onde o usuario nao escolhe o inimigo, mas o metodo que escolhe,
         alem de aqui sair o numero referente a cada inimigo de 1 a 4, tambem o usuario pode escolher jogar, salvar e sair:
         inimigo --> numero aleatoriamente escolhido pelo metodo para o usuruio enfrentar
         atk => onde o usuario colocara a entrada referente a Ataque(A), desistir(D) e Salvar(S)"""
        inimigo = random.randint(1, 4)
        while True:
            print("-=-=-" * 15)
            print(f"nome: {self.nome}\n"
                  f"Life: {self.player}\n"
                  f"Poder: {self.SPplayer}\n"
                  f"Defesa: {self.seif}\n"
                  f"Força: {self.fortaleza}")
            atk = input("vai querr atacar(A), Vai querer desissitir(D) ou vai salvar(S)?").upper().strip()
            if inimigo == 1 and atk.startswith("A"):
                InimigoDefesa = 20
                print(f" Guerreiro Morto-Vivo: \n"
                      f"vida: {self.esqueleto}\n"
                      f"Poder: {self.esqueletoSP}\n"
                      f"Defesa: {InimigoDefesa}")

                self.batalha(InimigoDefesa, inimigo)
                self.DanonoPlayer(inimigo)

            elif inimigo == 2 and atk.startswith("A"):
                InimigoDefesa = 10
                print(f" Goblin das Montanhas \n"
                      f"vida: {self.goblin}\n"
                      f"Poder: {self.goblinSP}\n"
                      f"Defesa: {InimigoDefesa}")
                self.batalha(InimigoDefesa, inimigo)
                self.DanonoPlayer(inimigo)

            elif inimigo == 3 and atk.startswith("A"):
                InimigoDefesa = 30
                print(f" Mago-Anciao-Necromantico: \n"
                      f"vida: {self.bruxo}\n"
                      f"Poder: {self.bruxoSP}\n"
                      f"Defesa: {InimigoDefesa}")

                self.batalha(InimigoDefesa, inimigo)
                self.DanonoPlayer(inimigo)

            elif inimigo == 4 and atk.startswith("A"):
                InimigoDefesa = 5
                print(f" Demonio-Recem-transformado: \n"
                      f"vida: {self.ogro}\n"
                      f"Poder: {self.ogroSP}\n"
                      f"Defesa: {InimigoDefesa}")

                self.batalha(InimigoDefesa, inimigo)
                self.DanonoPlayer(inimigo)

            elif self.player <= 0:
                print("voce foi perdeu!")
            elif atk.startswith("D"):
                print("Voce desistiu")
                return
            elif atk.startswith("S"):
                self.salvaGame(inimigo)



            else:
                print("Opçao invalida")





    def batalha(self, DefRival, NossoRival):
        """Metodo responsavel por portar todas as condiçoes ternarias qu cada uma representa uma arma diferente e seus referentes danos, mas paaa o Usuario escolher as armas,
        pode deve seguir os requisitos de cada condicional, alem de subtrair o poder a medida que que o usuario escolha a arma que tem suas exigencias de poder
         PlayerSP - Poder do Usuario
         NossoRival = representa o numero que o usuario representa"""
        print("-=-=-" * 15)
        arma = input("escolha sua arma(ESPADA (E), LANÇA DE GELO (L), CLAVA (CL), METRALHADORA (B), CANHAO ELETRICO (R), ARCO DE MADEIRA (A)) ou deseja curar-se? ").upper().strip()
        if arma.startswith("E"):
            Forca = 20
            Espada = max((Forca - DefRival) * random.randint(0, 1), 1)
            self.DanonoInimigo(NossoRival, Espada)

        elif arma.startswith("A") and self.SPplayer >= 2:
            Forca = 20
            Flexada = max((Forca - DefRival / 3) * random.randint(0, 1), 1)
            self.SPplayer -= 2
            self.DanonoInimigo(NossoRival, Flexada)


        elif arma.startswith("CL"):
            Forca = 20
            Clavada = max((Forca - DefRival/1)*random.randint(0,1), 1)
            self.DanonoInimigo(NossoRival, Clavada)

        elif arma.startswith("R") and self.SPplayer >= 5:
            Forca = 20
            Relampago = max((Forca - DefRival / 5) * random.randint(0, 1), 1)
            self.SPplayer -= 5
            self.DanonoInimigo(NossoRival, Relampago)

        elif arma.startswith("B") and self.SPplayer >= 10:
            Forca = 20
            BolaDeFogo = max((Forca - DefRival / 5) * random.randint(0, 1), 1)
            self.SPplayer -= 10
            self.DanonoInimigo(NossoRival, BolaDeFogo)

        elif arma.startswith("L") and self.SPplayer >= 10:
            Forca = 20
            LancaDeGelo = max((Forca - DefRival / 5) * random.randint(0, 1), 1)
            self.SPplayer -= 10
            self.DanonoInimigo(NossoRival, LancaDeGelo)

        elif arma.startswith("CU") and self.SPplayer >= 10:
            self.player += 10
            self.SPplayer -= 10


        else:
            print("voce nao tem SP suficiente para usar esse poder")



    def DanonoPlayer(self, rival):
        """Esse metodo ja funciona da forma que vai calcular o dano que o usuario ira receber e sua life ira se reduzir subtriando a vida com o dano recebido
         player = vida do usurio
         Random dentro dos ifs -> representa o soreio a cada turno que cada inimigo ira usar"""
        print("-=-=-" * 15)
        print()
        if rival == 1:
            esque = random.randint(1, 2)
            if esque == 1:
                For = 20
                Espada = max((For - self.seif / 2) * random.randint(0, 1), 1)
                self.player -= Espada
                print(f"Voce tomou {Espada} de dano da Espada Amaldiçoada")
                print("\033[1;32mGuerreiro Morto-Vivo\033[m: HAHAHAHAHAHAHHAHAHAHA morra mortal")
            if esque == 2:
                self.esqueleto += 10
                self.esqueletoSP -= 10
                print("Guerreiro-Morto-Vivo usou magia amaldiçoada que so os mortos vivos podem usar para se recuperar")
        elif rival == 2:
            For = 15
            goblin = max((For - self.seif / 3) * random.randint(0, 1), 1)
            self.player -= goblin
            print(f"Voce tomou {goblin} de dano da clava de metal Necromantico")
            print("\033[1;32mGoblin das Montanhas\033:[m GYAGYAAHHAHA")
        elif rival == 3:
            bruxo = random.randint(1, 4)
            For = 10
            if bruxo == 1:
                Relampago = max((For - self.seif / 7) * random.randint(0, 1), 1)
                self.player -= Relampago
                print(f"\033[1;32mMago-Anciao-Necromantico\033[m: Eu invoco o raio das Trevassss, Morra aniquilado mortal..HAHAHAHAHA")
                print(F"Voce tomou  {Relampago} de dano do Raio das Traves ")
            elif bruxo == 2:
                BolaDeFogo = max((For - self.seif / 6) * random.randint(0, 1), 1)
                self.player -= BolaDeFogo
                print("\033[1;32mMago-Anciao=Necromantica\033[m: Sua alma sera torrda com as chamas, que traz os mortos a semi-vida, e os vivos a morte.. HAHAHA")
                print(f"Voce tomou {BolaDeFogo} de dano da Chama Necromantca")
            elif bruxo == 3:
                Espada = max((For - self.seif/ 3) * random.randint(0, 1), 1)
                self.player -= Espada
                print(f"\033[1;32mMago-Anciao-Necromantico\033[m: Sofrra com o poder da espada de meu Mestre Azazel HUAHUAHAUHAUA")
                print(f"Voce tomou {Espada} de dano da Espada-Sumonada do rei de Azazel")
            elif bruxo == 4:
                self.bruxoSP -= 10
                self.bruxo += 10
                self.player -= 10
                print("\033[1;32mMago-Anciao-Necromantico\033[m: vou e curar usando um pouco de sua alma, NECROMOTIUN SU MORTIS MI VITALIIII ")
                print("O MAGO-ANCIAO-NECROMANTICO recuperou 10 de vida, te dando 10 de dano,"
                      "\n com o uso de uma magia SATANICA que Recupera a vida devorando a sua alma")
        elif rival == 4:
            For = 30
            Clavada = max((For - self.seif/1)*random.randint(0,1), 1)
            self.player -= Clavada
            print("\033[1;32mDemonio Recem transformado\033[m:GYAGYAGYAGYAGYAGYAGYA")
            print(f"Voce tomou {Clavada} de dano das garras")

    def DanonoInimigo(self, QueInimigo, DanoNele):
        """Metodo responsavel calcular o dano que os inimigo tomam, o QueInimigos siginifica o numero do que o inimigo representa
        e o DanoNele, foi o dano calculado no metodo anterior, que sera subtraido com sua vida"""
        print("-=-=-" * 15)
        print()
        if QueInimigo == 1:
            self.esqueleto -= DanoNele
            print(f"\033[1;33mvoce causou ao Guerreiro Morto-Vivo {DanoNele} dano\033[m")
            if self.esqueleto <= 0:
                print("\033[1;33mGuerreiro-Moto-Vivo foi derrotado e sera aprisionado no limbo por tempo indeterminado,\n"
                      " ate sair novamente para causar medo e terror\033[m")
                self.pontuaçao += 1
                self.AtributosMais()
                return self.NovoJogo()
            else:
                print("<--->")
        elif QueInimigo == 2:
            self.goblin -= DanoNele
            print(f"\033[1;33mVoce causou ao Goblin das Montanhas {DanoNele} dano\033[m")
            if self.goblin <= 0:
                print("\033[1;33mGoblin das montanhas foi derrotado com honra, foi poupado por ser um guerreiro honrado\n"
                      ", mas jurou retotrnar para uma revanche\033[m")
                self.pontuaçao += 1
                self.AtributosMais()
                return self.NovoJogo()
        elif QueInimigo == 3:
            self.bruxo -= DanoNele
            print(f"\033[1;33mVoce causou ao Mago-Anciao-Necromante {DanoNele} dano\033[m")
            if self.bruxo <= 0:
                print("\033[1;33mVoce destruiu o o corpo de boneco do Mago-Necromante,\n"
                      " que permanece vivo, pois sua alma continua intacta, e a qualquer momento ele pode retornar\n"
                      "para criar um exercito ara seu mestre demoniaco, usando a alma daqueles que ainda estao vivos\033[m ")
                self.pontuaçao += 1
                self.AtributosMais()
                return self.NovoJogo()
        elif QueInimigo == 4:
            self.ogro -= DanoNele
            print(f"\033[1;33mVoce causou ao Demonio-Recem-transformado {DanoNele} dano\033[m")
            if self.ogro <= 0:
                print("\033[1;33mVoce conseguiu destruir o Demonio recem-transformado, assim evitando que ele ficasse mais forte\n"
                      "e pudesse capturar almas para o Mago Necromante criar mais Demonios\033[m")
                self.pontuaçao += 1
                self.AtributosMais()
                return self.NovoJogo()

    def salvaGame(self, rivais):

        self.file["nome"] = self.nome
        self.file["vida"] = str(self.player)
        self.file["poder"] = str(self.SPplayer)
        self.file["defesa"] = str(self.seif)
        self.file["força"] = str(self.fortaleza)
        self.file["num_inimigos"] = str(rivais)
        self.file["pontuaçao"] = str(self.pontuaçao)





    def carregarGame(self):

        nome = self.file["nome"].decode()
        vida = self.file["vida"].decode()
        poder = self.file["poder"].decode()
        defesa = self.file["defesa"].decode()
        força = self.file["força"].decode()
        num_inimigos = self.file["num_inimigos"].decode()
        pontuaçaoS = self.file["pontuaçao"].decode()

        self.nome = nome
        self.player = int(vida)
        self.SPplayer = int(poder)
        self.seif = int(defesa)
        self.fortaleza = int(força)
        num_inimigosQ = int(num_inimigos)
        self.pontuaçao = pontuaçaoS


        return self.NovoJogo()


    def AtributosMais(self):

        while True:
            try:
                Escolha = input(f"Bom {self.nome}, como voce derroutou um inimigo, voce pode aumentar seus atributos de força e defesa, de forma aleatoria de 1 ate 15 de cada,\n"
                                f"mas voce tambem pode resturarsua vida e seu poder, escolha com sabedaria: (A)Atributos ou (R) Restauraçao").upper().strip()
                if Escolha.startswith("A"):
                    defesarand = random.randint(1,15)
                    forçarand = random.randint(1,15)
                    self.fortaleza += defesarand
                    self.seif += forçarand
                elif Escolha.startswith("R"):
                    self.SPplayer = 100
                    self.player = 500
                else:
                    print("Escolha invalida")
            except IndexError:
                print("Escolha Invalida")







if __name__ == '__main__':
        x = Game()
