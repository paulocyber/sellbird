# Este fork

Fork fino do [Sellbird](https://github.com/ethanplusai/sellbird): o núcleo do original com o mínimo
de mudanças, para continuar recebendo as melhorias dele. As funcionalidades novas ficam no
[bemtevi](../bemtevi), um pacote de extensão separado.

## Onde cada mudança vai

Na ordem, o primeiro lugar que resolve:

1. **Configuração, prompts e skills** na pasta home do Sellbird. Não mexe em código.
2. **bemtevi**, quando dá para fazer com o que a extensão oferece: regras de envio, passos do
   ciclo, comandos, rotas no painel, cabeçalhos, tipos de caixa de e-mail.
3. **PR no original**, quando a mudança serve para todo mundo. Aceito, ele chega aqui no próximo
   merge e deixa de ser diferença nossa.
4. **Patch neste fork**, só em último caso: pequeno, isolado e registrado na tabela abaixo.

## Como manter

Remotos: `upstream` é o original; `origin` é o seu fork no GitHub.

Toda semana:

```bash
git fetch upstream
git merge upstream/main
pip install -e ".[dev]" && python -m pytest -q
cd ../bemtevi && python -m pytest -q
```

- **Um commit por patch,** com a mensagem começando por `fork:`. O comando
  `git log --oneline --no-merges upstream/main..HEAD` lista tudo o que é só nosso.
- **PR aceito no original:** depois do merge, tire a linha da tabela.
- **Sinal para reavaliar a estratégia:** o merge semanal passa de uma hora de conflitos, ou
  passamos a rejeitar mais mudanças do original do que aceitamos.

## Patches do núcleo

| Patch | Por quê | PR no original | Estado |
|---|---|---|---|
| (nenhum ainda) | | | |

## Candidatos

Da avaliação de 11/11/2026, todos bons para PR no original:

- **TLS verificado no IMAP:** `sellbird/integrations/smtp_mail.py:152` e `:232` usam
  `IMAP4_SSL` sem `ssl_context`, e o padrão do Python não verifica o certificado.
- **STARTTLS obrigatório no SMTP** fora das portas 587 e 465 (`smtp_mail.py:133`).
- **Ligar respostas pela thread** (In-Reply-To ou Message-ID), não só pelo remetente
  (`integrations/gmail.py:449` e `:497`).
- **"Aprovar todos" passar pela revisão anti-injeção** (`agents/sender.py:866`,
  `state.py:1358`).
- **`heartbeat()` aceitar o transporte do `Brain`** (`main.py:292`), para usar o modelo via API.
- **Export respeitar a tabela de supressões** (`export.py:47-82`).
- **Descadastro em português no `handler.py`:** até o PR ser aceito, fica no bemtevi.

## Licença

AGPL-3.0, como o original. As mudanças deste fork também são AGPL.
