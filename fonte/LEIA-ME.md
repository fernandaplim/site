# Como publicar o site da Mila

A pasta `publicar/` já contém o site pronto. Só estes 5 arquivos precisam ir para o servidor:

- `index.html` — home
- `privacidade.html` — política de privacidade
- `termos.html` — termos de uso
- `robots.txt`
- `sitemap.xml`
- `CNAME` e `.nojekyll` — apenas se publicar no GitHub Pages

Cada HTML é autossuficiente: fontes, estilos e scripts estão embutidos. Não há pasta de assets, build nem servidor de aplicação.
(Os arquivos `.dc.html` nesta pasta são a fonte usada para gerar os HTML — não precisam ser publicados.)

## Opção 1 — arrastar para uma hospedagem estática (mais rápido)

1. Acesse **Netlify Drop** (app.netlify.com/drop) ou **Cloudflare Pages** ou **Vercel**.
2. Arraste os 5 arquivos (ou a pasta contendo só eles).
3. O site sobe em segundos numa URL provisória.
4. Em *Domains* / *Custom domain*, adicione `milaresolve.com` e `www.milaresolve.com`.
5. No painel do seu registrador de domínio, aponte o DNS conforme as instruções que a hospedagem mostrar (normalmente um registro A e um CNAME para `www`).
6. HTTPS é emitido automaticamente. Confira que `https://milaresolve.com` abre.

## Opção 1-B — GitHub Pages (grátis, com domínio próprio)

Funciona: o site é totalmente estático. Inclusos nesta pasta o `CNAME` (domínio) e o `.nojekyll` (desliga o Jekyll, que não é necessário aqui).

1. Crie um repositório no GitHub — pode ser público ou privado (Pages em repositório privado exige plano pago; se for grátis, use público).
2. Suba estes arquivos **na raiz** do repositório: `index.html`, `privacidade.html`, `termos.html`, `robots.txt`, `sitemap.xml`, `CNAME`, `.nojekyll`. Pela web: *Add file → Upload files* (o `.nojekyll` pode não aparecer no seletor por ser oculto — crie com *Add file → Create new file*, nome `.nojekyll`, conteúdo vazio).
3. Em **Settings → Pages**: em *Source* escolha **Deploy from a branch**, branch `main`, pasta `/ (root)`. Salve.
4. Em *Settings → Pages → Custom domain*, confirme `milaresolve.com` (o `CNAME` já preenche) e marque **Enforce HTTPS** depois que o certificado for emitido (leva alguns minutos até algumas horas).
5. No DNS do registrador do `milaresolve.com`, crie:
   - 4 registros **A** para `@` apontando para `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - 4 registros **AAAA** (opcional, IPv6): `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`
   - 1 registro **CNAME** para `www` apontando para `SEU-USUARIO.github.io`
6. A cada `git push` na `main` o site republica sozinho.

**Atenção:** se o repositório for público, os arquivos ficam visíveis — é só o site institucional, sem chaves nem dados, então tudo bem. Nunca suba tokens ou `.env` nesse repositório.

## Opção 2 — servidor próprio / hospedagem tradicional

Envie os 5 arquivos por FTP/SFTP para a pasta pública do domínio (`public_html`, `www` ou `htdocs`). O `index.html` deve ficar na raiz.

## Depois de publicar

1. **Google Search Console** — adicione a propriedade `milaresolve.com`, copie a meta tag de verificação e cole no lugar do comentário `SLOT: meta tag de verificação do Google Search Console` nos arquivos `.dc.html`; gere os HTML de novo e publique.
2. **Verificação do OAuth do Google** — na tela de consentimento, informe:
   - Página inicial: `https://milaresolve.com`
   - Política de privacidade: `https://milaresolve.com/privacidade.html`
   - Termos de uso: `https://milaresolve.com/termos.html`
   As três URLs precisam estar no ar, no mesmo domínio verificado, antes de submeter a revisão.
3. Teste os botões "Conversar com a Mila" no celular — devem abrir o WhatsApp com a mensagem "oi Mila" preenchida.

## Se quiser URLs sem `.html`

O GitHub Pages **não** faz regravação de URL — lá as páginas ficam em `/privacidade.html` mesmo (ou crie pastas `privacidade/index.html`, e eu ajusto os links). Nas outras hospedagens dá: no Netlify, crie um arquivo `_redirects` com:

    /privacidade  /privacidade.html  200
    /termos       /termos.html       200

Avise que eu ajusto os links internos das páginas para as URLs limpas.
