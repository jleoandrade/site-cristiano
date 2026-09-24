# Como publicar o site: GitHub + Vercel

Este pacote é o site completo, com uma página inicial (home) que pergunta qual modelo o visitante quer ver:

```
site/
├── index.html            ← home: "Qual modelo de site você gostaria de ver?"
├── assets/
│   ├── preview-modelo-1.jpg
│   └── preview-modelo-3.jpg
├── modelo-1/             ← Modelo 1 — Noturno
│   ├── index.html
│   └── assets/cristiano.jpg
└── modelo-3/             ← Modelo 3 — Blueprint tech
    ├── index.html
    └── assets/cristiano.jpg
```

No ar, os endereços ficam assim:
- `https://site-cristiano.vercel.app/` → home com a escolha
- `https://site-cristiano.vercel.app/modelo-1/`
- `https://site-cristiano.vercel.app/modelo-3/`

Não precisa instalar nada nem "compilar": é HTML puro, e a Vercel publica como está.

---

## 1. Personalize

1. Descompacte o arquivo e copie a pasta `site` para um lugar fácil, por exemplo `Documentos/site-cristiano`.
2. Abra **`modelo-1/index.html`** e **`modelo-3/index.html`** num editor de texto (recomendo o **VS Code**, gratuito: https://code.visualstudio.com). Nos **dois** arquivos, use **Ctrl+F** para buscar e trocar:

| Buscar | Trocar por |
|---|---|
| `5500000000000` | seu WhatsApp: 55 + DDD + número, só dígitos (ex.: `5511987654321`) |
| `(00) 00000-0000` | seu WhatsApp como deve aparecer na tela |
| `seuemail@dominio.com.br` | seu e-mail |
| `[Sua cidade / região]` | sua cidade ou região de atendimento |

3. **Colocar a sua logo**
   - Salve o arquivo da logo como `logo.png` dentro da pasta `assets` de **cada** modelo (`modelo-1/assets` e `modelo-3/assets`) e também na pasta `assets` da home.
   - Nos três `index.html` (home, modelo 1 e modelo 3), busque `<span class="brand-mark">C</span>` e troque o trecho inteiro
     `<span class="brand-mark">C</span><span class="brand-txt">…</span>` por:
     ```html
     <img src="assets/logo.png" alt="Cristiano – Tecnologia e Gestão de Serviços" height="44">
     ```
4. **Foto em alta qualidade (recomendado):** a foto atual foi recortada do cartaz e tem resolução baixa. Se tiver o arquivo original, salve-o como `cristiano.jpg` (mesmo nome) em `modelo-1/assets` e `modelo-3/assets`, substituindo o atual.
5. **Teste:** dê dois cliques no `index.html` da pasta `site`: abre a home, e os botões levam a cada modelo, exatamente como vai ficar na internet.

---

## 2. Colocar no GitHub (pelo navegador, sem instalar nada)

1. Crie uma conta em https://github.com (se ainda não tiver).
2. No canto superior direito, clique em **+** → **New repository**.
3. Preencha:
   - **Repository name:** `site-cristiano`
   - **Public** ou **Private** (os dois funcionam com a Vercel)
   - Deixe o resto como está e clique em **Create repository**.
4. Na página do repositório vazio, clique no link **uploading an existing file**.
5. Abra a pasta `site` no computador, selecione **tudo o que está dentro dela** (`index.html`, `assets`, `modelo-1`, `modelo-3`) e arraste para a página do GitHub.
   > Importante: arraste o **conteúdo** da pasta, não a pasta `site` em si. O `index.html` da home precisa ficar na raiz do repositório.
6. Em **Commit changes**, escreva algo como `Primeira versão do site` e clique em **Commit changes**.
7. Confira: a lista do repositório deve mostrar `index.html`, `assets/`, `modelo-1/` e `modelo-3/`.

<details>
<summary>Alternativa pelo terminal (se você usa Git)</summary>

```bash
cd caminho/para/site-cristiano
git init
git add .
git commit -m "Primeira versão do site"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/site-cristiano.git
git push -u origin main
```
</details>

---

## 3. Publicar na Vercel

1. Acesse https://vercel.com e clique em **Sign Up** → **Continue with GitHub** (use a mesma conta do GitHub).
2. No painel, clique em **Add New…** → **Project**.
3. Na lista "Import Git Repository", encontre `site-cristiano` e clique em **Import**.
   - Se o repositório não aparecer: clique em **Adjust GitHub App Permissions** e libere o acesso a ele.
4. Na tela de configuração:
   - **Framework Preset:** `Other`
   - **Root Directory:** `./` (padrão)
   - **Build and Output Settings:** deixe tudo em branco/padrão
5. Clique em **Deploy**. Em menos de um minuto o site fica no ar, num endereço como
   **`https://site-cristiano.vercel.app`**
   (se esse nome já existir, a Vercel adiciona um sufixo; dá para ajustar em **Settings → Domains**).

---

## 4. Como atualizar o site depois

Toda alteração enviada ao GitHub é publicada automaticamente pela Vercel.

- Pelo navegador: no GitHub, abra o arquivo (ex.: `modelo-1/index.html`) → ícone de lápis (**Edit**) → altere → **Commit changes**.
- Para trocar uma imagem: entre na pasta `assets` correspondente no GitHub → **Add file → Upload files** → envie com o mesmo nome → **Commit changes**.
- Em cerca de 30 segundos a nova versão está no ar.

---

## 5. (Opcional) Usar um domínio próprio

Se tiver um domínio (ex.: `cristianoti.com.br`, registrado no registro.br):

1. Na Vercel, abra o projeto → **Settings → Domains** → digite o domínio → **Add**.
2. A Vercel mostra os registros de DNS (normalmente um registro **A** e um **CNAME**).
3. No painel onde o domínio foi registrado, crie esses registros. Em algumas horas o domínio passa a abrir o site, já com HTTPS (cadeado).

---

## Quando escolher o modelo definitivo

Se decidir ficar só com um modelo e tirar a home de escolha: no repositório, apague o `index.html` e a pasta `assets` da raiz, e mova o conteúdo da pasta do modelo escolhido (`index.html` e `assets`) para a raiz. O site passa a abrir direto nesse modelo.
