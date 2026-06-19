# Roteiro para Vídeo — Copa do Mundo 2026 App

**Duração estimada:** 5 a 7 minutos
**Ferramentas para gravar:** OBS Studio (gratuito), ou Gravador de Tela do Windows (Win+Alt+R)
**Resolução sugerida:** 1920x1080

---

## Cena 1 — Abertura (30 segundos)

**Tela:** Área de trabalho com o ícone `Copa2026.exe` em destaque

**Narração:**
"Olá! Neste vídeo vou mostrar o sistema completo de acompanhamento da Copa do Mundo 2026. São 48 seleções, 12 grupos e chaveamento completo do mata-mata, tudo rodando em um aplicativo Python que você pode usar em qualquer computador."

**Ação:** Clicar duas vezes no `Copa2026.exe`

**Texto na tela (sobreposição):**
```
🏆 Copa do Mundo 2026
Canadá • México • Estados Unidos
11 Jun a 19 Jul
```

---

## Cena 2 — Inicialização (20 segundos)

**Tela:** Janela do terminal abrindo e o navegador abrindo automaticamente

**Narração:**
"O servidor inicia automaticamente e o navegador abre na página principal. Você não precisa configurar nada."

**Ação:** Apontar para a URL `http://localhost:5000`

---

## Cena 3 — Dashboard (40 segundos)

**Tela:** Página inicial (Dashboard)

**Narração:**
"Esta é a tela principal. Aqui vemos todos os 12 grupos lado a lado, com as seleções, bandeiras, ranking FIFA e pontuação. No topo, um resumo com 48 seleções, 12 grupos, 104 jogos e 40 dias de torneio."

**Ação:** Passar o mouse sobre alguns grupos, mostrar os cards

**Narração (continua):**
"Rolando para baixo, temos as probabilidades de cada jogo da fase de grupos, com odds calculadas automaticamente com base no ranking FIFA."

**Ação:** Rolar a página para mostrar a seção de probabilidades, clicar em "Detalhes" em um jogo

---

## Cena 4 — Fase de Grupos (50 segundos)

**Tela:** Clicar na aba "Grupos"

**Narração:**
"Na página de Grupos temos a classificação completa de cada chave: pontos, jogos, vitórias, empates, derrotas, gols pró, gols contra, saldo de gols. Os times em verde estão na zona de classificação."

**Ação:** Mostrar o Grupo C (Brasil), apontar para as colunas da tabela

**Narração (continua):**
"Abaixo da tabela, o calendário completo de jogos do grupo com data, horário e estádio. Todos os 72 jogos da fase de grupos estão aqui."

**Ação:** Rolar para baixo e mostrar a tabela de jogos de um grupo

---

## Cena 5 — Chaveamento (1 minuto)

**Tela:** Clicar na aba "Chaveamento"

**Narração:**
"O chaveamento mostra todas as fases eliminatórias lado a lado: 16-avos de final, oitavas, quartas, semis, disputa de 3º lugar e a grande final. Cada partida tem data, horário e estádio."

**Ação:** Mostrar o bracket completo, passar o mouse sobre algumas partidas

**Narração (continua):**
"Repare nas siglas — R32 significa 16-avos, R16 são oitavas, QF quartas, SF semis. O número é o identificador da partida. Se você passar o mouse, aparece uma explicação. E clicando no botão 'Legenda' temos a lista completa."

**Ação:** Clicar no botão "Legenda" para abrir o painel

---

## Cena 6 — Editando Placares (1 minuto)

**Tela:** Ainda no Chaveamento

**Narração:**
"Conforme os jogos vão acontecendo, você pode registrar os placares. Basta clicar no tracinho ao lado do time..."

**Ação:** Clicar no placar `-` de uma partida, digitar um número

**Narração (continua):**
"...digitar o número de gols e pressionar Enter. Depois clique em Salvar. O resultado fica salvo mesmo que você feche o programa."

**Ação:** Clicar em "Salvar", mostrar o badge verde "FINISHED"

---

## Cena 7 — Probabilidades e Odds (45 segundos)

**Tela:** Ainda no Chaveamento, painel lateral direito

**Narração:**
"No painel lateral podemos ver as odds detalhadas. Vou clicar em 'Odds' em uma partida..."

**Ação:** Clicar em "Odds" em uma partida qualquer

**Narração (continua):**
"...e temos: porcentagem de vitória do time da casa, empate e visitante, com odds decimais. Também mostra gols esperados, probabilidade de ambos marcarem e de mais ou menos 2.5 gols. Perfeito para quem gosta de apostas."

---

## Cena 8 — Exportação XLSX (40 segundos)

**Tela:** Topo da página, botão "Exportar XLSX"

**Narração:**
"Para exportar tudo para uma planilha, clique em Exportar XLSX. O download começa automaticamente."

**Ação:** Clicar no botão, depois abrir o arquivo baixado

**Narração (continua):**
"A planilha tem 5 abas: Grupos com calendário de jogos, Probabilidades com todas as odds, Chaveamento completo com datas, a lista de todas as 48 seleções e uma aba de Legenda explicando as siglas."

**Ação:** Navegar pelas abas do Excel mostrando cada uma

---

## Cena 9 — Atualização Automática (30 segundos)

**Tela:** Botão "Atualizar" no topo

**Narração:**
"O sistema tenta buscar resultados ao vivo da API oficial da FIFA a cada 90 segundos automaticamente. Você também pode clicar em 'Atualizar' manualmente para forçar a busca. Se a FIFA estiver disponível, os placares são preenchidos sozinhos."

**Ação:** Clicar em "Atualizar", mostrar a mensagem de atualização

---

## Cena 10 — Executável Portátil (40 segundos)

**Tela:** Explorador de arquivos mostrando o `Copa2026.exe`

**Narração:**
"Para usar em outros computadores, basta copiar o arquivo Copa2026.exe. Não precisa instalar Python nem nenhuma dependência. É só dar dois cliques e o navegador abre automaticamente."

**Ação:** Mostrar o arquivo nas propriedades (33 MB), mostrar um pendrive

**Narração (continua):**
"Os placares que você salvar ficam em um arquivo matches_data.json na mesma pasta do executável. Você pode copiar esse arquivo entre computadores para não perder os resultados."

---

## Cena 11 — Encerramento (20 segundos)

**Tela:** Página inicial do sistema

**Narração:**
"E este é o sistema completo da Copa do Mundo 2026. Código aberto em Python, fácil de usar e pronto para acompanhar todos os 104 jogos do maior torneio de futebol do mundo."

**Texto na tela:**
```
🏆 Copa do Mundo 2026
48 Seleções • 12 Grupos • 104 Jogos
Bom divertimento!
```

**Narração final:**
"Obrigado por assistir! Qualquer dúvida, é só consultar o arquivo README.md que acompanha o projeto."

---

## Dicas de Produção

| Dica | Descrição |
|---|---|
| **Gravação** | Use OBS Studio (gratuito) com resolução 1920x1080, 30 fps |
| **Áudio** | Grave em ambiente silencioso. Um microfone de headset já basta |
| **Mouse** | Ative o destaque do cursor no OBS (Configurações → Avançado → Destacar cursor) |
| **Zoom** | Dê Ctrl+ ou Ctrl- no navegador para ajustar o zoom (recomendo 110%) |
| **Cortes** | Se errar a narração, pause, volte um pouco e continue — edite depois |
| **Edição** | DaVinci Resolve (grátis) ou CapCut para cortar e adicionar legendas |
| **Legendas** | Adicione texto na tela nos momentos-chave (atalhos, nomes de botões) |

### Formatos de Exportação do Vídeo

| Plataforma | Resolução | Formato | Bitrate |
|---|---|---|---|
| YouTube | 1920x1080 | MP4 (H.264) | 15 Mbps |
| WhatsApp | 1920x1080 | MP4 | 5 Mbps |
| Instagram/TikTok | 1080x1920 (vertical) | MP4 | 8 Mbps |

---

## Sugestão de Thumbnail

```
┌─────────────────────────────────────┐
│  🏆 COPA DO MUNDO 2026              │
│                                     │
│  [ 48 seleções ] [ 12 grupos ]      │
│  [ 104 jogos ]   [ Chaveamento ]    │
│                                     │
│  ┌─────────────────────────┐        │
│  │  Sistema Completo em    │        │
│  │  Python + Flask         │        │
│  └─────────────────────────┘        │
│                                     │
│  ▶ 5 min de funcionalidades         │
└─────────────────────────────────────┘
```
