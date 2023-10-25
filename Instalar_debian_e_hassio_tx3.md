Apesar deste tutorial ter sido testado, pode ser expectável adversidades que não podem ser simuladas devido ao hw disponível e momento de referência das versões de sw utilizadas. 

Desse modo, não darei nenhum tipo de suporte a este tutorial, ficando o mesmo ainda disponível para quem quiser por sua conta e risco o usar.

1 – Começamos por fazer download do Balena Etcher - https://www.balena.io/etcher/ ou do https://app.rufeus.org/

2 – Depois fazer download do ArmBian https://github.com/ophub/amlogic-s9xxx-armbian/releases

Devem de usar a versão Armbian_bullseye_xxxxx por ser baseada em debian e estar atualizada com a última versão. As imagens de devem de usar são as Armbian_23.11.0_amlogic_s905x3_bookworm_yyyyy_server_xxxxxxxxxx.img.gz.-
yyyyy = versao da kernel caso nao funcione com a versao mais recente tento com as outras disponíveis 

![image](https://github.com/tv4you2016/Instalacao_armbian_hassio_TX3/assets/83761813/9cd34026-3976-46b0-990d-8fa183a26bf3)


3 – Com uma PEN formatada (podem e devem usar https://www.sdcard.org/downloads/formatter/ para o fazer) vamos flashar a imagem o com o BalenaEtcher ou rufus na PEN.

4 – Quando concluído, abrir uEnv.txt que esta na raiz da pen e substituir a dtb que lá está por uma referente a tua tx3.

![dtb](https://user-images.githubusercontent.com/43672635/212435135-13837ce5-d9b9-43b4-b276-49943e5dc334.png)

![uenv](https://user-images.githubusercontent.com/43672635/212434955-3c84c7e5-49ce-41e8-b596-eefc1b564e4a.png)

5 – Ejetar a PEN do computador e colocar na porta UBS 3.0 na lateral esquerda da TANIX.

6 – Ligar a TANIX ao cabo HDMI e Cabo de Rede. Atenção que a TANIX ainda deve estar desligada da eletricidade.

7 – Com uma agulha (em todos os testes que fiz nunca o precisei de fazer) clicar no botão de reset atrás da TANIX até sentir o clique e vamos ligar a box á energia.

8 – Quando aparecer o símbolo ```TX3``` no monitor/televisão, largar o botão de reset. Nesta altura espera pelo arranque da tua box e no final vai ter um ip atribuído, se tal não acontecer e tiveres certeza que tens o dtb certo (e mesmo que não tenhas) tira e volta a meter o cabo de rede sem desligar a box, (para teres a certeza do dtb só existe uma forma, abrir a box e confirmar na board) e se mesmo assim não obteres ip terás de testar outra dtb e em ultimo caso a outra imagem do armbian como referido no ponto 2.

9 - De seguida vamos fazer acesso por putty ou terminal caso uses o mac, no terminal do Mac: ssh root:1234@IP_BOX e se voltar a pedir a password é 1234

![putty](https://user-images.githubusercontent.com/43672635/212269473-e8f5bc73-39d8-4352-98cf-fd8240dec856.png)

10 - Coloca o ip da box e depois vais seguir as instruções que aparecem no ecrã, (os dados de acesso caso sejam precisos é root e pass 1234).

Quando entrarem vai pedir-vos para colocar um Username e uma Password nova, é só seguir os passos. Nunca esquecer estes dados. São muito importantes.

11- Aqui vamos criar a pass de acesso root

![criar pass](https://user-images.githubusercontent.com/43672635/212269776-ed27a55b-6676-4eca-a8e3-6418d0ad7947.jpeg)

12- agora vamos escolher a opção 1.

![opcao1](https://user-images.githubusercontent.com/43672635/212270022-2681da32-4073-4102-85f8-3daa138bbdd9.jpeg)

13- Aqui vamos escolher o username.

![user name](https://user-images.githubusercontent.com/43672635/212333440-deb4cfc2-1f09-4f76-ae35-2d5c272f1a41.jpeg)

14 - Aqui no menu seguinte apenas vamos dar enter…

![enter](https://user-images.githubusercontent.com/43672635/212333795-0eef3850-bc21-4ff2-8772-10e93a15e41e.jpeg)

15 - Depois disto já estamos prontos para instalar o armbian dando o seguinte comando: ```armbian-install -m yes -a no```

16 - Depois do comando dado irá aparecer uma lista de dtb´s ao qual deveremos escolher o mesmo escolhido no ponto 4, que poderá ser o 512, 514...

![dtb](https://user-images.githubusercontent.com/43672635/212334717-b3a50641-f55c-4f01-b631-e1b2b3f32d07.jpeg)

17 - Finalmente após alguma espera (nunca interrompam o processo) vamos ter esta msg no final…

![sucess](https://user-images.githubusercontent.com/43672635/212335189-f2d2090b-b343-4dc0-9509-d9d5f5859312.jpeg)

18 - Nesta altura devem retirar a pen da vossa box desligar da energia e voltar a ligar.
Vão novamente confirmar o ip da vossa box e fazem o processo de acesso pelo putty de igual forma que na fase inicial.

19 - Agora vamos entrar com o acesso root, metemos então root no user e depois a pass que escolheram e já têm acesso ao armbian. Resta agora correr apenas mais um comando que ira fazer atualizações pendentes do armbian (possivelmente poderá ser feito um reiniciar automático, se isso acontecer é voltar a repetir o ponto 19) assim como a instalação do Home Assistant supervisor.
Este é o comando que devem colar no putty ```curl -sL https://raw.githubusercontent.com/maxcalavera81/Instalacao_armbian_hassio_TX3/main/instalacao_homeassistant.sh | bash -s```
Depois de tudo bem sucedido vai aparecer a seguinte caixa e selecionamos ```qemuarm-64``` com a seta para baixo e damos enter.

![osagents](https://user-images.githubusercontent.com/43672635/212336624-b7161dfe-b0d1-4440-a8aa-589c95bd3abb.jpeg)

19 - Neste momento será instalado o home assistant com o supervisor.

20 - Depois apenas tens de ir ao teu browser e meter http://ip_da_box:8123 e aguardar a instalação.

21 - Após instalação do home assistant, resta criar login ou repor backups. Vais reparar que os alertas do apparmor e cgroups ainda lá continuam, neste momento tens de fazer um reboot ao host para que todas as alterações sejam aplicadas. 

Se quiserem usar o bluetooth da box vamos novamente ao putty e entramos. Tens de entrar com o user root e para isso metes root no user e a pass é a que escolheste,
depois dás o seguinte comando ```sudo armbian-config``` e vai abrir uma caixa de opções.

![network](https://user-images.githubusercontent.com/43672635/212344741-788c48c3-e7e4-4fce-b1b4-25d86ddac8f3.png)

Vamos a opção ```network``` e depois vamos escolher a opção ```bt install``` e aguardam a instalação. 

![bt install](https://user-images.githubusercontent.com/43672635/212345004-a5651ad2-c35e-4fa4-81f5-170757be65f1.png)

Depois de concluído a instalação basta ir ao Home Assistant e fazer a integração do bluetooth.

Boas instalações

Queria só salientar que os créditos da resolução dos alertas apparmor e cgroups assim como a atualização do novo script são todos dos membros Pedro Cardoso (@PCardoso7), Joel Mendes (@tv4you2016) e do Guilherme Sousa. Um muito obrigado para eles pela partilha de conhecimento.
