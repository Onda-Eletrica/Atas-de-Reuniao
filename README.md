# Atas de Reunião
Aqui está listado todas as atas de Reunião Geral do Onda Elétrica.
## Importante
>As atas estão organizadas na pasta ANO e os arquivos listados no formado MÊS-DATA.md 
>
>md é apenas um formato de arquivo markdown, editável em qualquer editor de texto / bloco de notas que segue algumas regrinhas para ser escrito
>Dicas de como escrever: https://docs.github.com/pt/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax

# Como editar o repositório no Visual Studio Dev (Versão Web)

![alt text](/ArquivosExtras/github_dev.gif)

# Como conectar o repositório ao editor do StackEdit

Clique no símbolo do StackEdit no canto superior direito, depois em 'Workspaces' e depois 'Add a GitHub workspace'. **Importante:** ao fazer login, coloque que a branch seja 'main' (ou a que você desejar). **Deixar vazio dá erro de sincronização 402**

![alt text](/ArquivosExtras/TelaLogin.png)

Prossiga, e quando estiver na tela solicitando "Conceder acesso aos seus repositórios privados" ("Grant access to your private repositories"), abra o console do desenvolvedor (CTRL+SHIFT+i e clique na aba 'Console') e cole as seguintes linhas.
FONTE: https://github.com/benweet/stackedit/issues/1755#issuecomment-918949789

~~~
window.XMLHttpRequest =  class MyXMLHttpRequest extends window.XMLHttpRequest {
  open(...args){
    if(args[1].startsWith("https://api.github.com/user?access_token=")) {
      // apply fix as described by github
      // https://developer.github.com/changes/2020-02-10-deprecating-auth-through-query-param/#changes-to-make
  
      const segments = args[1].split("?");
      args[1] = segments[0]; // remove query params from url
      const token = segments[1].split("=")[1]; // save the token
      
      const ret = super.open(...args);
      
      this.setRequestHeader("Authorization", `token ${token}`); // set required header
      
      return ret;
    }
    else {
      return super.open(...args);
    }
  }
}
~~~

Após isso, faça o login normalmente. Caso aconteça algum erro ao exibir ao editor (exceto os erros 404, 402 e 400) ou ele nem abra, atualize a página e pronto. Caso seja os erros **404, 402 e 400**, refaça os passos acima.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1Mzg4ODk4NjUsLTE5NTI1MjYwMzAsLT
kxNjU4OTQ0LC0xNDg2MzYzODQsLTk5NzgxNzU5MCwtMTY4Nzgx
NTA5NywtMTMwMzI2MDg4NF19
-->