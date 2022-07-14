# ProjetoFinalALA

# Chroma key
é uma técnica de efeito visual que consiste em colocar uma imagem sobre uma outra por meio do anulamento de uma cor padrão, como por exemplo o verde; é uma técnica de processamento de imagens cujo objetivo é eliminar o fundo de uma imagem para isolar os personagens ou objetos de interesse que posteriormente são combinados com uma outra imagem de fundo e é utilizado em vídeos em que se deseja substituir o fundo por algum outro vídeo ou foto.

# Imagem Digital 
composta por uma matriz, onde cada elemento da matriz em uma imagem é denominado pixel, que por sua vez, descreve, de alguma forma apropriada, uma cor para aquele ponto da imagem. Por serem pequenos e próximos uns dos outros, dificilmente são percebidos a olho nu. Assim, quanto maior o número de pixels, ou seja, quanto maior a matriz que forma a imagem, melhor é a sua resolução espacial, o que permite uma melhor diferenciação espacial entre as estruturas, ou seja mais nítidas são as imagens produzidas. O formato do pixel mais comum usado em imagens é o RGB (Red (vermelho), Green (verde) e Blue (azul)). A combinação destas cores deve possibilitar a geração quaisquer outras cores. 
 
# Vídeos
O vídeo digital é composto por uma série de imagens exibidas em rápida sucessão constante com frequências comuns de 15, 24, 30 e 60 quadros(frames) por segundo (FPS); quanto mais quadros tiver, mais detalhes do movimento serão capturados ou exibidos. Cada imagem ou quadro inclui uma varredura de pixels com largura e altura expressas em número de pixels, conhecido como resolução. Quanto maior a resolução do vídeo capturado, maior sua clareza e qualidade. 
Além disso, um vídeo pode ser uma animação, criada por imagens em sequência tendo uma ideia de movimento das cenas, uma gravação feita por imagens.

# Código Chroma key para Imagens
Em primeiro momento, carregamos a imagem ou vídeo, que possui o fundo ou o elemento verde a ser removido ou transformado, para dentro do programa. 

![telefone](https://user-images.githubusercontent.com/109240286/179090854-e0df2eee-4849-4e00-9c61-4e76d46ccc83.jpg)

Assim, seguimos para a etapa de identificação dos pixels verdes, através do espaço de cor HSV, cuja primeira coordenada representa a cor, a segunda a intensidade e a terceira o brilho na função máscara verde, estabelece-se uma faixa de tons verdes segura no sentido de não estar próxima das demais cores, diminuindo a chance do programa transformar espaços da imagem não desejados.  Dessa forma, convertemos inicialmente a imagem para o formato HSV e separamos os canais de cores que desejamos manipular, ou seja o tom da cor, a saturação e o brilho. Com isso, criamos uma matriz máscara de mesmo dimensão da matriz que representa a imagem trabalhada composta unicamente por 1. Então, verificamos cada posição dentro da matriz da imagem, se o valor estiver dentro da faixa de cor estabelecida, substituímos o 1 por 0 na posição. Desse modo, teremos ao final uma máscara binária, onde os zeros representam o espaço da imagem que não será transformado, não fará parte do chroma key. 

Destarte, realizamos o produto entre a máscara binária produzida e a própria imagem, sendo assim nas posições da matriz da máscara, onde temos o valor 1, ao multiplicarmos pela imagem, passarão a ter o mesmo valor da matriz que representa a imagem naquela posição e onde temos o valor 0, haverá a perda de informação da imagem, ou seja permanecerá 0. 

![telefonemascara](https://user-images.githubusercontent.com/109240286/179090507-5edf3458-26b8-4502-bdc7-c98e24e0be25.png)

Por conseguinte, carregamos a imagem, denominada plano de fundo, que irá substituir os espaços verdes da imagem trabalhada e convertemos suas dimensões, a fim de estipular um padrão de tamanho de imagens trabalhadas, como exige a linguagem Julia. Em seguida, criamos uma matriz, chamada máscara invertida, inicialmente inicializada apenas por 1 e com as mesmas dimensões da máscara binária previamente produzida, e subtraímos pela própria máscara binária, gerando uma matriz inversa a máscara binária no sentido de onde uma contém 1 a outra contém 0 e vice-versa. Por fim, realizamos o produto entre a máscara inversa produzida e o plano de fundo, sendo assim nas posições da matriz da máscara inversa, onde temos o valor 1, ao multiplicarmos pelo plano de fundo, passarão a ter o mesmo valor da matriz que representa o plano de fundo naquela posição e onde temos o valor 0, haverá a perda de informação do plano de fundo, ou seja permanecerá 0. 

Finalmente, somamos os produtos entre a máscara binária produzida e a própria imagem e entre a máscara inversa e o plano de fundo, fazendo com que onde na matriz que representa a imagem trabalhada sem os espaços verdes estava armazenado o valor 0, obtenha o valor do pixel do plano de fundo na posição análoga, e vice-versa. Portanto, juntando as duas imagens, de forma que o plano de fundo substitua os espaços da imagem que originalmente eram verdes.
