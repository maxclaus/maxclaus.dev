+++
title = "Failed to generate a user instance of SQL Server ..."
+++

Ao abrir pelo Visual Studio, um arquivo .mdf, a conexão falhava e aparecia a seguinte mensagem _"Failed to generate a user instance of SQL Server due to a failure in starting the process for the user instance. The connection will be closed."_.

Após procurar um pouco na internet achei a seguinte solução:

1.  Acesse o seguinte local - `c:Documents and Settings\[user\]Local SettingsApplication DataMicrosoftMicrosoft SQL Server Data`.
2.  Exclua a pasta `SQLEXPRESS`

O motivo que encontrei deste erro é que o nome da instância tanto no Express 2005 como no 2008 era SQLEXPRESS, e os arquivos de configurações de usuário estavam errados. E após excluir, os arquivos são criados novamente com uma nova configuração.

