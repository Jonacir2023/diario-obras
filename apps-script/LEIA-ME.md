# Apps Script do Diário de Obras

`DiarioObras.gs` é o script unificado (Pauta · CheckIn · Diário · Fotos · Backup), com três correções
sobre a versão anterior (`DiarioObrasv5.gs`):

1. **Sincronização com um arquivo por aparelho.** Antes, cada envio criava um arquivo novo de ~560 KB no
   Drive (centenas por dia) e os antigos iam para a lixeira, que continua contando na cota. Agora o envio
   sobrescreve `sync_<aparelho>.json`. Backups datados (manual/diário) ficam limitados a 10.
2. **`buscar-ultimo` aceita `excluir=<aparelho>`.** Cada aparelho recebe sempre o que os *outros* enviaram,
   mesmo quando o seu próprio envio é o mais recente.
3. **`lista-mes` e `carregar` normalizam a data.** A célula Data da planilha pode ser do tipo Data; comparar
   o texto dela com `2026-10` nunca casava e o mês saía vazio. O calendário do app usa `lista-mes`.

## Como implantar

1. Abra a planilha → Extensões → Apps Script.
2. Cole o conteúdo de `DiarioObras.gs` no lugar do código atual.
3. Implantar → Gerenciar implantações → editar (lápis) → Versão: **Nova versão** → Implantar.
   A URL `/exec` continua a mesma.

## Se as fotos pararam de subir: confira a cota do Drive

1. Abra <https://drive.google.com/settings/storage> (conta dona do script).
2. Se estiver perto de cheio: Drive → Lixeira → **Esvaziar lixeira**. É onde ficaram os backups antigos.
3. Teste enviando uma foto pelo app. O app agora mostra o erro real devolvido pelo Google.
