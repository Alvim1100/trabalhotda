# Roteiro de Apresentação - Análise de Criminalidade em Porto Alegre e Região Metropolitana

## ESTRUTURA GERAL
**Duração total: 15 minutos máximo**
**Formato: Gravação de tela + áudio narrado**
**Foco Principal: Docker - infraestrutura e reproduzibilidade**
**Foco Secundário: Análise de dados (superficial)**

---

## 🎬 SEÇÃO 1: INTRODUÇÃO (0:45-1:00 min)

### Fala:
> "Olá! Vou apresentar um projeto prático de análise de dados sobre criminalidade em Porto Alegre. Mas o mais importante aqui **não é o tema dos dados — é a arquitetura e infraestrutura**.
>
> Este projeto exemplifica como usar **Docker para criar um ambiente reproduzível e profissional** para análise de dados. Em 15 minutos, você vai ver:
> - Uma arquitetura completa com múltiplos containers
> - Como garantir que o código roda igual em qualquer máquina
> - E rapidamente como usamos dados reais para gerar insights
>
> Vamos começar!"

### O que mostrar na tela:
- Título do notebook: "Análise de criminalidade em Porto Alegre e Região Metropolitana"
- Mostrar a área de trabalho com os arquivos do projeto (analisecrimes.ipynb, dados_crimes.csv, docker-compose.yml, Dockerfile)

### Dica técnica:
- Fale de forma clara e pausada
- Deixe o título visível por 5 segundos antes de passar
- Zoom na tela se necessário (120% para ler melhor)

---

## 📊 SEÇÃO 2: O DESAFIO (0:30 min)

### Fala:
> "O problema típico em projetos de dados:
> - Seu notebook roda perfeito no seu laptop
> - Manda para o colega — não funciona
> - Instala as bibliotecas, rodam versões diferentes
> - No servidor de produção? Mais caos ainda
>
> **Docker resolve isso completamente.** Você empacotar tudo — code, dependências, versões — em um container. Roda no seu Mac, Windows, Linux, servidor em nuvem... sempre igual.
>
> Vamos ver como!"

---

## � SEÇÃO 3: ARQUITETURA COM DOCKER (3:00-3:30 min) — **SEÇÃO PRINCIPAL**

### Fala:
> "Nossa arquitetura tem 3 componentes principais, todos dockerizados:
>
> **1. Jupyter Notebook** (container de análise)
> - Baseado na imagem oficial jupyter/datascience-notebook
> - Rodando Python com pandas, scikit-learn, matplotlib já instalados
> - Acessível em localhost:8888 com senha configurada
> - Monta um volume com o código atual — mudanças no arquivo local refletem no container
>
> **2. PostgreSQL** (container de dados)
> - Banco de dados relacional para persistência
> - Configurado com usuário, senha e database automáticamente
> - Acessível em localhost:5433
> - Volume persistente — dados não são perdidos se o container cair
>
> **3. Docker Compose** (orquestração)
> - Um arquivo YAML que define toda a infraestrutura
> - Um comando: `docker-compose up` — tudo sobe junto
> - Garante que Jupyter espera PostgreSQL estar pronto
>
> O Dockerfile customizado estende jupyter/datascience-notebook e instala nossas dependências específicas do requirements.txt. Tudo versionado, tudo reproduzível."

### O que mostrar na tela:
1. **docker-compose.yml** (mostrar estrutura completa)
   - Apontar para `services:`
   - Explicar `jupyter:` com ports, volumes, environment
   - Explicar `postgres:` com POSTGRES_USER, POSTGRES_DB, volumes
   - Mostrar `volumes:` no final (dados persistem)
   - **Deixe visível por 15 segundos — é a parte principal**

2. **Dockerfile** (rápido)
   - Mostrar a linha `FROM jupyter/datascience-notebook:latest`
   - Mostrar `COPY requirements.txt` e `RUN pip install`
   - **10 segundos**

3. **requirements.txt** (rápido)
   - Mostrar os pacotes listados
   - Explicar: "Aqui definimos exatamente quais versões instalar"
   - **5 segundos**

4. **Executar o projeto** (o clímax)
   - Abrir terminal
   - Digitar: `docker-compose up`
   - Mostrar o output com containers iniciando
   - Mostrar mensagens: "PostgreSQL is ready to accept connections"
   - Mostrar: "Jupyter notebook server started"
   - **Deixe rodando por 10-15 segundos enquanto fala**

### Dica técnica:
- **Este é o momento crucial** da apresentação
- Fale lentamente: "Vejam o docker-compose.yml — tudo que precisamos está aqui"
- Quando executar `docker-compose up`, deixe as mensagens aparecerem — é satisfatório ver tudo iniciando
- Se possível, abra o navegador e mostre http://localhost:8888 carregando
- Destaque: "Com um comando, dois containers estão rodando, dois serviços diferentes, tudo configurado, tudo funcionando"

---

## 📥 SEÇÃO 4: EXECUTANDO O PROJETO (2:00-2:30 min)

### Fala:
> "Com Docker rodando, abro o Jupyter. Aqui está o notebook com toda a análise.
>
> O fluxo é simples:
> 1. **Coleta**: Ler CSV de crimes e consultar IBGE via API
> 2. **Processamento**: Limpar dados, normalizar texto, remover duplicatas
> 3. **Armazenamento**: Salvar em PostgreSQL (que está rodando no container)
> 4. **Análise**: Gerar gráficos e fazer clustering
>
> Vamos ver alguns resultados rápidos."

### O que mostrar na tela:
1. Abrir o Jupyter em localhost:8888
2. Mostrar o notebook carregado
3. Executar a célula de imports (2-3 segundos)
4. Executar a célula de leitura de CSV (mostrar as primeiras linhas)
5. **Não gaste tempo em coleta de APIs — pule** (diga: "aqui consultamos IBGE, demora alguns segundos, já foi executado")

### Dica técnica:
- Execute rápido (não precisa demonstrar APIs lentas)
- Foco é mostrar que tudo roda sem problemas
- Mostrar que PostgreSQL está recebendo dados
- Transição rápida para resultados

---

## 🧹 SEÇÃO 5: LIMPEZA E ANÁLISE (1:30 min) — SUPERFICIAL

### Fala:
> "A data é sempre bagunçada. Aqui limpamos: normalizar texto, remover acentos, preenchemos valores faltantes, removemos duplicatas.
>
> Rápido de fazer, e depois armazenamos no PostgreSQL:"

### O que mostrar na tela:
1. Executar a célula de limpeza (não leia o código em detalhes)
2. Mostrar o resultado final: "Total de ocorrências: 53.948 linhas"
3. Mostrar a tabela de ocorrências por município (5 segundos)

### Dica técnica:
- Não entre em detalhes de código de limpeza
- Apenas mostre o antes/depois
- Rápido, vai para próxima

---

## 💾 SEÇÃO 6: PERSISTÊNCIA EM BANCO (0:45 min)

### Fala:
> "Aqui é onde Docker brilha. Os dados vão para PostgreSQL — o container que está rodando separado.
>
> Usando SQLAlchemy (biblioteca Python), fazemos:
> ```
> engine = create_engine("postgresql+psycopg2://admin:admin@postgres:5432/crimes_db")
> df_crimes.to_sql("crimes", engine, if_exists="replace", index=False)
> ```
>
> Uma linha de código. O Jupyter (container A) fala com PostgreSQL (container B) transparentemente. Se desligar o notebook e ligar de novo — os dados ainda estão lá.
>
> Isso é a vantagem do Docker: **separação de responsabilidades**. Análise em um container, dados em outro."

### O que mostrar na tela:
1. Mostrar a célula com `create_engine()` (apontar para a string de conexão)
2. Apontar: "postgres://admin:admin@postgres:5432" — o `postgres` é o nome do container no docker-compose
3. Executar `to_sql()` — mostrar sucesso
4. Opcionalmente, abrir um terminal e fazer: `docker exec -it crimes_postgres_db psql -U admin -d crimes_db -c "SELECT COUNT(*) FROM crimes;"`
   - Mostrar que retorna 53948 linhas
   - Isso prova que os dados estão realmente no PostgreSQL

### Dica técnica:
- **Isto é um insight importante**: mostrar que Jupyter e PostgreSQL se comunicam
- Se possível, a query no terminal é o clímax técnico
- Se não conseguir, apenas executar to_sql() é suficiente

---

## 📈 SEÇÃO 7: ANÁLISE RÁPIDA (1:30 min) — NÃO ENTRAR EM DETALHES

### Fala:
> "Rapidamente, alguns insights dos dados:
>
> - Porto Alegre tem 31k crimes (maior volume)
> - Quando corrigimos por população, o ranking muda — algumas cidades menores têm taxa mais alta
> - 3 padrões criminais diferentes (clusters) foram identificados via machine learning
> - Mulheres sofrem mais com ameaça; idosos com fraudes
>
> Mas o foco aqui não é interpretar criminalidade — é mostrar que **Docker permitiu essa análise rodar completamente isolada e reproduzível**."

### O que mostrar na tela:
1. Executar 1-2 gráficos principais (máximo 30 segundos total)
   - Mostrar gráfico de crimes por município
   - Mostrar gráfico de clustering (3 cores representando 3 perfis)
2. Não entre em detalhes de interpretação
3. Transição rápida

### Dica técnica:
- Não gaste tempo nessa seção
- Objetivo é apenas mostrar que os dados geraram insights
- Foco permanece em Docker

---

## (DELETADO) SEÇÃO 8 REMOVIDA
Cortada para manter duração em 15 min e foco em Docker

---

## 🎯 SEÇÃO 8: MACHINE LEARNING (1:00 min) — RÁPIDO

### Fala:
> "Rapidamente: usamos K-Means para agrupar 409 bairros em 3 padrões criminais. O código é simples:
>
> ```python
> from sklearn.preprocessing import StandardScaler
> from sklearn.cluster import KMeans
>
> scaler = StandardScaler()
> X = scaler.fit_transform(perfil)
> km = KMeans(n_clusters=3, random_state=42, n_init=10)
> clusters = km.fit_predict(X)
> ```
>
> Encontramos 3 tipos: Violência Interpessoal (47%), Violência e Trânsito (30%), Crimes Financeiros (22%).
>
> Novamente: **isso roda no Jupyter, dentro do Docker, com dados do PostgreSQL**. Tudo conectado, tudo isolado, tudo reproduzível."

### O que mostrar na tela:
1. Mostrar o código de K-Means (breve)
2. Executar a célula
3. Mostrar 1 gráfico de clustering (30 segundos máximo)
4. Transição rápida

### Dica técnica:
- Não entre em detalhes de clustering
- Apenas mostre que roda e gera resultados
- O objetivo é ilustrar que é possível fazer ML dentro de Docker

---

## 💡 SEÇÃO 9: CONCLUSÃO — FOCO EM DOCKER (1:00 min)

### Fala:
> "Em resumo: este projeto exemplifica um pipeline **completo e profissional** de análise de dados usando Docker.
>
> **O que conseguimos:**
> ✓ Ambiente reproduzível (funciona em qualquer máquina)
> ✓ Múltiplos serviços orquestrados (Jupyter + PostgreSQL)
> ✓ Dados persistidos (não perdem se container cair)
> ✓ Dependências versionadas (requirements.txt)
> ✓ Um comando para tudo subir: `docker-compose up`
>
> **Benefícios práticos:**
> - Você pode mandar o projeto para o colega — ele roda igual
> - Pode deployar em servidor de produção — roda igual
> - Novo membro entra na equipe? Ele faz `docker-compose up` e está pronto
> - Precisa escalar? Adiciona mais containers, não precisa mexer no código
>
> E dentro dessa infraestrutura, você pode fazer análise de dados, machine learning, API services — o que quiser.
>
> Este é o padrão moderno de desenvolvimento de software."

---

## 🎥 SEÇÃO 10: FECHAMENTO (0:30 min)

### Fala:
> "Docker permite que você:
>
> 1. **Desenvolva localmente** com a mesma stack de produção
> 2. **Collaborate** sem "mas funciona no meu PC"
> 3. **Escale facilmente** — adicione containers conforme precisa
> 4. **Mantenha isolado** — código, dados, dependências em ambientes separados
>
> Isso foi um exemplo prático. Você pode usar exatamente esse padrão (Jupyter + PostgreSQL) para seus próprios projetos de análise de dados.
>
> Código disponível em [seu repositório]. Obrigado!"

---

## 📋 CHECKLIST PRÉ-GRAVAÇÃO

- [ ] Docker running: `docker-compose up` já executado
- [ ] Jupyter acessível em localhost:8888
- [ ] PostgreSQL conectado e com dados
- [ ] Notebook completamente executado (até a seção de conclusões)
- [ ] Zoom da tela em 120% para melhor legibilidade
- [ ] Microfone testado
- [ ] Nenhuma notificação (desativar Slack, email, Teams, etc.)
- [ ] Terminal pronto para mostrar `docker-compose up`
- [ ] Duração máxima: 15 minutos
- [ ] Cronômetro visível (opcional, para ficar dentro do tempo)

---

## 🎤 DICAS DE GRAVAÇÃO — FOCO EM DOCKER

1. **Seção 3 (Docker) é a mais importante** — deixe 30-45 segundos mostrando docker-compose.yml
2. **Deixe `docker-compose up` executando visível** — é satisfatório ver os containers iniciando
3. **Fale lentamente na seção de Docker** — a audiência quer aprender a tecnologia
4. **Na análise de dados, seja rápido** — não distraia com interpretações detalhadas
5. **Aponte para linhas específicas no código Docker** — "Vejam aqui... @postgres — isso conecta ao container postgres"
6. **Se possível, mostre uma query no PostgreSQL** — `SELECT COUNT(*) FROM crimes` prova que os dados estão realmente lá
7. **Use tom de "teach and show"** para Docker, tom de "aqui estão os resultados" para análise
8. **Não tente colocar análise muito detalhada** — você tem 15 min, Docker é a prioridade

---

## ⏱️ TIMING FINAL

| Seção | Duração |
|-------|----------|
| 1. Introdução | 0:45-1:00 |
| 2. O Desafio | 0:30 |
| **3. Docker (PRINCIPAL)** | **3:00-3:30** |
| 4. Executando Projeto | 2:00-2:30 |
| 5. Limpeza & Análise | 1:30 |
| 6. PostgreSQL | 0:45 |
| 7. Análise Rápida | 1:30 |
| 8. Machine Learning | 1:00 |
| 9. Conclusão Docker | 1:00 |
| 10. Fechamento | 0:30 |
| **TOTAL** | **~15:00** |

---

## 💬 FRASES-CHAVE (para memorizar)

- "Com um comando, tudo sobe: `docker-compose up`"
- "Jupyter no container A, PostgreSQL no container B, tudo comunicando"
- "Dados persistem — se desligar e ligar de novo, ainda estão lá"
- "Funciona no meu PC? Funciona em produção. Mesma coisa."
- "Isso é o padrão moderno de desenvolvimento de software"

---

**Pronto para gravar! Boa sorte! 🎬**
