# Copa do Mundo 2026 — Sistema de Acompanhamento

Sistema web em Python para acompanhar a Copa do Mundo FIFA 2026 com 48 seleções, 12 grupos, chaveamento completo, probabilidades para apostas e exportação para planilha.

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Flask](https://img.shields.io/badge/Flask-3.0-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

---

## Sumário

- [Funcionalidades](#funcionalidades)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Instalação](#instalação)
- [Como Usar](#como-usar)
- [Executável Portátil](#executável-portátil)
- [API REST](#api-rest)
- [Formato da Copa 2026](#formato-da-copa-2026)
- [Dados das Seleções](#dados-das-seleções)
- [Exportação XLSX](#exportação-xlsx)
- [Probabilidades e Apostas](#probabilidades-e-apostas)
- [Atualização via API da FIFA](#atualização-via-api-da-fifa)

---

## Funcionalidades

| Funcionalidade | Descrição |
|---|---|
| **Dashboard** | Visão geral dos 12 grupos com classificação ordenada por pontos |
| **Fase de Grupos** | Tabela detalhada com P/J/V/E/D/GP/GC/SG + calendário de jogos |
| **Chaveamento** | Bracket completo: 16-avos → Oitavas → Quartas → Semi → Final |
| **Placares ao Vivo** | Classificação ordenada por pontos (SG/GP) + auto-refresh via API da FIFA |
| **Probabilidades** | Cards com fundo claro, odds e barras de progresso para casa/empate/fora |
| **Exportação XLSX** | Planilha com 5 abas (Grupos, Probabilidades, Chaveamento, Seleções, Legenda) |
| **Legenda Interativa** | Tooltips explicativos para todas as siglas do chaveamento |
| **Persistência** | Resultados salvos em arquivo JSON — não perde dados ao reiniciar |

---

## Estrutura do Projeto

```
copa2026/
├── app.py              # Servidor Flask — rotas e API
├── data.py             # 48 seleções, 12 grupos, chaveamento, datas, legendas
├── fifa_api.py         # Integração com API da FIFA (automática)
├── scores.py           # Persistência de placares em JSON
├── utils.py            # Probabilidades e exportação XLSX
├── run.py              # Entry point para PyInstaller
├── requirements.txt    # Dependências
├── matches_data.json   # (gerado automaticamente) Placar salvo
├── templates/
│   ├── layout.html     # Template base — navbar, footer, auto-refresh
│   ├── index.html      # Dashboard com grupos e probabilidades
│   ├── groups.html     # Fase de grupos com tabela e jogos
│   └── bracket.html    # Chaveamento completo com placar editável
└── dist/
    └── Copa2026.exe    # Executável standalone (gerado pelo PyInstaller)
```

---

## Instalação

### Requisitos

- Python 3.10 ou superior
- Pip

### Passos

```bash
# 1. Clone ou copie os arquivos
# 2. Instale as dependências
pip install flask requests openpyxl

# 3. Execute
python app.py
```

Acesse em: **http://localhost:5000**

---

## Como Usar

### Navegação

| Aba | Descrição |
|---|---|
| **Dashboard** | Cards com todos os 12 grupos, classificação resumida e probabilidades da fase de grupos |
| **Grupos** | Tabela completa com estatísticas (P/J/V/E/D/GP/GC/SG) e calendário de jogos |
| **Chaveamento** | Bracket lado a lado do mata-mata com placar editável e odds |

### Editando Placares

1. Vá até a página **Chaveamento**
2. **Clique no placar** (`-`) de qualquer partida
3. Digite o número de gols e pressione **Enter**
4. Clique em **Salvar** — o resultado fica persistido

### Atualizando Resultados

- Clique no botão **Atualizar** no topo da página
- O sistema tenta buscar dados ao vivo da API da FIFA
- Auto-refresh automático a cada 90 segundos

### Exportando Planilha

Clique em **Exportar XLSX** no topo de qualquer página para baixar uma planilha completa com:

1. **Grupos** — Times, classificação e tabela de jogos
2. **Probabilidades** — Odds de cada partida com data
3. **Chaveamento** — Todas as partidas do mata-mata com datas
4. **Todas as Seleções** — Lista das 48 seleções ordenadas por ranking
5. **Legenda** — Explicação de todas as siglas

---

## Executável Portátil

O arquivo `dist/Copa2026.exe` é um executável **standalone** (33 MB) que não precisa de Python instalado.

### Para gerar:

```bash
pip install pyinstaller
pyinstaller --onefile --windowed --name "Copa2026" \
  --add-data "templates;templates" \
  --hidden-import flask --hidden-import openpyxl \
  --hidden-import requests \
  run.py
```

### Para usar:

1. Copie `dist/Copa2026.exe` para qualquer computador Windows
2. Dê dois cliques — o navegador abre automaticamente
3. Os dados de placar são salvos em `matches_data.json` na mesma pasta do `.exe`

> **Nota:** O Windows pode exibir um alerta de segurança na primeira execução por ser um executável não-assinado. Clique em "Executar assim mesmo".

---

## API REST

### Endpoints

| Método | Rota | Descrição |
|---|---|---|
| `GET` | `/` | Dashboard |
| `GET` | `/groups` | Fase de grupos |
| `GET` | `/bracket` | Chaveamento |
| `GET` | `/api/standings` | Classificação dos grupos (JSON) |
| `GET` | `/api/live` | Partidas ao vivo da FIFA (JSON) |
| `GET` | `/api/atualizar` | Força atualização dos dados (JSON) |
| `GET` | `/api/probabilidade?home=X&away=Y` | Probabilidade de uma partida (JSON) |
| `POST` | `/api/placar` | Salva placar de uma partida (JSON) |
| `POST` | `/api/placar/batch` | Salva múltiplos placares (JSON) |
| `GET` | `/exportar` | Download da planilha XLSX |

### Exemplo de requisição

```bash
# Probabilidade
curl "http://localhost:5000/api/probabilidade?home=Brasil&away=Argentina"

# Salvar placar
curl -X POST http://localhost:5000/api/placar \
  -H "Content-Type: application/json" \
  -d '{"match_id":"R32_1","home_score":2,"away_score":1,"status":"FINISHED"}'
```

### Exemplo de resposta (probabilidade)

```json
{
  "casa": { "nome": "Brasil", "probabilidade": 29.5, "odds": 3.39 },
  "empate": { "probabilidade": 33.4, "odds": 2.99 },
  "fora": { "nome": "Argentina", "probabilidade": 37.1, "odds": 2.69 },
  "media_gols_esperados": 2.92,
  "mercados": {
    "ambos_marcam_sim": 0.79,
    "mais_25_gols": 0.81,
    "menos_25_gols": 0.19
  }
}
```

---

## Formato da Copa 2026

A Copa do Mundo de 2026 é a primeira com **48 seleções**, sediada por **Canadá, México e Estados Unidos**.

### Fase de Grupos

- 12 grupos (A a L) com 4 times cada
- Cada time joga 3 partidas
- Avançam: **1º e 2º de cada grupo** + **8 melhores 3º colocados** = 32 times

### Mata-Mata

| Fase | Datas | Partidas |
|---|---|---|
| 16-avos de Final | 28 Jun a 3 Jul | 32 times → 16 |
| Oitavas de Final | 4 a 7 Jul | 16 times → 8 |
| Quartas de Final | 9 a 11 Jul | 8 times → 4 |
| Semifinais | 14 e 15 Jul | 4 times → 2 |
| Disputa de 3º Lugar | 18 Jul | 2 perdedores |
| Final | 19 Jul | 2 vencedores |

Total: **104 jogos** | Campeão joga **8 partidas**

---

## Dados das Seleções

### Confederações

| Confederação | Vagas | Seleções |
|---|---|---|
| **UEFA** (Europa) | 16 | Alemanha, Áustria, Bélgica, Bósnia, Croácia, Escócia, Espanha, França, Holanda, Inglaterra, Noruega, Portugal, República Tcheca, Suécia, Suíça, Turquia |
| **CAF** (África) | 9 | África do Sul, Argélia, Cabo Verde, Costa do Marfim, Egito, Gana, Marrocos, RD Congo, Senegal, Tunísia |
| **AFC** (Ásia) | 8 | Arábia Saudita, Austrália, Catar, Coreia do Sul, Irã, Iraque, Japão, Jordânia, Uzbequistão |
| **CONMEBOL** (América do Sul) | 6 | Argentina, Brasil, Colômbia, Equador, Paraguai, Uruguai |
| **CONCACAF** (América do Norte) | 6 | Canadá, Curaçao, Estados Unidos, Haiti, México, Panamá |
| **OFC** (Oceania) | 1 | Nova Zelândia |

### Grupos

| Grupo | Times |
|---|---|
| **A** | México, República Tcheca, África do Sul, Coreia do Sul |
| **B** | Canadá, Bósnia e Herzegovina, Catar, Suíça |
| **C** | Brasil, Escócia, Haiti, Marrocos |
| **D** | Estados Unidos, Austrália, Paraguai, Turquia |
| **E** | Alemanha, Curaçao, Costa do Marfim, Equador |
| **F** | Holanda, Japão, Suécia, Tunísia |
| **G** | Bélgica, Egito, Irã, Nova Zelândia |
| **H** | Espanha, Cabo Verde, Arábia Saudita, Uruguai |
| **I** | França, Noruega, Senegal, Iraque |
| **J** | Argentina, Argélia, Jordânia, Áustria |
| **K** | Colômbia, Portugal, Uzbequistão, RD Congo |
| **L** | Croácia, Inglaterra, Gana, Panamá |

---

## Exportação XLSX

A planilha gerada contém **5 abas**:

1. **Grupos** — Times com ranking, classificação e calendário de jogos por grupo
2. **Probabilidades** — Todas as partidas com odds calculadas (casa/empate/fora + gols esperados)
3. **Chaveamento** — Partida a partida do mata-mata com data, horário e estádio
4. **Todas as Seleções** — Lista completa ordenada por ranking FIFA
5. **Legenda** — Significado de todas as siglas usadas no chaveamento

---

## Probabilidades e Apostas

O sistema calcula probabilidades usando o **ranking FIFA** como base:

- **Modelo:** Adaptação do sistema Elo
- **Variáveis:** Diferença de ranking, posição (casa/fora)
- **Mercados disponíveis:**
  - Resultado final (casa/empate/fora) com odds decimais
  - Gols esperados (média)
  - Ambas equipes marcam (sim/não)
  - Total de gols (+2.5 / -2.5)

> **Aviso:** As probabilidades são estimativas matemáticas baseadas em ranking. Não garantem resultados reais. Use com responsabilidade.

---

## Atualização via API da FIFA

O sistema pode buscar resultados ao vivo de três fontes:

| Fonte | Endpoint | Requer Chave? |
|---|---|---|
| **FIFA Official API** | `api.fifa.com/api/v3` | Não |
| **Football-Data.org** | `api.football-data.org/v4` | Sim (gratuita) |
| **API-Sports** | `v3.football.api-sports.io` | Sim (gratuita) |

### Configuração

```bash
# Windows PowerShell
$env:FOOTBALL_DATA_API_KEY="seu_token"
$env:API_SPORTS_KEY="seu_token"
python app.py
```

Sem chaves configuradas, o sistema funciona no modo **offline** com placares editáveis manualmente.

---

## Licença

Este projeto é de uso livre e educacional. Dados das seleções e grupos baseados no sorteio oficial da FIFA para a Copa do Mundo 2026.

---

## Deploy no PythonAnywhere (grátis)

### 1. Crie uma conta
Acesse [pythonanywhere.com](https://www.pythonanywhere.com) e cadastre-se (plano **Beginner** é gratuito).

### 2. Envie o código para o GitHub
Crie um repositório e faça push dos arquivos do projeto, incluindo o `requirements.txt`.

### 3. Clone no PythonAnywhere
No painel, vá em **Consoles** → **bash** e execute:
```bash
git clone https://github.com/seu-usuario/seu-repositorio.git
```

### 4. Crie virtualenv e instale dependências
```bash
mkvirtualenv --python=python3.10 copa2026
pip install -r requirements.txt
```

### 5. Configure o Web App
- Vá em **Web** → **Add a new web app**
- Escolha **Manual configuration** → **Python 3.10**
- Em **Code**:
  - **Source code**: `/home/seu-usuario/copa2026/`
  - **Working directory**: `/home/seu-usuario/copa2026/`

### 6. Configure o WSGI
Clique no link do arquivo WSGI em **Web** e substitua por:
```python
import sys
path = '/home/seu-usuario/copa2026'
if path not in sys.path:
    sys.path.append(path)
from app import app as application
```

### 7. Aponte a virtualenv
Em **Web** → **Virtualenv**: `/home/seu-usuario/.virtualenvs/copa2026`

### 8. Recarregue
Clique em **Reload** — seu app estará em `seu-usuario.pythonanywhere.com`.

### 9. Sincronizar com GitHub (deploy automático)

#### Script de deploy

Crie um arquivo `deploy.sh` no console Bash do PythonAnywhere:
```bash
cd ~/Copa2026
git pull origin main
touch /var/www/seu-usuario_pythonanywhere_com_wsgi.py
```

Dê permissão de execução:
```bash
chmod +x ~/deploy.sh
```

#### Toda vez que alterar o código no GitHub
1. Faça `git push` para o GitHub
2. No PythonAnywhere, abra o **bash** e execute:
   ```bash
   ~/deploy.sh
   ```

#### Opção: agendar atualização automática (plano pago)
No painel **Web** → **Schedule**:
- Adicione uma task com frequência (ex: a cada 6 horas)
- Comando: `bash ~/deploy.sh`

#### Opção: webhook com GitHub Actions
Crie `.github/workflows/deploy.yml` no seu repositório:
```yaml
name: Deploy para PythonAnywhere
on:
  push:
    branches: [ main ]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - run: |
          curl -X POST "https://www.pythonanywhere.com/api/v0/user/${{ secrets.PA_USER }}/webapps/${{ secrets.PA_USER }}.pythonanywhere.com/reload/" \
            -H "Authorization: Token ${{ secrets.PA_TOKEN }}"
```
Gere um token de API em **Account** → **API token** no PythonAnywhere e adicione como secret (`PA_TOKEN` e `PA_USER`) no GitHub.

### Domínio próprio (plano pago)
No plano **Hacker** ($5/mês):
- Em **Web** → adicione `ideiasti.com`
- No DNS do seu domínio, crie um registro **A** apontando para o IP do PythonAnywhere

---

O arquivo `VIDEO_SCRIPT.md` contém um roteiro cena a cena para gravar um vídeo demonstrativo de 5 a 7 minutos, incluindo:

- Abertura e inicialização do app
- Dashboard e visão geral
- Fase de grupos com calendário
- Chaveamento e legenda
- Edição de placares
- Probabilidades e odds
- Exportação XLSX
- Atualização automática
- Executável portátil

Inclui também dicas de produção (OBS Studio, formatos, thumbnail).

---

*Criado em Junho de 2026 • Canadá, México e Estados Unidos*
