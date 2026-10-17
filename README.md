# nicolassa.com.br

Site do Nicolas Sá, cat sitter em Belo Horizonte: landing page + blog.
Feito em Jekyll, hospedado no GitHub Pages e editado pelo Pages CMS. Custo: só o domínio.

## Estrutura

| Caminho | O que é |
|---|---|
| `index.html` | Landing page. Lê os dados de `_data/info.yml`. |
| `_data/info.yml` | WhatsApp, Instagram, bairros, preços, faculdade, loja, foto e perguntas frequentes. |
| `_posts/` | Artigos do blog (um arquivo `.md` por artigo). |
| `blog/index.html` | Lista de artigos em `/blog/`. |
| `_layouts/`, `_includes/` | Moldes das páginas (cabeçalho, rodapé, artigo, link de WhatsApp). |
| `assets/css/site.css` | Estilos (cores e fontes do brand kit). |
| `assets/img/` | Logo, mascote, cenas, favicon e imagem de compartilhamento. |
| `assets/blog/` | Imagens que o Nicolas sobe pelo painel. |
| `.pages.yml` | Define os campos que aparecem no painel do Pages CMS. |
| `CNAME` | Domínio personalizado (`nicolassa.com.br`). |

Campos de preço vazios aparecem como "Consulte". Perguntas frequentes sem resposta não aparecem.

## 1. Publicar no GitHub Pages

1. Crie um repositório **público** (ex.: `nicolassa-site`) e suba todos os arquivos desta pasta, inclusive os que começam com ponto (`.pages.yml`, `.gitignore`).
2. No repositório: **Settings → Pages → Build and deployment**
   - Source: **Deploy from a branch**
   - Branch: **main** / pasta **/(root)**
3. Em 1 a 2 minutos o site sobe. Acompanhe na aba **Actions** (o job "pages build and deployment").

### Testar antes de ter o domínio

Enquanto o nicolassa.com.br não estiver apontado, o site fica em `https://SEU-USUARIO.github.io/nicolassa-site/`. Para funcionar nesse endereço:

1. **Apague o arquivo `CNAME`.** Com ele, o GitHub tenta redirecionar para nicolassa.com.br, que ainda não responde.
2. No `_config.yml`, troque:
   ```yaml
   url: "https://SEU-USUARIO.github.io"
   baseurl: "/nicolassa-site"
   ```

Quando o domínio estiver pronto, volte `url: "https://nicolassa.com.br"`, `baseurl: ""` e recrie o `CNAME` com `nicolassa.com.br`.

## 2. Ligar o domínio nicolassa.com.br

No **Registro.br** → domínio → **DNS** → "Editar zona" (usando os servidores DNS do próprio Registro.br):

| Tipo | Nome | Valor |
|---|---|---|
| A | (vazio / @) | `185.199.108.153` |
| A | (vazio / @) | `185.199.109.153` |
| A | (vazio / @) | `185.199.110.153` |
| A | (vazio / @) | `185.199.111.153` |
| CNAME | `www` | `SEU-USUARIO.github.io` |

Depois, em **Settings → Pages → Custom domain**, confirme `nicolassa.com.br` (o arquivo `CNAME` já preenche isso).
Quando o GitHub validar o DNS (de minutos a algumas horas), marque **Enforce HTTPS**.

## 3. Ligar o painel do Pages CMS

1. Acesse **https://app.pagescms.org** e entre com a sua conta do GitHub.
2. Autorize o acesso ao repositório `nicolassa-site` e abra o projeto.
3. Nas configurações do projeto no Pages CMS, **convide o e-mail do Nicolas**. Ele não precisa ter conta no GitHub.

O Nicolas vai ver duas áreas no painel:

- **Blog**: criar, editar e despublicar artigos. O campo "Publicado" desmarcado salva como rascunho.
- **Informações do site**: WhatsApp, preços, bairros, foto, perguntas frequentes etc.

Cada vez que ele salva, o painel faz um commit no repositório e o GitHub Pages atualiza o site em cerca de 1 minuto.

## 4. Primeiro artigo

Já existe um rascunho em `_posts/2026-10-17-vai-viajar-como-deixar-seu-gato-bem-em-casa.md` com `published: false`.
O Nicolas deve revisar o texto pelo painel e marcar **Publicado** quando estiver de acordo.

## Pré-visualizar no computador (opcional)

**Windows:** instale o **Ruby+Devkit 3.3.x (x64)** pelo https://rubyinstaller.org. Evite o 3.4, que ainda dá conflito com o Jekyll 3.10 usado pelo GitHub Pages. No fim da instalação, deixe rodar o `ridk install` e escolha a opção 3.

Depois, na pasta do projeto:

```bash
gem install bundler
bundle install
bundle exec jekyll serve --livereload
```

Abra http://localhost:4000. Para ver também os rascunhos (`published: false`), use `bundle exec jekyll serve --unpublished`.

Rodando local, mantenha `baseurl: ""` mesmo que esteja testando no github.io.

## Passar o repositório para o Nicolas

1. O Nicolas cria uma conta no GitHub.
2. No repositório: **Settings → General → Danger Zone → Transfer ownership** → usuário dele. Ele aceita pelo e-mail.
3. No repositório transferido: **Settings → Pages**, confira a branch e o domínio personalizado, e salve de novo se preciso.
4. No Registro.br, troque o CNAME `www` para `USUARIO-DELE.github.io`. Os registros A continuam iguais.
5. Na conta dele: **Settings → Pages → Add a domain**, para verificar o nicolassa.com.br com um registro TXT. Isso impede que outra conta use o domínio.
6. No Pages CMS, ele entra com o GitHub e autoriza o repositório. Você pode continuar como colaborador.

O GitHub redireciona o endereço antigo do repositório automaticamente. Se preferir, dá para nunca transferir: o Nicolas edita tudo pelo Pages CMS só com o convite por e-mail.

## SEO já incluído

- Título, descrição e imagem de compartilhamento (WhatsApp, Instagram, Google) via `jekyll-seo-tag`.
- `sitemap.xml` automático (`jekyll-sitemap`) e `robots.txt`.
- Feed do blog em `/blog/feed.xml` (`jekyll-feed`).
- Dados estruturados de negócio local (LocalBusiness com os bairros atendidos) e das perguntas frequentes (FAQPage) na página inicial.

Depois de publicar, cadastre o site no **Google Search Console** e envie o `https://nicolassa.com.br/sitemap.xml`.
O que mais pesa para aparecer em "cat sitter BH" continua sendo o **Perfil da Empresa no Google** com avaliações. Use o mesmo telefone e o mesmo endereço do site.
