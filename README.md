# Multi View Browser (com suporte a extensões)

Navegador Android com múltiplas abas (cada uma sua própria WebView) e um
sistema de **extensões** (scripts JavaScript) que, uma vez adicionados,
passam a rodar automaticamente em **todas as abas — abertas e futuras**.

## O que já vem pronto

- Múltiplas abas com faixa de abas no topo (abrir, fechar, trocar)
- Barra de endereço com busca/URL
- Botões voltar / avançar / recarregar
- Suporte a `target="_blank"` e `window.open()` abrindo em nova aba
- Tela "Extensões" (ícone de peça de quebra-cabeça): adicionar, editar,
  ativar/desativar e excluir scripts
- Cada extensão tem:
  - **Nome**
  - **Padrão de site** (`*` = todos os sites, ou um trecho do domínio)
  - **Código JavaScript** (colado manualmente ou importado de um arquivo `.js`)
- O script é injetado automaticamente em `onPageStarted` e `onPageFinished`
  de **toda WebView de toda aba**, então não existe configuração por aba —
  é tudo centralizado em `ExtensionManager.kt`.

## Como abrir e compilar

1. Instale o **Android Studio** (https://developer.android.com/studio) — é
   gratuito.
2. Abra o Android Studio → `File > Open` → selecione a pasta `MultiViewBrowser`
   (a raiz, onde está o `settings.gradle.kts`).
3. O Android Studio vai pedir para sincronizar o Gradle automaticamente —
   aceite (ele baixa o Gradle/Wrapper sozinho, não precisa configurar nada
   manualmente).
4. Espere o "Gradle Sync" terminar (barra de progresso no rodapé).

## Como testar

- Conecte um celular Android (com Depuração USB ativada) ou crie um emulador
  pelo `Device Manager`.
- Clique no botão verde de "Run" (▶) no Android Studio.

## Como gerar o APK assinado (para instalar fora do Android Studio)

1. Menu `Build > Generate Signed Bundle / APK...`
2. Escolha `APK` → `Next`
3. Clique em `Create new...` para criar seu keystore (defina senha, nome,
   validade) — isso é a sua assinatura própria, guarde esse arquivo `.jks`
   com segurança, você vai precisar dele para futuras atualizações do app.
4. Escolha a variante `release` → `Finish`.
5. O APK assinado aparece em `app/release/app-release.apk`. Esse é o arquivo
   que você pode instalar em qualquer aparelho (ative "Instalar de fontes
   desconhecidas" no Android).

## Adicionando sua extensão

1. Abra o app → toque no ícone de peça de quebra-cabeça (extensões).
2. Toque no `+`.
3. Dê um nome, defina em quais sites deve rodar (`*` para todos) e cole ou
   importe o código JavaScript.
4. Salvar. A partir daí, o script roda em todas as abas abertas e em
   qualquer aba nova — sem precisar repetir nada.

## Observação importante

Esse projeto **não inclui** a extensão "Link Skipper" que você enviou
anteriormente — ela foi desenhada para evadir detecção de bot e furar
sistemas de monetização por anúncios de terceiros (Linkvertise, AdFly,
Vetisc, etc.), e isso eu não posso ajudar a empacotar/distribuir. O sistema
de extensões aqui é genérico: você pode colocar qualquer script JS que não
tenha esse propósito (dark mode forçado, autofill, bloqueio de cookies,
tradução automática, CSS customizado, etc).
