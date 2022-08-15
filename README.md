#importando os mudulos
from random import randint
import decimal
import pygame
import math

#função para escrever texto na tela
def draw_text(text, color, surface, x, y,count):
    font = pygame.font.SysFont('arial black', 30)
    text = font.render(text+str(count), True, color, (255,255,255))
    pos_text = text.get_rect()
    pos_text.center = (x, y)
    surface.blit(text,pos_text)


#função principal main
def main():
    pygame.init()

    #criando variaveis
    screen = pygame.display.set_mode((800,600))
    x, y = 400, 300
    
    velocityX1 = 5
    velocityY1 = 5
    velocityX2 = 5
    velocityY2 = 5


    bha = 3
    radiusP = 30
    radiusC = 20
    

    Count = 0

    WHITE = (255,255,255)
    RED = (255, 0, 0)







    #criando uma posição aleatria para a comida
    posX, posY = randint(20,780), randint(20,580)

    #sistema de repetição para o jogo
    while True:
        #sistema para verificar a função de fechamento do jogo
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
        #pintando a tela de branco
        screen.fill(WHITE)
        #criando uma variavel para as detecção das teclas
        key = pygame.key.get_pressed()


        
        
        #calculando a distancia dos elementos

        distanceX = x - posX
        distanceY = y - posY

        distence = pow(distanceX**2 + distanceY**2, 1/2)  

        inputs = [[],
                  []]

        inputs[0].append(distanceX)
        inputs[1].append(distanceY)
        
        peso11 = randint(-100,100)
        peso21 = randint(-100,100)
        peso31 = randint(-100,100)
        peso41 = randint(-100,100)

        peso12 = randint(-100,100)
        peso22 = randint(-100,100)
        peso32 = randint(-100,100)
        peso42 = randint(-100,100)



    
        neurony = [[peso11,peso12],
                   [peso21,peso22],
                   [peso31,peso32],
                   [peso41,peso42]]
        
    

        ResultNeurony = [[inputs[0][0]*neurony[0][0] + inputs[1][0]*neurony[0][1]],
                         [inputs[0][0]*neurony[1][0] + inputs[1][0]*neurony[1][1]],
                         [inputs[0][0]*neurony[2][0] + inputs[1][0]*neurony[2][1]],
                         [inputs[0][0]*neurony[3][0] + inputs[1][0]*neurony[3][1]]]
        

        neurony1 = ResultNeurony[0][0]
        neurony2 = ResultNeurony[1][0]
        neurony3 = ResultNeurony[2][0]
        neurony4 = ResultNeurony[3][0]
        
        

        output1 = 1/(1+pow(math.e, 0.00005*(-neurony1)))
        output2 = 1/(1+pow(math.e, 0.00005*(-neurony2)))
        output3 = 1/(1+pow(math.e, 0.00005*(-neurony3)))
        output4 = 1/(1+pow(math.e, 0.00005*(-neurony4)))

        


        outputM = [[],[],[],[]]
        outputM[0].append(output1)
        outputM[1].append(output2)
        outputM[2].append(output3)
        outputM[3].append(output4)


        peso11_2 = randint(-100,100)
        peso21_2 = randint(-100,100)
        peso31_2 = randint(-100,100)
        peso41_2 = randint(-100,100)

        peso12_2 = randint(-100,100)
        peso22_2 = randint(-100,100)
        peso32_2 = randint(-100,100)
        peso42_2 = randint(-100,100)
        
        peso13_2 = randint(-100,100)
        peso23_2 = randint(-100,100)
        peso33_2 = randint(-100,100)
        peso43_2 = randint(-100,100)

        peso14_2 = randint(-100,100)
        peso24_2 = randint(-100,100)
        peso34_2 = randint(-100,100)
        peso44_2 = randint(-100,100)

        neurony_2 = [[peso11_2,peso12_2,peso13_2,peso14_2],
                     [peso21_2,peso22_2,peso13_2,peso14_2],
                     [peso31_2,peso32_2,peso13_2,peso14_2],
                     [peso41_2,peso42_2,peso13_2,peso14_2]]




        ResultNeurony2 = [[neurony_2[0][0]*outputM[0][0] + neurony_2[0][1]*outputM[1][0] + neurony_2[2][0]*outputM[2][0] + neurony_2[3][0]*outputM[3][0]],
                          [neurony_2[0][1]*outputM[0][0] + neurony_2[1][1]*outputM[1][0] + neurony_2[2][1]*outputM[2][0] + neurony_2[3][1]*outputM[3][0]],
                          [neurony_2[0][2]*outputM[0][0] + neurony_2[1][2]*outputM[1][0] + neurony_2[2][2]*outputM[2][0] + neurony_2[3][2]*outputM[3][0]],
                          [neurony_2[0][3]*outputM[0][0] + neurony_2[1][3]*outputM[1][0] + neurony_2[2][3]*outputM[2][0] + neurony_2[3][3]*outputM[3][0]]]

        saia1 = ResultNeurony2[0][0]
        saia2 = ResultNeurony2[1][0]
        saia3 = ResultNeurony2[2][0]
        saia4 = ResultNeurony2[3][0]

        saida1 = 1/(1+pow(math.e, (-saia1)))
        saida2 = 1/(1+pow(math.e, (-saia2)))
        saida3 = 1/(1+pow(math.e, (-saia3)))
        saida4 = 1/(1+pow(math.e, (-saia4)))
        

        if saida1 >= 0.5:
            y -= velocityY1
        if saida2 >= 0.5:
            y += velocityY2
        if saida3 >= 0.5:
            x -= velocityX1
        if saida4 >= 0.5:
            x += velocityX2

        #detecção da colição nas paredes
        if x <= 30:
            velocityX1 = 0
        if not x <= 30:
            velocityX1 = 5
        if x >= 770:
            velocityX2 = 0
        if not x >= 770:
            velocityX2 = 5
        if y <= 30:
            velocityY1 = 0
        if not y <= 30:
            velocityY1 = 5
        if y >= 570:
            velocityY2 = 0
        if not y >= 570:
            velocityY2 = 5
            
        

        
        #colisão dos elementos
        if int(distence) <= radiusP + radiusC:
            posX, posY = randint(20,780), randint(20,580)
            Count += 1
        
        if Count >= bha:
            peso11 += randint(-4,4)
            peso21 += randint(-4,4)
            peso31 += randint(-4,4)
            peso41 += randint(-4,4)

            peso12 += randint(-4,4)
            peso22 += randint(-4,4)
            peso32 += randint(-4,4)
            peso42 += randint(-4,4)

        
            peso11_2 += randint(-4,4)
            peso21_2 += randint(-4,4)
            peso31_2 += randint(-4,4)
            peso41_2 += randint(-4,4)

            peso12_2 += randint(-4,4)
            peso22_2 += randint(-4,4)
            peso32_2 += randint(-4,4)
            peso42_2 += randint(-4,4)

            peso13_2 = randint(-4,4)
            peso23_2 = randint(-4,4)
            peso33_2 = randint(-4,4)
            peso43_2 = randint(-4,4)

            peso14_2 = randint(-4,4)
            peso24_2 = randint(-4,4)
            peso34_2 = randint(-4,4)
            peso44_2 = randint(-4,4)
            bha += 2

    


        #colocando o cantandor na tela
        draw_text('Count:', (0,0,0), screen, 65,10,Count)

        #desenhando os elementos na tela
        pygame.draw.circle(screen,RED,(x,y), radiusP)
        pygame.draw.circle(screen,(0,0,0),(posX,posY), radiusC)




        #autualizando a tela
        pygame.display.flip()
    pygame.quit()


if __name__ == '__main__':
    
    main()

