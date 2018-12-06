# xva2proxmox
Procedimentos de migração de máquinas virtuais do Xen para Proxmox (5.2-1)

1) Copiar a imagem da máquina virtual (xva) para o servidor proxmox
estacao# scp arquivo.xva nome@ip_proxmox:/root
2) Descompactar o arquivo da máquina virtual. Será criado um diretório com nome parecido com Ref:999
proxmox#  tar -xvf arquivo.xva
3) Converter o diretório para o format raw
proxmox# python --convert=Ref\:999 maquina.img
4) Identificar o local do hd virtual da nova máquina com o comando lvdisplay (deve ser algo como /dev/pve/vm-999-disk-9)
proxmox# lvdisplay
5) Substituir o hd virtual
proxmox# dd if=/root/maquina.img of=/dev/pve/vm-999-disk-9
6) Inicializar a máquina virtual, no proxmox, com o novo hd virtual
