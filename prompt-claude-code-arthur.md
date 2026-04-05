# Prompt para Claude Code — Simulador do Arthur

Crie um arquivo `index.html` — um simulador interativo de humor chamado **"Simulador: Um Dia na Vida do Arthur"**, presente de aniversário de um colega de trabalho.

## Conceito

Jogo de escolhas no estilo text adventure. O jogador é o Arthur. Ele acorda e precisa sobreviver um dia inteiro. Cada cena apresenta uma situação com 2-3 opções — todas levam a consequências cômicas. Não existe caminho "bom": toda escolha tem um custo diferente.

Existem 4 medidores persistentes visíveis no topo durante o jogo:
- **😰 Estresse** (começa em 3, sempre tende a subir)
- **☕ Borras de Café na Pia** (começa em 2, quase nunca desce)
- **💍 Humor da Luísa** (começa em 5, tende a cair — Luísa é a noiva dele)
- **🎩 Dignidade** (começa em 5, tende a cair)

Cada escolha altera esses stats com feedback visual (flash verde/vermelho no stat que mudou).

## Contexto das Piadas Internas (IMPORTANTE — o humor depende disso)

- **Arthur** trabalha na Allos (uma clínica-escola de psicologia) na área de comunicação
- **Luísa** é a noiva dele. Ele vai casar em breve e está atarefado
- Sua marca registrada é **deixar borra de café na pia** e não limpar
- Ele ODEIA a ferramenta **Lovable** (uma ferramenta no-code pra fazer landing pages) — faz ele sofrer
- **Lucas e Alan** são colegas que vivem discordando/brigando e o Arthur tem que mediar
- **Picolé de panetone** é um item absurdo que ele gosta — deve ser tratado com reverência cômica
- Periodicamente alguém quer explicar o **"novo modelo de negócios da Allos"** pra ele, o que gera reuniões intermináveis
- O **mecânico** sempre aparece com problemas novos no carro e custos crescentes
- A **sogra** manda mensagem no pior momento possível

## Estilo Visual

- Fundo escuro com gradiente (tons de slate/indigo: `#0f172a` → `#1e1b4b`)
- Cards com `background: rgba(255,255,255,0.04)`, borda sutil `rgba(255,255,255,0.08)`, border-radius generoso (16-20px)
- Texto principal em `#e2e8f0`, texto secundário em `#94a3b8`, accent em `#818cf8`
- Fonte do corpo: importar **DM Sans** do Google Fonts (weights 400, 500, 600, 700)
- Fonte dos títulos: importar **Space Mono** weight 700 do Google Fonts
- Emojis grandes (32-56px) como ícone de cada cena
- Efeito de typewriter no texto narrativo (letra por letra, ~14ms por caractere), com cursor piscante `▊` na cor accent. Clicar/tocar no texto pula a animação e mostra tudo de uma vez.
- Os botões de escolha só aparecem DEPOIS que o texto termina de digitar (ou se o jogador pular), com animação fadeUp escalonada
- Botões: fundo `rgba(255,255,255,0.06)`, borda `rgba(255,255,255,0.1)`, no hover deslizam levemente pra direita (`translateX(6px)`) e a borda fica accent
- **Mobile-first e responsivo** — vai ser aberto no celular. Max-width do container: ~520px, padding confortável
- Notificações aleatórias pipocando no canto superior direito a cada 2-3 cenas (estilo push notification): mensagens da Luísa, mecânico, Slack, sogra. Aparecem com slideIn, somem após 2s com fadeOut.

## Fluxo do Jogo (10+ cenas encadeadas)

### 1. INTRO — Tela Título
- Emoji grande `🎮` pulsando
- Título: "SIMULADOR" (Space Mono, grande)
- Subtítulo: "Um Dia na Vida do Arthur" (accent color, uppercase, letter-spacing)
- Texto: "Você é Arthur. Está prestes a casar, trabalha na Allos, e tem uma relação complicada com a limpeza. Sobreviva a um dia inteiro sem perder a sanidade.\n\nBoa sorte. Você vai precisar."
- Botão único: "▶ INICIAR SIMULAÇÃO" (estilo destacado, gradiente indigo/violet)
- Nesta tela NÃO mostra os stats

### 2. MANHÃ — O Despertar (⏰)
Título: "06:47 — O Despertar"

Texto: Arthur acorda, vai até a cozinha, encontra a pia com camadas arqueológicas de borra de café (de ontem, anteontem, e possivelmente de 2019).

Opções:
- "Limpar a borra agora" → Cena onde ele tenta limpar, desiste em 30 segundos, e faz mais café por cima. Borra +1 mesmo assim. "A borra é resistente — parece ter criado raízes."
- "Fazer mais café (gerando mais borra)" → Borra +2. "A pia agora tem 3 camadas geológicas. Se um arqueólogo encontrasse essa pia, publicaria na Nature."
- "Fingir que não viu" → Dignidade -1, Luísa -1. "Se eu não olhar, não existe. Filosofia de vida comprovada."

### 3. WHATSAPP EXPLODE (📱)
Título: "07:30 — O Inferno Digital"

Texto mostrando as notificações empilhadas (cada uma em linha separada com emoji):
- 💍 Luísa (12 msgs): "amor vc viu o orçamento do buffet?"
- 🔧 Mecânico (3 msgs): "chefe o carro tá pronto, ficou R$1.800"
- 👔 Allos (8 msgs): "@Arthur urgente"
- 👰 Sogra (6 msgs): "Luísa me disse que vocês ainda não..."
- 🎂 Mãe (2 msgs): "filho feliz aniver meu bebê 🥰🥰"
- 📋 Lucas e Alan (16 msgs): [estão brigando no grupo]

Opções:
- "Luísa (prioridade sobrevivência)" → Luísa +2, mas estresse +1. Ele responde "Vi sim amor, tá ótimo!" sem ter visto nada. Ouve 11 segundos de um áudio de 4 minutos.
- "Allos (prioridade profissional)" → Luísa -2, estresse +1. Enquanto responde o Slack, Luísa manda: "ok, entendi suas prioridades 🙂". O emoji mais perigoso da língua portuguesa.
- "Ninguém. Modo avião. Paz." → Luísa -2, dignidade -1, estresse -1. 3 minutos de paz. Depois lembra da reunião às 9h e que a Luísa tem acesso à localização dele.

### 4. ALLOS — Chegada (🏢)
Título: "09:00 — Chegando na Allos"

Texto: Três coisas te esperam. Cada uma pior que a outra.

Opções (cada uma leva a sua própria cena):
- "Fazer a LP no Lovable (a ferramenta do demônio)" → Estresse +3, Dignidade -2
- "Mediar Lucas vs Alan" → Estresse +2
- "Ouvir o novo modelo de negócios" → Estresse +1, Dignidade -1

### 5a. LOVABLE (💻)
Título: "Lovable: A Provação"

Ele abre o Lovable. Arrasta um bloco, vai pro lugar errado. Desfaz, a página quebra. Refaz, o CSS ignora as instruções. 45 minutos e o botão não centraliza. Questiona as escolhas de vida.

Opções:
- "Eu odeio essa ferramenta" → Segue pro picolé
- "Deixa eu tentar SÓ MAIS UMA VEZ" → Estresse +3. O Lovable deleta o header do SITE INTEIRO. Não o dele. O header do site inteiro. "Não tinha nem como. Mas conseguiu." Depois segue pro picolé.

### 5b. A BRIGA (⚔️)
Título: "O Mediador"

Lucas quer ir pra esquerda, Alan quer ir pra direita. Arthur sugere o centro. Ambos discordam. Agora os dois estão bravos com ELE. Promovido de mediador a bode expiatório.

→ Segue pro picolé

### 5c. MODELO DE NEGÓCIOS (📊)
Título: "O Novo Modelo de Negócios"

"Então Arthur, a ideia é a seguinte..." Slide 1 de 47. Ele acena com a cabeça ritmicamente. Olhos abertos, alma saiu no slide 3. No slide 28 pedem a opinião dele. "Faz sentido, preciso digerir." Ninguém questiona.

→ Segue pro picolé

### 6. PICOLÉ DE PANETONE (🍦)
Título: "12:30 — O Picolé Sagrado"

Momento de paz. O picolé de panetone. Sabor estranho? Sim. Faz sentido? Não. Reconfortante de uma forma inexplicável? Absolutamente. Come em silêncio contemplativo enquanto 14 novas notificações chegam.

Opções:
- "Mais um picolé" → Estresse -2. Cena breve: "Ninguém precisa de motivo pra um segundo picolé de panetone. Você come olhando pro horizonte como um cowboy contemplando a vastidão. Por 4 minutos, tudo faz sentido no universo."
- "Voltar ao trabalho" → Estresse +1

### 7. TARDE (🌅)
Título: "15:00 — A Reta Final"

Luísa: "amor, a gente precisa resolver a lista de convidados HOJE". Mecânico: "chefe, descobri mais um problema no carro 😬". Slack: +23 msgs. Faltam 3 horas.

Opções:
- "Ligar pra Luísa e resolver convidados" → Luísa +2, Estresse +2. Logística combinatória de casamento: Tio Geraldo não pode sentar do lado da Tia Márcia (ódio desde 2007). "Qual dos 47 primos do seu pai?"
- "Responder o mecânico" → Luísa -2. "Melhor trocar a correia também." +R$600. Ele concorda sem saber o que é uma correia. Luísa: "vc não ligou né? 🙂". O emoji de novo.
- "Ir embora mais cedo escondido" → Dignidade -2. Sai às 16h, 43 segundos de liberdade, depois "@Arthur cadê vc?" no Slack e ligação perdida da sogra.

### 8. VOLTA PRA CASA (🏠)
Título: "19:00 — De Volta ao Lar"

Chega em casa. A pia recebe ele. A borra sorri como velha amiga. Luísa olha pra pia. Olha pra ele. Olha pra pia. "Arthur." "..." "A pia." "..." "ARTHUR."

Opções:
- "Eu ia limpar agora mesmo!" → Luísa -1, Dignidade -1
- "Isso é minha coleção, tem valor sentimental" → Luísa -2, Dignidade +1 (pela audácia)
- "Limpar em silêncio e dignidade" → Luísa +1, Dignidade +2. MILAGRE. Luísa tira foto. Manda no grupo da família. A mãe chora. O mecânico manda parabéns.

### 9. TELA DE STATS — Relatório Final

Fundo escuro, estilo "resultado de fase". Mostra:
- Emoji grande + título de ranking baseado no score total (dignidade + luísa - estresse - borra):
  - ≤ -20: 💀 "Desastre Ambulante"
  - ≤ -10: 🩹 "Sobrevivente Acidental"
  - ≤ -3: 😅 "Arthur Médio"
  - ≤ 2: ⭐ "Arthur Premium"
  - > 2: 👑 "Arthur Lendário"
- Os 4 stats finais com seus valores
- Estatísticas extras absurdas em texto (ex: "Vezes que ouviu 'modelo de negócios': ∞")
- Botão "Continuar..." que leva ao cartão de aniversário

### 10. CARTÃO DE ANIVERSÁRIO (🎂)

Tela especial:
- Confetti animado com emojis (🎉🎊🥳🎂✨🍦☕💍) flutuando
- "🎂" grande
- "Feliz Aniversário, Arthur!" em Space Mono
- Card com mensagem sincera:

> Seu dia a dia pode ser caótico — entre borra de café, Lovable, brigas pra mediar, casamento pra planejar e modelos de negócio pra fingir que entendeu.
>
> Mas a real é que a Allos não seria a mesma sem você. A comunicação, as ideias, a energia — tudo isso tem a sua marca (e um pouco de borra de café).
>
> Que esse novo ano traga menos Lovable, mais picolé de panetone, e uma pia limpinha (a gente pode sonhar).
>
> Com carinho de toda a equipe! 💜

- Botão "🔄 Jogar de novo"

## Requisitos Técnicos

- **Arquivo HTML único, self-contained** — CSS e JS inline, ZERO dependências externas (nem Google Fonts — use `system-ui, -apple-system, 'Segoe UI', sans-serif` pro corpo e uma fallback boa pra títulos, ou embede as fontes via `@font-face` com base64 se quiser)
  - CORREÇÃO: pode usar Google Fonts via `<link>` — importar DM Sans (400,500,600,700) e Space Mono (700). Não tem problema pra GitHub Pages.
- **Mobile-first e responsivo** — será aberto no celular. Testar com viewport 375px
- Transições suaves entre cenas (fade/slide)
- Efeito typewriter no texto narrativo
- Os botões de escolha só aparecem após o typewriter terminar (ou se o jogador tocar pra pular)
- Sem frameworks — vanilla HTML/CSS/JS
- Código limpo e organizado, cenas definidas como objetos/dados pra facilitar edição
- O jogo inteiro deve caber confortavelmente num celular sem scroll horizontal

## Tom

Zoeira pesada de grupo de amigos, mas o final é sincero e carinhoso. O humor vem de TODAS as opções serem ruins de formas diferentes. Nenhum caminho é seguro. A graça é o Arthur reconhecer o absurdo da própria rotina.
