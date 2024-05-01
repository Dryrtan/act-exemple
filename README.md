Recentemente, precisei implementar alguns workflows do GitHub Actions para fazer o deploy de alguns projetos da empresa onde trabalho. Essa tarefa se revelou tediosa e repetitiva, pois a cada alteração no arquivo .yml, eu precisava realizar um commit para verificar se o workflow estava funcionando corretamente. Decidi pesquisar sobre o assunto e, para minha surpresa, não encontrei uma maneira para testar esses workflows sem fazer commits pra o GitHub(ou talvez eu que não tenha procurado mais). Pensei comigo mesmo: "Que dificuldade há em adicionar um botão para executar o código antes de realizar o commit?" Mas, como costuma acontecer, o que parece simples na mente do usuário nem sempre é tão simples de implementar.

  Decidi pesquisar um pouco mais e acabei encontrando o [act](https://github.com/nektos/act) que resolve esse problema de fazer commits repetidamente. De acordo com o README do projeto, ele funciona da seguinte maneira:
> Quando você executa act ele lê em seus workflows do GitHub de .github/workflows/e determina o conjunto de ações que precisam ser executadas. Ele usa a API Docker para extrair ou construir as imagens necessárias, conforme definido em seus arquivos de workflow e, finalmente, determina o caminho de execução com base nas dependências que foram definidas. Depois de obter o caminho de execução, ele usa a API Docker novamente para executar contêineres para cada ação com base nas imagens preparadas anteriormente. As variáveis ​​de ambiente e o sistema de arquivos são todos configurados para corresponder ao que o GitHub fornece.
---
## Mão na massa
### Instalando
Para fazer o uso do act é nescessario possuir o Docker instalado na sua maquina, no meu caso estou executando atraves do WSL2 e funciona sem problemas, dê uma olhada [aqui](https://nektosact.com/installation/index.html) sobre os requisitos e sobre a forma de instalar no Linux, Windows e Mac.

---

### Executando
Na primeira execução, o act solicitará o download da imagem padrão a ser utilizada. Optei pela 'Medium' e acredito que seja adequada para a maioria dos casos.
![img1](https://imgur.com/inmC89c.png)


Para iniciar, execute o comando act na raiz do seu projeto. Por padrão, ele executará o workflow associado ao evento on: push:. As imagens necessárias serão baixadas e as instruções contidas no arquivo .yml serão executadas.

![img2](https://imgur.com/UDtaQrR.png)


Para executar um workflow de pull request, utilize o comando `act pull_request` o mesmo vai funcionar para release, schedule, create e etc.

![img3](https://imgur.com/ivHAWRx.png)


Um exemplo de workflow que requer secrets para ser executado: `act -s NAME="Dryrtan" -s PASSWORD="admin123"`

![img4](https://imgur.com/HvaOdOx.png)

---
### Conclusão
O Act é uma excelente ferramenta para desenvolver workflows no Git Actions, especialmente para aqueles sem experiência prévia na criação desses processos. Além disso, ele é ótimo para realizar experimentos e testes, permitindo que os usuários testem suas configurações antes de implantá-las em ambientes de produção.

https://nektosact.com/

https://github.com/nektos/act
