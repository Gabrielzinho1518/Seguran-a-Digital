# Seguranca-Digital

1. Preparação do servidor (Linux)

Atualize o gerenciador de pacotes e instale o vsftpd:

sudo apt update
sudo apt install vsftpd


Crie um usuário de teste:

sudo adduser ftpuser
sudo passwd ftpuser


Inicie e habilite o serviço:

sudo systemctl start vsftpd
sudo systemctl enable vsftpd


Verifique o IP do servidor:

ip a


Anote o IP (ex.: 192.168.1.10).

2. Preparar a captura (Linux)

Abra o Wireshark com privilégios:

sudo wireshark


Selecione a interface de rede correta (eth0 / wlan0).

Configure filtro de exibição (após captura) ou de captura se desejar:

Filtro de exibição recomendado: ftp

Filtro por IPs: ip.addr == 192.168.1.10 && ip.addr == 192.168.1.20

Inicie a captura antes de iniciar a conexão no Windows.

3. Conectar via FTP (Windows)

No cmd:

ftp 192.168.1.10


Insira ftpuser e a senha quando solicitado.

Execute comandos simples (por exemplo ls, get, put) para gerar tráfego.

Encerre a sessão (bye) e depois pare a captura no Wireshark.

4. Análise no Wireshark

Aplique o filtro ftp no painel de exibição.

Localize pacotes com USER e PASS.

Use Follow → TCP Stream (botão direito em um pacote TCP) para visualizar toda a sessão em ordem.

Capture prints onde USER e PASS aparecem claramente.

Comandos úteis (apêndice)

Instalar vsftpd:

sudo apt install vsftpd


Criar usuário:

sudo adduser ftpuser


Ver IP:

ip a


Iniciar Wireshark:

sudo wireshark


Conectar via cmd (Windows):

ftp 192.168.1.10

Como gerar o PDF final

Cole o texto do relatório em um editor (LibreOffice Writer, Microsoft Word).

Insira as imagens capturadas nas seções apropriadas com legendas (Figura 1, Figura 2, ...).

Exporte como PDF (Arquivo → Exportar como PDF).

Alternativa via linha de comando (se preferir): use pandoc para converter Markdown para PDF (requer LaTeX instalado):

pandoc relatorio.md -o relatorio.pdf

Observações de segurança

Em produção, NÃO use FTP sem TLS. Prefira SFTP (SSH) ou FTPS.

Para capturar tráfego em switches gerenciados, configure SPAN/mirror port ou capture no host participante.

Em Wi‑Fi, a captura pode exigir modo monitor ou técnicas específicas dependendo do modo de autenticação da rede.

Resultados esperados

Confirmação de que USER e PASS aparecem em texto claro no tráfego capturado (quando FTP não está usando TLS).

Geração de evidências visuais (prints) exibindo os pacotes relevantes e a sequência do fluxo TCP.
