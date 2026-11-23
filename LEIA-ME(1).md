# Pétala · Planner — guia de instalação e uso

Agenda pessoal completa (agenda, tarefas, hábitos, notas, metas, gamificação e finanças) feita como **PWA**: um site que se instala na tela inicial do iPhone e funciona como app, inclusive offline.

## 1. Colocar o app no ar (uma vez só, ~5 minutos)

O iPhone só instala um app web a partir de um endereço `https://`. Escolha uma opção gratuita:

### Opção A: GitHub Pages (recomendada, fica no ar para sempre)
1. Crie uma conta grátis em github.com.
2. Clique em **New repository**, nome `petala`, marque **Public** e crie.
3. Clique em **uploading an existing file** e arraste **todo o conteúdo da pasta `petala`** (index.html, manifest.webmanifest, sw.js e a pasta icons).
4. Clique em **Commit changes**.
5. Vá em **Settings → Pages**, em *Branch* escolha `main` e `/ (root)`, e salve.
6. Em 1 ou 2 minutos o app estará em `https://SEU-USUARIO.github.io/petala/`.

> Só o código do app fica público. **Seus dados nunca saem do iPhone**: não há servidor, conta nem banco de dados online.

### Opção B: Netlify Drop
1. Acesse app.netlify.com/drop, crie uma conta grátis.
2. Arraste a pasta `petala` inteira para a página.
3. Use o endereço `https://….netlify.app` gerado.

## 2. Instalar no iPhone
1. Abra o endereço no **Safari** (precisa ser o Safari).
2. Toque em **Compartilhar** (quadrado com seta para cima).
3. Toque em **Adicionar à Tela de Início** → **Adicionar**.
4. Abra pelo ícone da flor. Ele abre em tela cheia, sem barra do navegador, e funciona offline.

## 3. Seus dados
- Ficam salvos **só neste aparelho**, automaticamente, a cada alteração.
- **Faça backup** de vez em quando: Perfil → Configurações → Exportar. Para restaurar: Importar.
- ⚠️ Se você **remover o app da tela inicial**, o iOS apaga os dados dele junto. Exporte antes.
- Os dados do app instalado são separados dos dados do Safari: use sempre pelo ícone.

## 4. Limitações do iPhone (e as alternativas usadas)
| Recurso | Limitação | Alternativa no app |
|---|---|---|
| Notificações | No iOS 16.4+, um app web instalado pode notificar, mas **não consegue agendar alarmes com o app fechado** sem um servidor | Lembretes funcionam com o app aberto/recém-usado; e o botão **"Adicionar ao Calendário do iPhone"** envia compromissos (com alarme) ao app Calendário, que avisa mesmo com tudo fechado |
| Conexão bancária | Não usada, por escolha (privacidade) | Lançamentos manuais, recorrências automáticas e controle de cartão |
| Sincronizar entre aparelhos | Sem servidor, não há sincronização | Exportar/Importar backup |

## 5. Como funciona o controle financeiro
- **Saldo** = saldo inicial + entradas recebidas − despesas pagas − pagamentos de fatura ± transferências − depósitos em metas.
- **Compra no cartão** entra na fatura e **não** desconta do saldo. O saldo só muda quando você registra o **pagamento da fatura**. Nos relatórios a compra conta como despesa na data em que foi feita, e o pagamento não é contado de novo: **sem duplicidade**.
- **Parcelado**: cada parcela vai para a fatura do seu mês.
- **Fixas/recorrentes**: ative "Repetir todo mês" e o app cria o lançamento como pendente todo mês. Toque em "Paguei"/"Recebi" para confirmar.
- Valores aceitam o formato brasileiro: `1.234,56`, `2.000`, `89,90`.

## 6. Gamificação (XP)
Tarefa baixa 10 · média 15 · alta 25 · compromisso 10 · hábito 8 · etapa de meta 15 · meta concluída 60 · registro financeiro 4 (até 5 por dia) · depósito em meta 10 · conquista 25 · desafios 10 a 70.
Desmarcar algo devolve o XP, então não dá para "farmar" pontos. Registrar despesas dá XP pelo **controle**, nunca pelo valor gasto.

## 7. Estrutura do código (para atualizar depois)
O arquivo `index.html` é gerado a partir do código-fonte organizado:
```
src/
  index.html            casca da página
  css/                  base (cores/tokens), components, views
  js/core/              utils (datas, R$), icons, store (dados), ui (sheets, toasts)
  js/game/              gamification (XP, níveis, desafios, conquistas)
  js/views/             home, agenda, tasks, habits, notes, goals, profile
  js/finance/           fin-core (cálculos), fin-charts, fin-views, fin-forms
pwa/                    manifest, service worker, ícones
build.py                junta tudo em dist/petala/
```
Para mudar as cores, edite as variáveis no topo de `src/css/base.css`. Para mudar as categorias padrão, `src/js/core/store.js`. Depois rode `python3 build.py` e envie a pasta `dist/petala` de novo para o GitHub (o app instalado se atualiza sozinho na próxima abertura com internet).
