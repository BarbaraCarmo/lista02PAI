# Questão 01

## Análise Técnica da Segmentação de Imagem

Este experimento demonstrou a aplicação de duas técnicas distintas para a segmentação de imagem em tons de cinza: Limiarização de Otsu e Detecção de Bordas Laplaciano. O objetivo foi comparar a eficácia de cada método na realce de diferentes características da imagem.

### Raciocínio Adotado

A escolha dessas duas técnicas baseia-se em seus princípios operacionais complementares:

*   **Limiarização de Otsu:** Ideal para separar objetos do fundo em imagens com histogramas bimodais. O algoritmo busca automaticamente um limiar global que minimize a variância intra-classe entre os dois grupos (fundo e objeto).
*   **Detecção de Bordas Laplaciano:** Um operador de segunda ordem que identifica regiões de rápida variação na intensidade de pixels, correspondendo a bordas. É particularmente sensível a detalhes finos, mas também ao ruído, justificando a aplicação de um desfoque prévio.

### Etapas do Experimento

O experimento seguiu as seguintes etapas:

1.  **Carregamento da Imagem:** A imagem de entrada foi carregada em dois formatos: colorido (para referência visual) e em tons de cinza (para processamento).
2.  **Limiarização de Otsu:** A imagem em tons de cinza foi submetida à Limiarização de Otsu utilizando a função `cv2.threshold`. O algoritmo calculou automaticamente o limiar ideal.
3.  **Pré-processamento para Laplaciano:** Um filtro Gaussiano (`cv2.GaussianBlur`) foi aplicado à imagem em tons de cinza para reduzir o ruído antes da detecção de bordas.
4.  **Detecção de Bordas Laplaciano:** O operador Laplaciano (`cv2.Laplacian`) foi aplicado à imagem desfocada. A saída foi convertida para um formato visualizável (`uint8`).
5.  **Visualização dos Resultados:** As imagens original colorida, em tons de cinza, a imagem limiarizada por Otsu e a imagem com as bordas detectadas pelo Laplaciano foram exibidas lado a lado para comparação visual.

### Resultados

Os resultados obtidos foram os seguintes:

*   **Limiar de Otsu Calculado:** O algoritmo de Otsu calculou um limiar de `%.2f`.
*   **Imagem Limiarizada por Otsu:** A imagem resultante apresentou uma segmentação binária clara, separando as regiões de maior intensidade (objeto) das de menor intensidade (fundo) com base no limiar calculado.
*   **Imagem com Bordas Laplaciano:** A imagem resultante realçou as bordas e contornos presentes na imagem original, com maior ou menor intensidade dependendo da variação de intensidade dos pixels na borda.


### Tabela Comparativa

| Técnica                     | Princípio de Segmentação                                | Tipo de Saída    | Sensibilidade ao Ruído | Vantagens                                                                 | Desvantagens                                                                  | Aplicações Típicas                                  |
| :-------------------------- | :------------------------------------------------------ | :--------------- | :--------------------- | :------------------------------------------------------------------------ | :---------------------------------------------------------------------------- | :-------------------------------------------------- |
| Limiarização de Otsu        | Análise do histograma, minimização da variância intra-classe | Imagem Binária   | Baixa                  | Automático, eficaz para fundos uniformes, simples de implementar.           | Fornece apenas segmentação binária, ineficaz para histogramas não bimodais.   | Segmentação de objetos em fundos uniformes        |
| Detecção de Bordas Laplaciano | Segunda derivada espacial, variação de intensidade        | Imagem em Tons de Cinza | Alta                   | Realça contornos e detalhes finos, detecta bordas em diferentes orientações. | Sensível ao ruído (requer pré-processamento), não realiza segmentação semântica. | Detecção de contornos, realce de detalhes finos |

### Evidências
<img width="1000" height="193" alt="image" src="https://github.com/user-attachments/assets/8957427a-f737-477c-aceb-7511c606da70" />
<img width="1000" height="286" alt="image" src="https://github.com/user-attachments/assets/0645025a-f97f-4b31-ae79-507b723b6782" />
<img width="1000" height="261" alt="image" src="https://github.com/user-attachments/assets/f8997103-62aa-403c-9c32-a2f6ffd7c678" />
<img width="1000" height="349" alt="image" src="https://github.com/user-attachments/assets/c3b7f129-4284-4260-8548-ad1f0ff47555" />
<img width="1000" height="241" alt="image" src="https://github.com/user-attachments/assets/118eedff-72e0-4318-81e8-2f7dade82cff" />
<img width="1000" height="411" alt="image" src="https://github.com/user-attachments/assets/4ef7a4d1-94c4-4fd1-a3c4-4492bea613ed" />

### Análise Crítica dos Resultados

A Limiarização de Otsu demonstrou ser eficaz na separação global do objeto principal do fundo, como esperado para imagens com características bimodais. O limiar calculado automaticamente é um ponto forte, eliminando a necessidade de ajuste manual. No entanto, essa técnica fornece apenas uma segmentação binária e não realça detalhes internos ou bordas finas dentro das regiões segmentadas.

Por outro lado, a Detecção de Bordas Laplaciano foi bem-sucedida em identificar as bordas e contornos na imagem. A aplicação prévia do filtro Gaussiano foi crucial para mitigar a sensibilidade do operador Laplaciano ao ruído, resultando em bordas mais nítidas. Contudo, o Laplaciano é um detector de bordas e não um método de segmentação no sentido de separar regiões semanticamente diferentes. A saída é uma imagem que realça as transições de intensidade, o que pode ser útil para outras etapas de processamento de imagem, como extração de características ou reconhecimento de padrões.

A combinação dessas técnicas pode ser poderosa em aplicações onde é necessário primeiro isolar um objeto principal (Otsu) e depois analisar suas características internas ou contornos (Laplaciano). A escolha da técnica mais adequada depende intrinsecamente do objetivo da segmentação e das características da imagem de entrada. Para imagens com ruído significativo, a Limiarização de Otsu pode ser mais robusta para a separação global, enquanto o Laplaciano (com pré-processamento adequado) é superior para a detecção de bordas finas.
