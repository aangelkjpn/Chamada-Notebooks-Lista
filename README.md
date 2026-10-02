# Chamada dos Notebooks

Site da **E.E. Francisco Pessoa** para organizar a distribuição dos notebooks em sala de aula.

Os professores acessam pelo QR code ou pelo link, escolhem a turma e veem a lista de alunos com o número da chamada. A regra é simples: **o aluno nº 1 usa o notebook 1, o aluno nº 2 usa o notebook 2**, e assim por diante. Na hora de guardar no carrinho, a mesma ordem.

**🔗 [Ver online](https://aangelkjpn.github.io/Chamada-Notebooks-Lista/)** · a lista de alunos é protegida pelo código de acesso da escola.

## O que o site faz

- Mostra a lista de alunos de cada turma, com o número da chamada
- Busca alunos pelo nome em todas as turmas
- Permite adicionar alunos novos, que entram no fim da lista com o próximo número
- Imprime a lista da turma e a folha com o QR code
- Funciona no celular e no computador

## Como funciona

A lista de alunos fica numa Planilha Google da escola, e o site lê e grava nela por meio do Google Apps Script. Nenhum dado de aluno fica neste repositório, e o acesso à lista é protegido por um código da escola.

## Tecnologias

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Bootstrap](https://img.shields.io/badge/Bootstrap-7952B3?style=flat&logo=bootstrap&logoColor=white)
![Google Apps Script](https://img.shields.io/badge/Google_Apps_Script-4285F4?style=flat&logo=google&logoColor=white)

- **HTML, CSS e JavaScript** puros, com **Bootstrap 5**
- **Google Apps Script + Planilhas Google** como back-end
- **GitHub Pages** para hospedar o site

## Como configurar

1. Na Planilha Google da escola, crie uma aba por turma (ex.: `6A`, `1B`), com o número da chamada na coluna A e o nome do aluno na coluna B.
2. Em **Extensões → Apps Script**, cole o conteúdo de `apps-script/Codigo.gs` e troque o `CODIGO_DE_ACESSO`.
3. Publique como **App da Web** e copie a URL gerada.
4. Cole essa URL no `API_URL` do arquivo `js/config.js`.

## Estrutura

```
├── index.html            # Página principal
├── style.css             # Estilos
├── js/
│   ├── config.js         # URL da API e nome da escola
│   └── app.js            # Lógica do site
├── apps-script/
│   └── Codigo.gs         # Back-end no Google Apps Script
└── libs/                 # Bootstrap e gerador de QR code
```

---

Criado durante o estágio no **PROATI (SEDUC-SP)** · Desenvolvido por [Angelo Gabriel](https://github.com/aangelkjpn)
