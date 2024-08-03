# IA_Flappy
 **Treinando a IA para jogar Flappybird**
 
 A ideia é usar o sistema NEAT 

 ## O que é NEAT?
NEAT é um algoritmo de inteligência artificial que usa conceitos de evolução e crescimento incremental para treinar redes neurais.
Ele usa os seguintes processos

**Evolução de Redes Neurais:**

    Ao invés de treinar uma rede neural usando métodos tradicionais, o NEAT usa um processo evolutivo, parecido com a seleção natural. Isso significa que ele começa com várias redes neurais simples e as melhora ao longo de várias gerações, selecionando as melhores e combinando-as para criar novas redes.

**Aumento Incremental:** 

    Diferente de outros métodos que começam com redes neurais grandes e complexas, o NEAT começa com redes simples e as torna mais complexas ao longo do tempo, adicionando novos nós e conexões conforme necessário. Isso permite que as redes cresçam e se adaptem de forma mais eficiente ao problema que estão tentando resolver.

**Como Funciona:**
 - Inicialização: Começa com uma população de redes neurais simples.
 - Avaliação: Cada rede é avaliada com base em quão bem resolve o problema (sua "aptidão").
 - Seleção e Reprodução: As redes com melhor desempenho são selecionadas para "cruzamento" e "mutação" para criar a próxima geração de redes.
 - Mutação: Adiciona ou remove conexões e nós, ou altera os pesos das conexões.
 - Repetição: Este processo se repete por várias gerações, com as redes evoluindo e melhorando ao longo do tempo
   

  ## Explicando o config.txt

    Esta seção define os parâmetros gerais do algoritmo NEAT.

### [NEAT]
---
- **fitness_criterion = max:** O critério de aptidão é maximizar a pontuação.
- **fitness_threshold = 1000:** A aptidão alvo para a qual a evolução deve tentar alcançar.
- **pop_size = 100:** Tamanho da população, ou seja, quantos indivíduos (redes neurais) existem em cada geração.
- **reset_on_extinction = False:** Se deve reiniciar a evolução se todas as espécies se extinguirem.
---

###  [DEFAULT_GENOME]
- **activation_default = tanh:** A função de ativação padrão para os nós (tanh). 
Função que define se o neuronio vai ou não ativar.
usando a formula da tangente hiperbolica, que transforma qualquer valor recebido em algum valor entre 1 e -1
a função de ativação recebe os dados de entrada, no caso são. 
 - Posição vertical do passaro
 - Distancia do proximo cano
 - Velocidade vertical do passaro
(estes valores sao coletados nas posições atuais do passaro na tela, me de inico, começam setados com a posição inicial)

 - **activation_mutate_rate = 0.0:** A taxa de mutação para as funções de ativação.
Como estamos usando apenas uma função de ativação, esse valor nunca sera alterado.

 - **activation_options = tanh:** Funções de ativação permitidas.

- **aggregation_default = sum:** A função de agregação padrão (soma).
Uma função de agregação toma todas as entradas ponderadas (entrada multiplicadas pelos pesos) de um 
neurônio e combina esses valores em um único valor que será passado para a função de ativação
varias funções de ativação são posiveis como soma media e produto. A escolhida foi soma

- **aggregation_mutate_rate = 0.0:** Taxa de mutação para funções de agregação.
- **aggregation_options = sum:** Funções de agregação permitidas.

---

### [BIAS]

--- 

Bias é o valor adicionado a soma ponderada, que ajuda o codigo a transformar o valor em algo proximo de 1 e -1
(Nós (Neurônios) sao unidades que recebem alguma entrada e multiplicam pelo peso)

- **bias_init_mean = 0.0:** Média inicial dos bias dos nós. o primeiro bias, é alguma valor aleatorio proximo de 0.0
- **bias_init_stdev = 1.0:** Desvio padrão inicial dos bias dos nós.
- **bias_max_value = 30.0:** Valor máximo do bias.
- **bias_min_value = -30.0:** Valor mínimo do bias.
- **bias_mutate_power = 0.5:** Grau de mudança aplicada aos bias durante a mutação.
- **bias_mutate_rate = 0.7:** Probabilidade de mutação do bias.
- **bias_replace_rate = 0.1:** Taxa de substituição do bias.

---

### [COMPATIBILIDADE]

---

Compatibilidade é uma medida de quão semelhantes são dois indivíduos em uma população evolutiva. Na configuração NEAT , a compatibilidade ajuda a decidir se dois indivíduos (ou redes neurais) devem ser considerados parte da mesma espécie. Isso é crucial para o processo de especiação e evolução da rede neural.

# compatibility_disjoint_coefficient = 1.0 Define o coeficiente para a compatibilidade dos genes disjuntos
Genes disjuntos são aqueles que não têm correspondentes em ambos os indivíduos comparados. Se um gene está presente em um indivíduo, mas não no outro, ele é considerado disjunto. De outra especie

# compatibility_weight_coefficient = 0.5 Define o coeficiente para a compatibilidade das diferenças de peso.
As diferenças de peso entre os genes correspondentes em dois indivíduos também são usadas para calcular a compatibilidade. Este coeficiente determina o quanto essas diferenças de peso influenciam a compatibilidade.

Um coeficiente maior para diferenças de peso aumenta a penalidade para variações nos pesos dos genes, ajudando a garantir que indivíduos com grandes diferenças nos pesos sejam menos propensos a serem considerados da mesma espécie.

---

### [CONEXOES]

---

Em uma rede neural, conexões são as ligações entre os nós (ou neurônios) que permitem a transferência de informações de um nó para outro. Cada conexão tem um peso associado que influencia a força e a direção da informação transmitida.

- **conn_add_prob = 0.5** Probabilidade de adicionar uma nova conexão entre dois nós.
Durante o processo de evolução da rede neural, novas conexões podem ser introduzidas 
para melhorar a capacidade de modelagem da rede. Este parâmetro define a probabilidade 
de que uma nova conexão seja adicionada durante o processo de mutação.
Com uma probabilidade de 0.5, há uma chance de 50% de que uma nova 
conexão será adicionada a cada tentativa de mutação.

- **conn_delete_prob = 0.5** Probabilidade de deletar uma conexão existente
Com uma probabilidade de 0.5, há uma chance de 50% de que uma conexão existente 
será deletada a cada tentativa de mutação. Isso ajuda a reduzir a complexidade da 
rede e a eliminar conexões que não contribuem significativamente para o desempenho.

- **enabled_default = True** Define se as conexões são habilitadas por padrão quando são criadas

- **enabled_mutate_rate = 0.01** Taxa de mutação que ativa ou desativa uma conexão existente.

---

### [ESTRUTURA_DE_REDE]

---

A estrutura de rede em uma rede neural refere-se à organização e ao arranjo dos seus componentes, que incluem os nós (ou neurônios) e as conexões entre eles.

- **feed_forward = True**
Em uma rede feed-forward, as informações fluem apenas em uma direção, da entrada para a saída, sem conexões que retornem ou criem ciclos (conexões recorrentes). Isso significa que não há conexões que levam de volta a camadas anteriores.

- **initial_connection = full** Todas as conexões são inicialmente completas.
Quando a rede é inicializada, todos os nós são conectados uns aos outros. 
Isso significa que, na configuração inicial da rede, cada nó está ligado a todos 
os outros nós. A rede começa com uma topologia completamente conectada. Isso pode facilitar 
o início do treinamento, pois todos os nós estão inicialmente interconectados, mas 
pode ser alterado durante a evolução para otimizar a estrutura da rede.

- **node_add_prob = 0.2** Probabilidade de adicionar um novo nó.
Durante o processo de evolução, novos nós podem ser adicionados à rede. 
Este parâmetro define a probabilidade de que um novo nó será adicionado durante 
cada tentativa de mutação. há uma chance de 20% de adicionar um novo nó a cada 
tentativa de mutação. Adicionar nós pode ajudar a rede a capturar padrões mais 
complexos ao aumentar sua capacidade de modelagem.

- **node_delete_prob = 0.2** Probabilidade de deletar um nó existente.

---

### [PARAMETROS_DE_REDE]

---

Esses parâmetros definem a estrutura inicial da rede neural, determinando 
o número de nós (ou neurônios) em cada camada da rede.

- **num_hidden = 0** Número de nós ocultos iniciais
Neste caso, o valor é 0, o que significa que a rede neural começa sem nós ocultos. 
Inicialmente, a rede terá apenas a camada de entrada e a camada de saída.
Sem nós ocultos, a rede não terá capacidade para modelar complexidades intermediárias 
nos dados. No entanto, durante a evolução, a rede pode adicionar nós ocultos 
conforme necessário, permitindo a exploração de estruturas mais complexas.

- **num_inputs = 3**  Número de nós de entrada
Define quantos valores de entrada a rede irá receber.
No contexto do jogo Flappy Bird, isso pode inclur
- Posição do pássaro: A posição vertical do pássaro na tela.
- Posição do próximo cano: A posição vertical do cano mais próximo.
- Velocidade do pássaro: A velocidade com que o pássaro está se movendo.

Esses valores de entrada fornecem à rede as informações necessárias para 
tomar decisões, como se deve pular ou não.

- **num_outputs = 1** Número de nós de saída.
Define quantas ações a rede pode tomar como saída. Isso define a açao de pular ou nao 1 ou -1

---

### [RESPOSTA_DE_NÓS]

---

Esses parâmetros se referem à configuração da resposta dos nós na rede neural, 
o que afeta como cada nó processa e transmite informações.

- **response_init_mean = 1.0** Média inicial da resposta dos nós.
Define o valor médio inicial para a resposta dos nós quando a rede é criada. 
Neste caso, a média inicial é 1.0, o que significa que a maioria dos nós começará 
com uma resposta de cerca de 1.0. A resposta dos nós pode afetar como eles 
processam as entradas. Com uma média inicial de 1.0, todos os nós começam com 
um valor de resposta que não é nem muito baixo nem muito alto, o 
que pode influenciar como a rede começa a aprender.

- **response_init_stdev = 0.0** Desvio padrão inicial da resposta dos nós.
Define a variação da resposta dos nós a partir da média inicial. 
Um desvio padrão de 0.0 significa que todas as respostas dos nós 
começarão exatamente no valor médio de 1.0, sem variação.
Sem variação, todos os nós começam com a mesma resposta, tornando a 
inicialização da rede mais uniforme e previsível.

- **response_max_value = 30.0** Valor máximo da resposta dos nós.
- **response_min_value = -30.0** Valor mínimo da resposta dos nós.
- **response_mutate_power = 0.0** Grau de mudança aplicado à resposta durante a mutação.
- **response_mutate_rate = 0.0** Probabilidade de mutação da resposta.
- **response_replace_rate = 0.0** Taxa de substituição da resposta.

---

### [PESOS_DAS_CONEXOES]

- **weight_init_mean = 0.0:** Média inicial dos pesos das conexões.
- **weight_init_stdev = 1.0:** Desvio padrão inicial dos pesos das conexões.
- **weight_max_value = 30:** Valor máximo dos pesos.
- **weight_min_value = -30:** Valor mínimo dos pesos.
- **weight_mutate_power = 0.5:** Grau de mudança aplicada aos pesos durante a mutação.
- **weight_mutate_rate = 0.8:** Probabilidade de mutação dos pesos.
- **weight_replace_rate = 0.1:** Taxa de substituição dos pesos

---

### [DEFAULTESPECIESET]

---

Esta seção define como as espécies são gerenciadas.

- **compatibility_threshold = 3.0:** Limite de compatibilidade para determinar se dois genomas pertencem à mesma espécie.

---

### [DefaultStagnation]

---

Esta seção define como lidar com estagnação dentro das espécies.

- **species_fitness_func = max:** Função de aptidão para a espécie (máximo).
- **max_stagnation = 20:** Número máximo de gerações que uma espécie pode estagnar antes de ser extinta.
- **species_elitism = 2:** Número de indivíduos da espécie que são protegidos da extinção.

---

### [DefaultReproduction]

---

Esta seção define como a reprodução é gerenciada.

- **elitism = 2:** Número de indivíduos da geração atual que são passados diretamente para a próxima geração sem modificação.
- **survival_threshold = 0.2:** Percentual de indivíduos de uma espécie que são elegíveis para reprodução.
