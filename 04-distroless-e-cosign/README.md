kube-news: Imagem Docker Assinada com Cosign
Este repositório apresenta a imagem Docker venanccio/kube-news:v3, publicada e assinada digitalmente para garantir sua autenticidade e integridade. Abaixo estão os comandos completos para instalação do Cosign, geração de chaves, construção, assinatura e verificação da imagem.

Repositório da Imagem no Docker Hub:
https://hub.docker.com/repository/docker/venanccio/kube-news/general

1. Instalar o Cosign
bash:
curl -O -L "https://github.com/sigstore/cosign/releases/latest/download/cosign-linux-amd64"
sudo mv cosign-linux-amd64 /usr/local/bin/cosign
sudo chmod +x /usr/local/bin/cosign

2. Gerar o Par de Chaves Cosign
bash: cosign generate-key-pair
Serão criados os arquivos cosign.key (privada) e cosign.pub (pública).

3. Construir e Publicar a Imagem
bash: docker build --push -t venanccio/kube-news:v3 .
A imagem é construída localmente e enviada ao Docker Hub.

4. Assinar a Imagem
bash: cosign sign --key cosign.key venanccio/kube-news:v3
A assinatura digital é anexada à imagem no registro remoto.

5. Verificar a Assinatura
bash: cosign verify --key cosign.pub venanccio/kube-news:v3 > cosign-signature.txt
O comando valida a assinatura utilizando a chave pública. O resultado pode ser salvo em cosign-signature.txt.

Como Verificar a Assinatura da Imagem
Obtenha a chave pública (cosign.pub) utilizada na assinatura.

Execute o comando abaixo para validar a imagem:

bash: cosign verify --key cosign.pub venanccio/kube-news:v3
Se a assinatura for válida, o Cosign exibirá informações confirmando a integridade e autoria da imagem.

Mais informações:
Documentação oficial do Cosign - https://github.com/sigstore/cosign