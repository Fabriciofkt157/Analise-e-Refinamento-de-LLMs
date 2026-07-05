# Analise-e-Refinamento-de-LLMs

## NOTA: Este repositório contém as análises fundamentadas para o Artigo <nome artigo indefinido> submetido na Latinoware. Todas as informações contidas aqui são baseadas no projeto de IC Análise do Processamento Linguístico em Português Brasileiro com LLMs (ainda em andamento). 

-- relatório escrito em: 05/07/2026

modelo = DeepSeek LLM 7B, a menos que explicitado outro.
VM = AWS Cloud 1x L40S
Rasp = Raspberry Pi 5 (8GB)


Baterias de testes:
Um conjunto de 200 perguntas de conhecimentos gerais e conversação foi escrito e submetido ao modelo com seus pesos originais (safetensors) usando VM. As respostas originais podem ser conferidas em '/Baterias de testes/Conhecimentos\_gerais-v1.txt'
Como resultado, o modelo demonstrou grande imprecisão em suas respostas. Em sua grande maioria estavam factualmente incorretas, contendo diversos erros gramaticais e interlinguagem (uso de palavras de outras línguas quando uma correspondente existe no idioma solicitado).

Um conjunto de 300 prompts tratando sobre regionalismos brasileiros (gírias de diferentes regiões do Brasil) foi escrito e submetido ao modelo quantizado em Q6\_K\_M usando Rasp. Como resultado, o modelo demonstrou completa insuficiência no quesito veracidade da informação: o modelo alucinou respostas para os 300 prompts. As respostas podem ser encontradas em '/Bateria de testes/Resultado\_regionalismos.txt'.


Preparação da base de dados para Fine-tunning: 
Um conjunto de pares user -> assistant foram formulados a partir dos resultados das baterias de testes realizadas anteriormente. Como as respostas geradas pelo modelo estão incorretas, diversas modificações e adequações são necessárias. Essas alterações foram feitas mantendo a estrutura da resposta do modelo, mas complementando e corrigindo as informações geradas por ele. Esse conjunto é composto por 800 pares, dos quais:
- 400 sobre conhecimentos gerais. A finalidade dessa base é evitar esquecimento catastrófico de funções básicas. Ao inserir prompts gerais num conjunto específico (regionalismos), o modelo é forçado a adaptar seus pesos em função das novas informações, mas também mantendo os pesos gerais corretos. Isso acontece pois para ambos os casos (regionalismos ou conhecimento geral), a função de loss é modificada para chegar a resposta correta. Como é necessário que o modelo aprenda mais conceitos, consequentemente o número de pares será maior do que o número de prompts da medição. Isso ocorre porque para o aprendizado de uma única informação, o modelo precisa de 6 a 9 amostras diferentes tratando do mesmo assunto. Dessa forma, algumas respostas do modelo foram corrigidas levemente e as factualmente incorretas foram reescritas e adicionadas de 4 pares para aprendizado.
- 300 sobre regionalismos. Essa base foi reescrita totalmente do zero, pois o modelo não possui o conhecimento mínimo para escrever uma resposta minimamente viável para essas soluções. Ainda sim, as respostas foram escritas de modo a preservar a estrutura gramatical que o modelo adota ao responder. 
- 100 para adaptações no estilo de escrita das respostas. Como as respostas do modelo tendem a ser "prestativas" demais e não soam naturais para humanos conversando com humanos, o estilo de resposta precisa ser adaptado. Exemplificando: 
    user: E aí, Pierre!
    assistant: Olá, como posso te ajudar?
      |-> Deve ser adaptado para soar mais natural, como "E aí? Tudo certo?"

Último par refinado em resultado_limpo-1.txt: 50