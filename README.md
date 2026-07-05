# Analise-e-Refinamento-de-LLMs

## NOTA: Este repositório contém as análises fundamentadas para o Artigo <nome artigo indefinido> submetido na Latinoware. Todas as informações contidas aqui são baseadas no projeto de IC Análise do Processamento Linguístico em Português Brasileiro com LLMs (ainda em andamento). 

-- relatório escrito em: 05/07/2026

modelo = DeepSeek LLM 7B, a menos que explicitado outro.
VM = AWS Cloud 1x L40S
Rasp = Raspberry Pi 5 (8GB)

Um conjunto de 200 perguntas de conhecimentos gerais e conversação foi escrito e submetido ao modelo com seus pesos originais (safetensors). As respostas originais podem ser conferidas em '/Baterias de testes/Conhecimentos\_gerais-v1.txt'
Como resultado, o modelo demonstrou grande imprecisão em suas respostas. Em sua grande maioria estavam factualmente incorretas, contendo diversos erros gramaticais e interlinguagem (uso de palavras de outras línguas quando uma correspondente existe no idioma solicitado).

Um conjunto de 300 prompts tratando sobre regionalismos brasileiros (gírias de diferentes regiões do Brasil) foi escrito e submetido ao modelo quantizado em Q6\_K\_M usando Rasp. Como resultado, o modelo demonstrou completa insuficiência no quesito veracidade da informação: o modelo alucinou respostas para os 300 prompts. As respostas podem ser encontradas em '/Bateria de testes/Resultado\_regionalismos.txt'.

