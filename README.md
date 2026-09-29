# Chamada dos Notebooks

Site simples para os professores verem, pelo celular ou pelo computador, a lista de alunos de cada turma com o número da chamada. **Aluno nº 1 usa o notebook 1, aluno nº 2 usa o notebook 2**, e assim por diante; na hora de guardar no carrinho, a mesma ordem.

- Os professores entram pelo **QR code** (ou pelo link) e escolhem a turma.
- Dá para **buscar um aluno pelo nome** em todas as turmas.
- Chegou aluno novo? O professor toca em **+ Aluno novo**. O aluno entra no fim da lista da turma, com o próximo número, e aparece para todos os professores.
- Botão **🖨️ Imprimir** para deixar a lista da turma impressa no carrinho.
- Mesmo visual do site de Controle de TI.

## Onde ficam os nomes dos alunos

A lista fica numa **Planilha Google da escola**, no mesmo formato do Excel `Notebooks.xlsx` (uma aba por turma: coluna A = número, coluna B = nome). O site lê e grava nessa planilha por meio de um pequeno código do Apps Script.

Este repositório é público, então **nenhum nome de aluno fica aqui**. Para ver a lista é preciso o código de acesso da escola, e quem entra pelo QR code já recebe o código automaticamente. O RA não aparece no site.

O PROATI pode corrigir qualquer coisa direto na planilha: nome errado, aluno que saiu (apague o nome; o número dele fica vago) etc. Tudo o que é adicionado pelo site também fica anotado na aba **"Adicionados pelo site"** (data, turma, número e nome).

## Configurar (uma vez só, uns 10 minutos)

### 1. Planilha Google

1. Envie o `Notebooks.xlsx` para o Google Drive da conta da escola.
2. Abra o arquivo e vá em **Arquivo → Salvar como Planilhas Google**. O Apps Script só funciona em Planilha Google, não em `.xlsx`.
3. Confira: cada turma é uma aba com nome `6A`, `6B`, …, `1A`, `3A`.

### 2. Apps Script (a ligação entre o site e a planilha)

1. Na Planilha Google: **Extensões → Apps Script**.
2. Apague o que estiver no editor e cole todo o conteúdo de [`apps-script/Codigo.gs`](apps-script/Codigo.gs).
3. Logo no começo do código, em `CODIGO_DE_ACESSO="troque-este-codigo"`, troque `troque-este-codigo` pelo código da escola (ex: `fp-notebooks-2026`). Salve (💾).
4. No topo, escolha a função **`testar`** e clique em **▷ Executar**. O Google vai pedir autorização: escolha a conta → *Avançado* → *Acessar (não seguro)* → *Permitir*. No registro de execução devem aparecer as 14 turmas.
5. **Implantar → Nova implantação** → engrenagem ⚙️ → **App da Web**:
   - Executar como: **Eu**
   - Quem pode acessar: **Qualquer pessoa** (assim os professores não precisam fazer login; quem protege a lista é o código de acesso)
6. Clique em **Implantar** e copie o **URL do app da Web** (termina em `/exec`).

### 3. Site

1. Cole o URL em [`js/config.js`](js/config.js):
   ```js
   const API_URL="https://script.google.com/macros/s/.../exec",ESCOLA="E.E. Francisco Pessoa";
   ```
2. Publique no GitHub Pages: no repositório, **Settings → Pages → Deploy from a branch →** `main` / `(root)`. O site fica em `https://aangelkjpn.github.io/Chamada-Notebooks-Lista/`.
3. Abra o site, digite o código da escola e clique em **📱 QR code**:
   - **🖨️ Imprimir** gera uma folha com o QR code para colar nos carrinhos ou na sala dos professores.
   - **📋 Copiar link** (ou **📤 Enviar**, no celular) gera um link para mandar no grupo dos professores. O link já leva o código.

## Manutenção

- **Mudou o `Codigo.gs`?** Cole a versão nova no Apps Script e vá em **Implantar → Gerenciar implantações → ✏️ → Versão: Nova versão → Implantar**. O URL continua o mesmo.
- **Trocar o código de acesso:** altere `CODIGO_DE_ACESSO` e publique uma nova versão (como acima). Os QR codes e links antigos param de funcionar, então imprima um QR novo pelo site.
- **Turma nova:** crie uma aba com o nome da turma (ex: `7C`) no mesmo formato das outras.
- **Ano novo:** substitua as abas pelas listas novas, mantendo o formato.

## Arquivos

| Arquivo | O que é |
| --- | --- |
| `index.html`, `style.css`, `js/app.js` | O site |
| `js/config.js` | Endereço do Apps Script e nome da escola |
| `apps-script/Codigo.gs` | Código que vai dentro da Planilha Google |
| `libs/` | Bootstrap 5.3.8 e [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) 2.0.4 (MIT), guardados no próprio site como no Controle de TI |

O código está minificado, como no Controle de TI.
