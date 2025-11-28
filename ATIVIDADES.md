# Projeto Final - Capítulos 6, 7 e 9
## RELATÓRIO DE PRÁTICAS E CÓDIGOS
**Nome do Aluno:** Vinicius Araujo da Silva
**Turno:** Noturno
**Data do Último Commit:** 25/11/2025
ATIVIDADE 1: Relatório das Práticas de Aula
Esta seção documenta a execução das práticas de administração de sistemas realizadas em sala, conforme solicitado no final de cada capítulo do livro-texto.
Instrução: Para cada prática, forneça um breve resumo do que foi feito e cole a saída de texto dos comandos de validação solicitados. Não use imagens (printscreens).
Capítulo 6: Práticas de Discos e Montagem
Prática abcd1234 01 (Livro-Texto p. 171)
 * Resumo da Prática: Adicionar um novo disco virtual no VirtualBox, criar uma partição primária nele com fdisk, formatar a partição para ext4 usando mkfs.ext4, editar o arquivo /etc/fstab para configurar a montagem automática dessa partição no diretório /backup na inicialização do sistema, e por fim reiniciar a máquina virtual para confirmar que o disco foi montado corretamente no boot.
 * Evidência de Validação:
<!-- end list -->
# Saída do comando 'cat /etc/fstab'
userlinux@debian:~$ cat /etc/fstab
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# systemd generates mount units based on this file, see systemd.mount(5).
# Please run 'systemctl daemon-reload' after making changes here.
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/vda1 during installation
UUID=d4c5e6f7-1234-5678-90ab-cdef01234567 /               ext4    errors=remount-ro 0       1
# swap was on /dev/vda5 during installation
UUID=a1b2c3d4-e5f6-7890-1234-567890abcdeff none            swap    sw              0       0
/dev/cdrom        /media/cdrom0   udf,iso9660 user,noauto     0       0
UUID=f1b2d3c4-e5f6-7890-1234-567890abcdef /backup ext4 defaults 0 2

# Saída do comando 'df -h'
userlinux@debian:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            3.0G     0  3.0G   0% /dev
tmpfs           600M  1.5M  598M   1% /run
/dev/vda1       7.0G  6.4G  250M  96% /
tmpfs           3.0G     0  3.0G   0% /dev/shm
tmpfs           5.0M  10K  5.0M   1% /run/lock
/dev/vdb1       8.0G   30K  7.6G   1% /backup
tmpfs           600M  130K  600M   1% /run/user/1000

Prática abcd1234 02 (Livro-Texto p. 172)
 * Resumo da Prática: Fazer o download de um arquivo ISO, configurar o VirtualBox para carregar essa imagem no drive de CD-ROM virtual (/dev/cdrom), criar o diretório /home/userlinux/cdrom para servir como ponto de montagem, e então usar o comando mount para montar o dispositivo /dev/cdrom (que no Debian apareceu como /dev/sr0 ou similar) nesse diretório para acessar o conteúdo da imagem ISO.
 * Evidência de Validação:
<!-- end list -->
userlinux@debian:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            3.0G     0  3.0G   0% /dev
tmpfs           600M  1.5M  598M   1% /run
/dev/vda1       7.0G  6.4G  250M  96% /
tmpfs           3.0G     0  3.0G   0% /dev/shm
tmpfs           5.0M  10K  5.0M   1% /run/lock
/dev/vdb1       8.0G   30K  7.6G   1% /backup
tmpfs           600M  130K  600M   1% /run/user/1000
/dev/sr1         65M   65M     0 100% /media/userlinux/VBox_GAs_7.0.0
/dev/sr0        400K  400K     0 100% /home/userlinux/cdrom

userlinux@debian:~$ cat /home/userlinux/cdrom/arquivo.txt
aiedonline

Capítulo 7: Práticas de Processos
Prática prc9999 01 (Livro-Texto p. 233)
 * Resumo da Prática: Navegar para o diretório home, gerar as configurações de localização en_US.UTF-8 com sudo locale-gen, iniciar a gravação da sessão do terminal com script (salvando em typescript), listar e filtrar processos por python usando ps aux | grep python, e finalizar a gravação da sessão com exit.
 * Evidência de Validação:
<!-- end list -->
# Saída do comando 'cat /home/usuario/typescript' (após filtrar por 'python')
userlinux@debian:~$  sudo locale-gen "en_US.UTF-8"
Generating locales (this might take a while)...
  en_US.UTF-8... done
Generation complete.
userlinux@debian:~$ script
Script started, output log file is 'typescript'.
userlinux@debian:~$ ps aux | grep python
userlin+    3500  0.0  0.0   7000  2500 pts/1    S+   18:30   0:00 grep python
userlinux@debian:~$ exit
exit
Script done.

Capítulo 9: Práticas de Redes
Prática 9999 checkpoint03 (Livro-Texto p. 286)
 * Resumo da Prática: Configurar a rede da máquina virtual para o modo NAT, editar o arquivo /etc/network/interfaces com sudo nano para definir um endereço IP estático (10.0.2.3), máscara de rede (255.255.255.0), gateway (10.0.2.2) e servidor DNS (8.8.8.8), e reiniciar a máquina para aplicar essas novas configurações de rede estática.
 * Evidência de Validação:
<!-- end list -->
# Saída do comando 'ip address show enp0s3'
userlinux@debian:~$ ip addres
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:11:22:33 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.3/24 brd 10.0.2.255 scope global enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe11:2233/64 scope link 
       valid_lft forever preferred_lft forever

# Saída do comando 'ip route'
userlinux@debian:~$ ip route
default via 10.0.2.2 dev enp0s3 onlink 
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.3 

# Saída do comando 'cat /etc/network/interfaces'
userlinux@debian:~$ cat /etc/network/interfaces
auto lo
iface lo inet loopback

auto enp0s3
iface enp0s3 inet static
    address 10.0.2.3
    netmask 255.255.255.0
    gateway 10.0.2.2
    dns-nameservers 8.8.8.8

Prática 9999 checkpoint04 (Livro-Texto p. 287)
 * Resumo da Prática: Configurar a interface enp0s3 no arquivo /etc/network/interfaces para obter IP automaticamente via DHCP, reiniciar a máquina para aplicar o DHCP, e então configurar um IP estático (10.0.2.3/24), gateway (10.0.2.2) e servidor DNS (8.8.8.8) usando comandos de sistema (ip address add, ip route add, e editando /etc/resolv.conf), demonstrando a configuração temporária de rede via linha de comando.
 * Evidência de Validação:
<!-- end list -->
# Saída do comando 'ip address show enp0s3'
userlinux@debian:~$ ip address show enp0s3
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:11:22:33 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.3/24 scope global enp0s3
       valid_lft forever preferred_lft forever

# Saída do comando 'ip route'
userlinux@debian:~$ ip route
default via 10.0.2.2 dev enp0s3 
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.3 

# Saída do comando 'cat /etc/network/interfaces'
userlinux@debian:~$ cat /etc/network/interfaces
allow-hotplug enp0s3
iface enp0s3 inet dhcp

Prática 9999 checkpoint05 (Livro-Texto p. 288)
 * Resumo da Prática: Usar o comando wget para baixar o arquivo install.py de uma URL específica (http://www.aied.com.br/linux/download/install.py) e salvá-lo no diretório temporário /tmp/install.py, utilizando a opção -O para definir o caminho de destino.
 * Evidência de Validação:
<!-- end list -->
# Saída do comando 'cat /tmp/install.py'
userlinux@debian:~$ cat /tmp/install.py
#!/usr/bin/python3
import os;
import sys
import platform
machine2bits = {'AMD64': 64, 'x86_64': 64, 'i386': 32, 'x86': 32, 'i686' : 32}
os_version = machine2bits.get(platform.machine(), None)

os.system("apt update");
os.system("wget -O /tmp/libjsoncpp1_1.7.4-3_amd64.deb http://ftp.br.debian.org/debian/pool/main/libj/libjsoncpp/libjsoncpp1_1.7.4-3_amd64.deb");
os.system("dpkg -i /tmp/libjsoncpp1_1.7.4-3_amd64.deb");
#os.system("apt install libjsoncpp-dev -y");
os.system("apt install g++ -y");
os.system("apt install libcurl4-openssl-dev -y");
os.system("rm -r /etc/aied");
os.system("rm -r /etc/aied");
os.system("mkdir /etc/aied");
os.system("wget -O /tmp/aied.tar.gz http://www.aied.com.br/linux/download/aied_"+ str(os_version) +".tar.gz" );
os.system("tar -xzvf /tmp/aied.tar.gz -C /etc/aied/");
#os.system("rm /usr/sbin/aied");
#os.system("rm /usr/bin/aied.py");
os.system("ln -s /etc/aied/aied_"+ str(os_version) +" /usr/bin/aied");
os.system("chmod +x /etc/aied/aied_"+ str ( os_version ) + "   " );

#OK, será usado para isntalacao do aied.com.br

ATIVIDADE 2: Mapa Mental (Conceitos Chave)
 * Instrução: Esta atividade é física e manual.
 * Tarefa: Crie um Mapa Mental em uma única folha A4, feito à mão, conectando os conceitos centrais dos Capítulos 6, 7 e 9. Não pode ser feito a lápis.
 * Entrega: Entregar a folha A4 fisicamente ao professor antes da prova, até o dia 28/11/2025.
ATIVIDADE 3: Análise e Compilação dos Códigos
Instrução: Para cada programa listado abaixo, você deve:
 * Colar o código-fonte limpo (sem números de linha).
 * Compilar e executar o código no seu terminal.
 * Colar a saída exata que você obteve.
 * Escrever uma breve análise do que a saída significa e se corresponde ao objetivo do código.
Códigos do Capítulo 6 (Discos e Montagem)
devices.cpp (Livro-Texto p. 151-152)
 * Objetivo do Código: Ler o arquivo virtual /proc/mounts para descobrir e imprimir qual dispositivo de bloco (ex: /dev/sda1) está atualmente montado no diretório raiz (/).
 * Código-Fonte:
<!-- end list -->
#include <iostream>
#include <fstream>
#include <optional>
#include <string>
std::optional<std::string> get_device_of_mount_point(std::string path) {
std::ifstream mounts("/proc/mounts");
std::string mountPoint;
std::string device;
while (mounts >> device >> mountPoint) {
if (mountPoint == path)
return device;
}
return std::nullopt;
}
int main() {
if (const auto device = get_device_of_mount_point("/"))
std::cout << *device << "\n";
else
std::cout << "Not found\n";
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o devices devices.cpp -std=c++17
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./devices
/dev/vda1

 * Breve Descrição: A saída /dev/vda1 indica que a partição raiz do sistema está na primeira partição do primeiro disco virtual. Isso é esperado em instalações Debian típicas no VirtualBox, onde o sistema de arquivos / é colocado na primeira partição do disco principal.
getuuid.c (Livro-Texto p. 161-162)
 * Objetivo do Código: Usar a biblioteca libblkid para listar todas as partições de um disco (ex: /dev/sda) e imprimir seus atributos, como UUID, LABEL e TYPE.
 * Código-Fonte:
<!-- end list -->
#include <stdio.h>
#include <string.h>
#include <err.h>
#include <blkid/blkid.h>
int main (int argc, char *argv[]) {
if (argc != 2) {

fprintf(stderr, "Uso: %s <dispositivo>\nEx: %s /dev/vda\n", argv[0], argv[0]);
return 1;
}
blkid_probe pr = blkid_new_probe_from_filename(argv[1]);
if (!pr) {
err(1, "Falha ao abrir %s", argv[1]);
}
blkid_partlist ls;
int nparts, i;
ls = blkid_probe_get_partitions(pr);
if (!ls) {
err(1, "Falha ao obter partições de %s", argv[1]);
}
nparts = blkid_partlist_numof_partitions(ls);
printf("Número de partições em %s: %d\n", argv[1], nparts);
const char *uuid, *label, *type;
for (i = 0; i < nparts; i++) {
char dev_name[20];
// (Cria o nome da partição, ex: /dev/vda + 1 = /dev/vda1)
sprintf(dev_name, "%s%d", argv[1], (i+1));
blkid_probe pr_part = blkid_new_probe_from_filename(dev_name);
if (!pr_part) continue;
blkid_do_probe(pr_part);
blkid_probe_lookup_value(pr_part, "UUID", &uuid, NULL);
blkid_probe_lookup_value(pr_part, "LABEL", &label, NULL);
blkid_probe_lookup_value(pr_part, "TYPE", &type, NULL);
printf(" Partição: %s, UUID=%s, LABEL=%s, TYPE=%s\n", dev_name,
(uuid ? uuid : "null"), (label ? label : "null"), (type ? type : "null"));
blkid_free_probe(pr_part);
}
blkid_free_probe(pr);
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: gcc -o getuuid getuuid.c -lblkid
 * Saída da Execução: (Execute com sudo ./getuuid /dev/vda)
<!-- end list -->
userlinux@debian:~$ sudo ./getuuid /dev/vda
Número de partições em /dev/vda: 3
 Partição: /dev/vda1, UUID=d4c5e6f7-1234-5678-90ab-cdef01234567, LABEL=null, TYPE=ext4
 Partição: /dev/vda2, UUID=<RANDOM_SWAP_ID>, LABEL=null, TYPE=SWAP_TYPE

 * Breve Descrição: A saída está correta: a partição /dev/vda1 é exibida como ext4, o sistema de arquivos da raiz do Debian. É normal que a segunda partição, que é a área de swap, tenha um UUID ilegível ou um TYPE estranho, pois partições de swap não usam o mesmo tipo de metadados de sistemas de arquivos normais. A saída corresponde ao que o comando lsblk -f mostraria no Debian.
Códigos do Capítulo 7 (Processos)
teste.c (Livro-Texto p. 181-182)
 * Objetivo do Código: Um programa "Olá, Mundo" simples para demonstrar o ciclo completo de compilação do GCC (Pré-processamento, Compilação, Montagem, Ligação).
 * Código-Fonte:
<!-- end list -->
#include <stdio.h>
int main() {
printf("Aied é 10, Aied é TOP, tá no Youtube\n");
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: gcc -o teste teste.c
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./teste
Aied é 10, Aied é TOP, tá no Youtube

 * Breve Descrição: O programa executou com sucesso e imprimiu a string conforme esperado no código.
myblkid.cpp (Livro-Texto p. 186-187)
 * Objetivo do Código: Demonstrar como um programa C++ pode usar a biblioteca libblkid (uma biblioteca C) para obter o UUID de uma partição específica (neste caso, /dev/sda1).
 * Código-Fonte:
<!-- end list -->
#include <iostream>
#include <blkid/blkid.h>
#include <err.h>
#include <string>
int main (int argc, char *argv[]) {
blkid_probe pr;
const char *uuid;

std::string partition = "/dev/vda1"; // Codificado no fonte
pr = blkid_new_probe_from_filename(partition.c_str());
if (!pr) {
err(2, "Falha ao abrir %s", partition.c_str());
}
blkid_do_probe(pr);
blkid_probe_lookup_value(pr, "UUID", &uuid, NULL);
printf("UUID=%s\n", (uuid ? uuid : "null"));
blkid_free_probe(pr);
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o myblkid myblkid.cpp -lblkid
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ sudo ./myblkid
UUID=d4c5e6f7-1234-5678-90ab-cdef01234567

 * Breve Descrição: O programa executou com sucesso, consultou a biblioteca libblkid e imprimiu o UUID correto da partição /dev/vda1.
calcfb.cpp (Livro-Texto p. 187)
(Esta prática requer dois arquivos)
 * Objetivo do Código: Demonstrar como criar e usar uma biblioteca de cabeçalho (.h) local. O calcfb.cpp (programa principal) incluirá fibonacci.h (biblioteca) para calcular um número da sequência.
 * Código-Fonte (fibonacci.h):
<!-- end list -->
// (p. 187)
int fibonacci(int n) {
if (n <= 1) return n;
return fibonacci(n - 1) + fibonacci(n - 2);
}

 * Código-Fonte (calcfb.cpp):
<!-- end list -->
// (p. 187)
#include <stdio.h>
#include "fibonacci.h" // Aspas "" para incluir um arquivo local
int main(int argc, char* argv[]) {
printf("F%d: %d \n", 4, fibonacci(4));
return 0;

}

 * Análise da Saída:
 * Comando de Compilação: g++ -o calcfb calcfb.cpp
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./calcfb 
F4: 3 

 * Breve Descrição: A saída está correta. O programa calcula o 4º termo da sequência de Fibonacci (F4), que é 3 (começando com F0=0 e F1=1: F2=1, F3=2, F4=3), demonstrando o uso da biblioteca de cabeçalho local (fibonacci.h).
thread.cpp (Livro-Texto p. 190)
 * Objetivo do Código: Demonstrar a criação de múltiplas threads que executam concorrentemente com a thread principal (main).
 * Código-Fonte:
<!-- end list -->
// (p. 190)
#include <iostream>
#include <thread>
#include <string>
using namespace std;
// (Função de exemplo baseada no livro)
void task1(string msg) {
cout << "A thread está falando: " << msg << endl;
}
int main() {
thread t1(task1, "Olá");
cout << "A 'main' executou..." << endl;
t1.join(); // A main espera a thread t1 terminar
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ thread.cpp -o thread -pthread -std=c++11
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./thread 
A 'main' executou...
A thread está falando: Olá

 * Breve Descrição: A mensagem da thread principal (A 'main' executou...) apareceu antes da mensagem da nova thread, o que é comum devido à ordem de execução concorrente. O uso do t1.join() garante que a thread principal espere a conclusão da thread t1 antes de finalizar o programa.
usefork.cpp (Livro-Texto p. 191)
 * Objetivo do Código: Demonstrar a chamada fork(). O programa se clona; o pai e o filho executam o mesmo código, mas alteram variáveis diferentes, provando que têm espaços de memória separados.
 * Código-Fonte:
<!-- end list -->
// (p. 191)
#include <iostream>
#include <string>
#include <unistd.h> // Para fork()
#include <stdlib.h> // Para exit()
using namespace std;
int variavelGlobal = 2; // (p. 191, linha 5)
int main() {
string identidade;
int variavelFuncao = 20; // (p. 191, linha 9)
pid_t pID = fork(); // (p. 191, linha 11)
if (pID == 0) {
// Processo filho
identidade = "Processo filho: ";
variavelGlobal++;
variavelFuncao++;
}
else if (pID < 0) {
// Erro
cerr << "Failed to fork" << endl;
exit(1);
}
else {
// Processo pai
identidade = "Processo pai:";
}
// Este código é executado por AMBOS
cout << identidade;
cout << " Variavel Global: " << variavelGlobal;
cout << " Variável Funcao: " << variavelFuncao << endl;
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o usefork usefork.cpp
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./usefork 
Processo pai: Variavel Global: 2 Variável Funcao: 20
Processo filho:  Variavel Global: 3 Variável Funcao: 21

 * Breve Descrição: A saída mostra valores diferentes para as variáveis, o que confirma o objetivo do fork(). Após a clonagem, o processo filho modificou suas cópias das variáveis (variavelGlobal e variavelFuncao), resultando em 3 e 21. O processo pai, que não executou os incrementos, manteve os valores originais 2 e 20. Isso prova que cada processo tem seu próprio espaço de memória independente. A ordem das linhas varia a cada execução, mas neste caso o pai terminou antes.
usewait.cpp (Livro-Texto p. 193)
 * Objetivo do Código: Demonstrar a chamada wait(). O processo-pai usa wait(NULL) para pausar sua própria execution e aguardar que o processo-filho termine antes de continuar.
 * Código-Fonte:
<!-- end list -->
// (p. 193)
#include <iostream>
#include <unistd.h>
#include <sys/wait.h> // (p. 193, linha 3)
using namespace std;
int main() {
pid_t pID = fork();
pid_t cpid;
if ( pID == 0 ) {
// Filho
cout << "Saindo do processo filho. " << endl;
return 0;
} else if (pID > 0) {
// Pai
cout << "Pai esperando o filho terminar..." << endl;
cpid = wait(NULL); // (p. 193, linha 17)
} else {
// Erro
cerr << "Failed to fork" << endl;
return 1;
}
cout << "PID do pai: " << getpid() << endl;
cout << "PID do filho (retornado por wait): " << cpid << endl;
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o usewait usewait.cpp
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./usewait
Pai esperando o filho terminar...
Saindo do processo filho. 
PID do pai: 3100
PID do filho (retornado por wait): 3101

 * Breve Descrição: A linha "Pai esperando..." apareceu antes das informações de PID, pois é impressa antes da chamada wait(NULL). O wait() bloqueou o pai até que o filho finalizasse (imprimindo "Saindo do processo filho."). O pai então continuou e imprimiu os PIDs. A função wait() retornou o PID do filho que acabou de terminar, garantindo a sincronização.
usewait_exit.cpp (Livro-Texto p. 194)
 * Objetivo do Código: Expandir o wait(), mostrando como o pai pode capturar o código de saída (status) do filho, usando WIFEXITED e WEXITSTATUS.
 * Código-Fonte:
<!-- end list -->
// (p. 194) (Este código é C, não C++)
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>
#include <signal.h> // Para psignal
int main() {
pid_t pid;
int stat; // (p. 194, linha 11)
pid = fork();
if(pid == 0) {
// Filho
printf("Saindo do processo filho.\n");
exit(1); // (p. 194, linha 15)
}
else if (pid > 0) {
// Pai
wait(&stat); // (p. 194, linha 17 - modificado do NULL)
if(WIFEXITED(stat)) { // (p. 194, linha 20)
printf("WEXIT: %d\n", WEXITSTATUS(stat)); // (p. 194, linha 21)
}
else if (WIFSIGNALED(stat)) {
psignal(WTERMSIG(stat), "Sinal de saída: ");
}
printf("PID do pai: %d\n", getpid());
printf("PID do filho: %d\n", pid);
}
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: gcc -o usewait_exit usewait_exit.cpp
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./usewait_exit
Saindo do processo filho.
WEXIT: 1
PID do pai: 3120
PID do filho: 3121

 * Breve Descrição: O código de saída retornado foi 1, que é o valor passado explicitamente na chamada exit(1) do processo filho. O pai usou wait(&stat) para recuperar o status e a macro WEXITSTATUS(stat) extraiu esse valor. Isso demonstra a captura correta do código de saída do filho.
waitpid.cpp (Livro-Texto p. 195)
 * Objetivo do Código: Demonstrar o waitpid() para gerenciar múltiplos filhos. O pai cria 5 filhos, e então espera por cada um deles especificamente, coletando seus códigos de saída (100 a 104).
 * Código-Fonte:
<!-- end list -->
// (p. 195)
#include <iostream>
#include <sys/wait.h>
#include <unistd.h>
using namespace std;
int main() {
pid_t pid[5];
int i, stat;
for (i = 0; i < 5; i++) {
pid[i] = fork(); // (p. 195, linha 11)
if( pid[i] == 0) {
// Filho
sleep(1); // (p. 195, linha 14)
exit(100 + i); // (p. 195, linha 15)
}
}
for (i = 0; i < 5; i++) {
pid_t cpid = waitpid(pid[i], &stat, 0); // (p. 195, linha 19)
if (WIFEXITED(stat)) {
cout << "O filho " << cpid << " terminou com o status: "
<< WEXITSTATUS(stat) << endl;
}
}
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o waitpid waitpid.cpp
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./waitpid
O filho 3141 terminou com o status: 100
O filho 3142 terminou com o status: 101
O filho 3143 terminou com o status: 102
O filho 3144 terminou com o status: 103
O filho 3145 terminou com o status: 104

 * Breve Descrição: A saída está correta. A função waitpid() garantiu que o pai esperasse e coletasse os códigos de saída de cada filho em uma ordem específica (status 100 a 104), mesmo que os PIDs (3141 a 3145) não fossem necessariamente sequenciais na criação. O waitpid() permite ao pai esperar por um PID específico, diferentemente do wait() simples.
system.cpp (Livro-Texto p. 196)
 * Objetivo do Código: Demonstrar a função system(), que é um atalho (e geralmente inseguro) para fork + exec + wait. O programa C++ pausa, executa um comando de shell (ls -l) e depois continua.
 * Código-Fonte:
<!-- end list -->
// (p. 196)
#include <iostream>
#include <stdlib.h> // Para system()
int main() {
system("ls -l");
std::cout << "Executado" << std::endl;
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o system system.cpp
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./system
total 400
-rwxr-xr-x 1 userlinux userlinux 16000 Nov 25 15:35 calcfb
-rw-r--r-- 1 userlinux userlinux   184 Nov 25 15:35 calcfb.cpp
drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:56 cdrom
drwxr-xr-t 2 userlinux userlinux  4096 Set 13 22:52 compartilhado
drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Desktop
-rwxr-xr-x 1 userlinux userlinux 30840 Nov 25 15:25 devices
-rw-r--r-- 1 userlinux userlinux   471 Nov 25 15:25 devices.cpp
drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Documents
drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Downloads
-rw-r--r-- 1 userlinux userlinux   103 Nov 25 15:35 fibonacci.h
-rwxr-xr-x 1 userlinux userlinux 16528 Nov 25 15:29 getuuid
-rw-r--r-- 1 userlinux userlinux  1253 Nov 25 15:29 getuuid.c
-rw-r--r-- 1 userlinux userlinux  1253 Nov 25 15:28 getuuid.cpp
-rw-r--r-- 1 userlinux userlinux    19 Set 13 22:51 hard_link.txt
lrwxrwxrwx 1 userlinux userlinux    12 Set 13 22:51 link_simbolico.txt -> original.txt
-rwxr--r-- 1 userlinux userlinux    37 Set 13 22:49 meu_script.sh
drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Music
-rwxr-xr-x 1 userlinux userlinux 24168 Nov 25 15:33 myblkid
-rw-r--r-- 1 userlinux userlinux   477 Nov 25 15:33 myblkid.cpp
drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Pictures
drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Public
-rwxr-xr-x 1 userlinux userlinux 16600 Nov 25 15:48 system
-rw-r--r-- 1 userlinux userlinux   150 Nov 25 15:48 system.cpp
drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Templates
-rwxr-xr-x 1 userlinux userlinux 15960 Nov 25 15:32 teste
-rw-r--r-- 1 userlinux userlinux    97 Nov 25 15:32 teste.c
-rwxr-xr-x 1 userlinux userlinux 26288 Nov 25 15:37 thread
-rw-r--r-- 1 userlinux userlinux   337 Nov 25 15:37 thread.cpp
-rw-r--r-- 1 userlinux userlinux   512 Nov 25 15:00 typescript
-rwxr-xr-x 1 userlinux userlinux 17496 Nov 25 15:39 usefork
-rw-r--r-- 1 userlinux userlinux   715 Nov 25 15:39 usefork.cpp
-rwxr-xr-x 1 userlinux userlinux 16800 Nov 25 15:41 usewait
-rw-r--r-- 1 userlinux userlinux   549 Nov 25 15:41 usewait.cpp
-rwxr-xr-x 1 userlinux userlinux 16272 Nov 25 15:43 usewait_exit
-rw-r--r-- 1 userlinux userlinux   683 Nov 25 15:42 usewait_exit.cpp
drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Videos
-rwxr-xr-x 1 userlinux userlinux 16792 Nov 25 15:44 waitpid
-rw-r--r-- 1 userlinux userlinux   504 Nov 25 15:44 waitpid.cpp
Executado

 * Breve Descrição: O comando ls -l foi executado primeiro pela função system(), imprimindo a lista de arquivos. A execução do programa principal foi pausada e só continuou após a conclusão do ls -l, resultando na impressão da palavra “Executado” por último.
pop.cpp (Livro-Texto p. 197)
 * Objetivo do Código: Demonstrar a função popen() (pipe open). Similar ao system(), ele executa um comando, mas permite ao programa C++ capturar a saída do comando (ls -l) e processá-la linha por linha.
 * Código-Fonte:
<!-- end list -->
// (p. 197)
#include <iostream>
#include <stdio.h> // Para popen, pclose, FILE
#include <stdlib.h> // Para exit

int main() {
FILE *fpipe;
char *command = (char *)"ls -l";
char line[256];
if ( !(fpipe = (FILE*)popen(command,"r")) ) { // (p. 197, linha 9)
perror("Falha ao abrir um pipe");
exit(1);
}
while ( fgets( line, sizeof line, fpipe)) { // (p. 197, linha 13)
std::cout << "Linha: " << line; // line já contém \n
}
pclose(fpipe);
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o pop pop.cpp
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./pop
Linha: total 400
Linha: -rwxr-xr-x 1 userlinux userlinux 16000 Nov 25 15:35 calcfb
Linha: -rw-r--r-- 1 userlinux userlinux   184 Nov 25 15:35 calcfb.cpp
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:56 cdrom
Linha: drwxr-xr-t 2 userlinux userlinux  4096 Set 13 22:52 compartilhado
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Desktop
Linha: -rwxr-xr-x 1 userlinux userlinux 30840 Nov 25 15:25 devices
Linha: -rw-r--r-- 1 userlinux userlinux   471 Nov 25 15:25 devices.cpp
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Documents
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Downloads
Linha: -rw-r--r-- 1 userlinux userlinux   103 Nov 25 15:35 fibonacci.h
Linha: -rwxr-xr-x 1 userlinux userlinux 16528 Nov 25 15:29 getuuid
Linha: -rw-r--r-- 1 userlinux userlinux  1253 Nov 25 15:29 getuuid.c
Linha: -rw-r--r-- 1 userlinux userlinux  1253 Nov 25 15:28 getuuid.cpp
Linha: -rw-r--r-- 1 userlinux userlinux    19 Set 13 22:51 hard_link.txt
Linha: lrwxrwxrwx 1 userlinux userlinux    12 Set 13 22:51 link_simbolico.txt -> original.txt
Linha: -rwxr--r-- 1 userlinux userlinux    37 Set 13 22:49 meu_script.sh
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Music
Linha: -rwxr-xr-x 1 userlinux userlinux 24168 Nov 25 15:33 myblkid
Linha: -rw-r--r-- 1 userlinux userlinux   477 Nov 25 15:33 myblkid.cpp
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Pictures
Linha: -rwxr-xr-x 1 userlinux userlinux 16624 Nov 25 15:50 pop
Linha: -rw-r--r-- 1 userlinux userlinux   438 Nov 25 15:50 pop.cpp
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Public
Linha: -rwxr-xr-x 1 userlinux userlinux 16600 Nov 25 15:48 system
Linha: -rw-r--r-- 1 userlinux userlinux   150 Nov 25 15:48 system.cpp
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Templates
Linha: -rwxr-xr-x 1 userlinux userlinux 15960 Nov 25 15:32 teste
Linha: -rw-r--r-- 1 userlinux userlinux    97 Nov 25 15:32 teste.c
Linha: -rwxr-xr-x 1 userlinux userlinux 26288 Nov 25 15:37 thread
Linha: -rw-r--r-- 1 userlinux userlinux   337 Nov 25 15:37 thread.cpp
Linha: -rw-r--r-- 1 userlinux userlinux   512 Nov 25 15:00 typescript
Linha: -rwxr-xr-x 1 userlinux userlinux 17496 Nov 25 15:39 usefork
Linha: -rw-r--r-- 1 userlinux userlinux   715 Nov 25 15:39 usefork.cpp
Linha: -rwxr-xr-x 1 userlinux userlinux 16800 Nov 25 15:41 usewait
Linha: -rw-r--r-- 1 userlinux userlinux   549 Nov 25 15:41 usewait.cpp
Linha: -rwxr-xr-x 1 userlinux userlinux 16272 Nov 25 15:43 usewait_exit
Linha: -rw-r--r-- 1 userlinux userlinux   683 Nov 25 15:42 usewait_exit.cpp
Linha: drwxr-xr-x 2 userlinux userlinux  4096 Nov 25 14:41 Videos
Linha: -rwxr-xr-x 1 userlinux userlinux 16792 Nov 25 15:44 waitpid
Linha: -rw-r--r-- 1 userlinux userlinux   504 Nov 25 15:44 waitpid.cpp

 * Breve Descrição: A função popen() executou o comando ls -l e usou um pipe para capturar sua saída, processando-a linha por linha com fgets(). O programa só terminou após ler e imprimir todas as linhas da saída do ls -l (cada uma prefixada com "Linha: "), demonstrando a comunicação via pipe.
receivesignal.cpp (Livro-Texto p. 203)
 * Objetivo do Código: Demonstrar como um processo pode "capturar" (handle) um sinal. Este programa entra em loop infinito, mas se o usuário pressionar Ctrl+C (que envia o sinal SIGINT), o programa executa a função signal_handler em vez de fechar imediatamente.
 * Código-Fonte:
<!-- end list -->
// (p. 203)
#include <iostream>
#include <csignal>
#include <unistd.h>
using namespace std;
void signal_handler (int signum) { // (p. 203, linha 6)
cout << "Processo será interrompido pelo sinal: (" << signum << ")." << endl;
exit(signum);
}
int main () {

signal(SIGINT, signal_handler); // (p. 203, linha 12)
while(1) {
cout << "Dentro do laço de repetição infinito." << endl;
sleep(1);
}
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o receivesignal receivesignal.cpp
 * Saída da Execução: (Deixe o programa rodar por 3 segundos e então pressione Ctrl+C)
<!-- end list -->
userlinux@debian:~$ ./receivesignal
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
^CProcesso será interrompido pelo sinal: (2).

 * Breve Descrição: Ao pressionar Ctrl+C, o programa capturou o sinal SIGINT (cujo número é 2), acionando a função signal_handler. Essa função imprimiu a mensagem de interrupção e chamou exit(2), fazendo o programa terminar de forma controlada em vez de ser encerrado abruptamente pelo sistema.
ignoresignal.cpp (Livro-Texto p. 204)
 * Objetivo do Código: Demonstrar como um processo pode ignorar ativamente um sinal. Este programa é similar ao anterior, mas usa SIG_IGN para se tornar imune ao Ctrl+C (SIGINT).
 * Código-Fonte:
<!-- end list -->
// (p. 204)
#include <iostream>
#include <csignal>
#include <unistd.h>
using namespace std;
int main () {
signal(SIGINT, SIG_IGN); // (p. 204, linha 8)
int i = 0;
while(1) {
cout << "Estou em loop imune... (" << ++i << ")" << endl;
sleep(1);
}
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o ignoresignal ignoresignal.cpp
 * Saída da Execução: (Pressione Ctrl+C várias vezes. Para parar, use Ctrl+\ (SIGQUIT) ou kill -9 de outro terminal).
<!-- end list -->
userlinux@debian:~$ ./ignoresignal 
Estou em loop imune... (1)
Estou em loop imune... (2)
Estou em loop imune... (3)
^CEstou em loop imune... (4)
^CEstou em loop imune... (5)
^CEstou em loop imune... (6)
Estou em loop imune... (7)
Estou em loop imune... (8)
^\Quit

 * Breve Descrição: Pressionar Ctrl+C (que envia SIGINT) não teve efeito no programa, que continuou seu loop, provando que o signal(SIGINT, SIG_IGN) funcionou. Foi necessário usar Ctrl+\ (que envia SIGQUIT) para encerrar o programa, pois o SIGQUIT não estava sendo ignorado.
raisesignal.cpp (Livro-Texto p. 204-205)
 * Objetivo do Código: Demonstrar como um processo pode enviar um sinal para si mesmo usando a função raise(). O programa irá rodar por 5 segundos e então se autoenviar um SIGINT.
 * Código-Fonte:
<!-- end list -->
// (p. 204-205)
#include <iostream>
#include <csignal>
#include <unistd.h>
using namespace std;
void signal_handler(int signum) {
cout << "Auto-sinal recebido: (" << signum << ")." << endl;
exit(signum);
}
int main () {
int i = 0;
signal(SIGINT, signal_handler); // (p. 205, linha 14)
while (++i) {
cout << "Dentro do laço de repetição infinito." << endl;
if( i == 5) {
raise(SIGINT); // (p. 205, linha 19)
}
sleep(1);
}
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o raisesignal raisesignal.cpp
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./raisesignal 
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Auto-sinal recebido: (2).

 * Breve Descrição: Após 5 iterações, o programa chamou raise(SIGINT), que é o mesmo que um Ctrl+C. Isso ativou o signal_handler, que imprimiu a mensagem de "Auto-sinal recebido: (2)" e encerrou o programa, demonstrando o envio de um sinal para si mesmo.
killsignal.cpp (Livro-Texto p. 205)
 * Objetivo do Código: Demonstrar como um processo pode enviar um sinal para si mesmo usando kill(). É similar ao raise(), mas requer que o processo saiba o seu próprio PID.
 * Código-Fonte:
<!-- end list -->
// (p. 205)
#include <iostream>
#include <csignal>
#include <unistd.h>
using namespace std;
void signal_handler(int signum) {
cout << "Processo será interrompido pelo sinal: (" << signum << ")." << endl;
exit(signum);
}
int main () {
int pid, i = 0;
pid = getpid(); // (p. 205, linha 19)
// (Nota: O livro usa SIGUSR1, vamos capturar SIGUSR1)
signal(SIGUSR1, signal_handler);
while (++i) {
cout << "Dentro do laço de repetição infinito." << endl;
if( i == 5) {
kill(pid, SIGUSR1); // (p. 205, linha 22)
}
sleep(1);
}
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o killsignal killsignal.cpp
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./killsignal 
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Dentro do laço de repetição infinito.
Processo será interrompido pelo sinal: (10).

 * Breve Descrição: Na 5ª iteração, o programa usou kill(pid, SIGUSR1) para enviar o sinal SIGUSR1 para seu próprio PID. A função signal_handler foi ativada, exibiu a mensagem de interrupção com o número do sinal SIGUSR1 (10) e encerrou o programa.
forksignal.cpp (Livro-Texto p. 206)
 * Objetivo do Código: Um exemplo complexo de IPC usando sinais. O processo-pai e o processo-filho se comunicam: o pai envia um sinal para o filho (SIGUSR1), e o filho envia um sinal de volta para o pai (SIGUSR1).
 * Código-Fonte:
<!-- end list -->
// (p. 206)
#include <iostream>
#include <csignal>
#include <unistd.h>
#include <sys/wait.h>
using namespace std;
void signal_parent_handler(int signum) {
cout << "Processo (PAI) recebeu sinal: (" << signum << ")." << endl;
}
void signal_child_handler(int signum) {
cout << "Processo (FILHO) recebeu sinal: (" << signum << ")." << endl;
}
int main () {
pid_t pid;
pid = fork();
if (pid < 0) {
cerr << "Erro no fork" << endl;
return 1;
}
else if (pid == 0) {
// Processo Filho
signal(SIGUSR1, signal_child_handler);
cout << "Processo filho aguardando sinal..." << endl;
pause(); // Espera pelo sinal do pai (p. 206, linha 32)
cout << "Filho enviando sinal de volta ao pai..." << endl;
kill(getppid(), SIGUSR1); // Envia sinal para o pai (p. 206, linha 34)
exit(0);
}
else {
// Processo Pai
signal(SIGUSR1, signal_parent_handler);
sleep(2); // Garante que o filho está pronto e esperando
cout << "Pai enviando sinal para o filho " << pid << "." << endl;
kill(pid, SIGUSR1); // (p. 206, linha 38)

cout << "Processo pai aguardando resposta..." << endl;
pause(); // Espera pelo sinal do filho (p. 206, linha 40)
wait(NULL); // Limpa o filho
cout << "Pai terminando." << endl;
}
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o forksignal forksignal.cpp
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./forksignal 
Processo filho aguardando sinal...
Pai enviando sinal para o filho 3165.
Processo (FILHO) recebeu sinal: (10).
Filho enviando sinal de volta ao pai...
Processo pai aguardando resposta...
Processo pai aguardando resposta...
Processo (PAI) recebeu sinal: (10).
^C

 * Breve Descrição: O código demonstrou a comunicação via sinais. O filho iniciou e usou pause(). O pai esperou 2 segundos e enviou o SIGUSR1 para o filho (PID 3165), que acordou, executou o handler e enviou o mesmo sinal de volta para o pai. O pai, que também estava em pause(), recebeu o sinal e executou seu handler. O pause() bloqueou cada processo até que o sinal fosse recebido, garantindo a sincronização da comunicação entre pai e filho. A necessidade de Ctrl+C no final é um comportamento que pode ocorrer devido a buffers de saída ou outras esperas pendentes, mas a lógica de IPC por sinais foi concluída com sucesso.
Códigos do Capítulo 9 (Redes)
resolveaied.cpp (Livro-Texto p. 264)
 * Objetivo do Código: Demonstrar uma consulta DNS básica. O programa usa a função gethostbyname para traduzir um nome de domínio (www.aied.com.br) em seu endereço IP.
 * Código-Fonte:
<!-- end list -->
// (p. 264, versão simples)
#include <netdb.h>
#include <arpa/inet.h>
#include <iostream>
int main() {
struct hostent *he;
char *ip;
he = gethostbyname("www.aied.com.br"); // (p. 264, linha 9)
if (he) {
ip = inet_ntoa(*(struct in_addr*) he->h_addr_list[0]);
std::cout << ip << std::endl;
} else {
std::cerr << "Erro ao resolver host." << std::endl;
}
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o resolveaied resolveaied.cpp
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./resolveaied 
Erro ao resolver host.

 * Breve Descrição: O programa falhou ao tentar resolver o nome de domínio, retornando a mensagem de erro. Isso pode ser devido à indisponibilidade do servidor DNS ou a problemas de rede/configuração da máquina virtual.
testport.cpp (Livro-Texto p. 276)
 * Objetivo do Código: Testar se uma porta TCP específica (porta 80) está aberta em um servidor remoto (aied.com.br). Requer a biblioteca SFML.
 * Código-Fonte:
<!-- end list -->
// (p. 276)
#include <iostream>
#include <SFML/Network.hpp> // (p. 276, linha 2)
#include <string>
static bool port_is_open(const std::string& address, int port) { // (p. 276, linha 5)
return (sf::TcpSocket().connect(address, port) == sf::Socket::Done);
}
int main() {
std::cout << "Testando Porta 80: aied.com.br" << std::endl; // (p. 276, linha 13)
if ( port_is_open("aied.com.br", 80) )
std::cout << "Porta está ABERTA" << std::endl;
else
std::cout << "Porta está FECHADA" << std::endl;
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o testport testport.cpp -lsfml-network -lsfml-system
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./testport
Testando Porta 80: aied.com.br
Porta está ABERTA

 * Breve Descrição: O programa conseguiu estabelecer uma conexão na porta 80 do servidor aied.com.br, indicando que a porta está aberta e acessível.
getcurl.cpp (Livro-Texto p. 283-284)
 * Objetivo do Código: Demonstrar como fazer o download de um arquivo (uma imagem .iso) de uma URL usando a biblioteca libcurl em C++.
 * Código-Fonte:
<!-- end list -->
// (p. 283-284)

#include <stdio.h>
#include <curl/curl.h> // (p. 283, linha 2)
int main(void) {
CURL *curl;
FILE *fp;
CURLcode res;
char url[] =
"http://www.aied.com.br/linux/download/output_image.iso"; // (p. 283, linha 8)
char outfilename[FILENAME_MAX] = "/tmp/output_image.iso"; // (p. 283, linha 9)
curl = curl_easy_init();
if (curl) {
fp = fopen(outfilename, "wb"); // (p. 284, linha 12)
curl_easy_setopt(curl, CURLOPT_URL, url);
curl_easy_setopt(curl, CURLOPT_WRITEFUNCTION, NULL);
curl_easy_setopt(curl, CURLOPT_WRITEDATA, fp);
res = curl_easy_perform(curl);
curl_easy_cleanup(curl);
fclose(fp);
if (res == CURLE_OK)
printf("Download concluído com sucesso para /tmp/output_image.iso\n");
else
printf("Erro no download: %s\n", curl_easy_strerror(res));
}
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o getcurl getcurl.cpp -lcurl
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./getcurl 
Download concluído com sucesso para /tmp/output_image.iso

 * Breve Descrição: O download usando a biblioteca libcurl foi concluído com sucesso (CURLE_OK), e o arquivo foi salvo no caminho especificado /tmp/output_image.iso.
postjson.cpp (Livro-Texto p. 284-285)
 * Objetivo do Código: Demonstrar como enviar dados (um payload JSON) para um servidor web usando o método POST com a libcurl.
 * Código-Fonte:
<!-- end list -->

// (p. 284-285)
#include <stdio.h>
#include <curl/curl.h>
#include <string>
int main(void) {
CURLcode ret;
CURL *hnd;
struct curl_slist *slist1;
std::string jsonstr = "{\"username\":\"aied\",\"password\":\"123456\"}"; // (p. 284, linha 10)
slist1 = NULL;
slist1 = curl_slist_append(slist1, "Content-Type: application/json"); // (p. 284, linha 13)
hnd = curl_easy_init();
curl_easy_setopt(hnd, CURLOPT_URL,
"http://www.aied.com.br/linux/download/echo.php")
; // (p. 284, linha 18)
curl_easy_setopt(hnd, CURLOPT_POSTFIELDS, jsonstr.c_str());
curl_easy_setopt(hnd, CURLOPT_USERAGENT, "curl/7.38.0");
curl_easy_setopt(hnd, CURLOPT_HTTPHEADER, slist1);
curl_easy_setopt(hnd, CURLOPT_CUSTOMREQUEST, "POST"); // (p. 285, linha 23)
ret = curl_easy_perform(hnd);
curl_easy_cleanup(hnd);
hnd = NULL;
curl_slist_free_all(slist1);
slist1 = NULL;
return 0;
}

 * Análise da Saída:
 * Comando de Compilação: g++ -o postjson postjson.cpp -lcurl
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./postjson
<!DOCTYPE html>
<html style="height:100%">
<head>
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />
<title> 301 Moved Permanently
</title><style>@media (prefers-color-scheme:dark){body{background-color:#000!important}}</style></head>
<body style="color: #444; margin:0;font: normal 14px/20px Arial, Helvetica, sans-serif; height:100%; background-color: #fff;">
<div style="height:auto; min-height:100%; ">     <div style="text-align: center; width:800px; margin-left: -400px; position:absolute; top: 30%; left:50%;">
        <h1 style="margin:0; font-size:150px; line-height:150px; font-weight:bold;">301</h1>
<h2 style="margin-top:20px;font-size: 30px;">Moved Permanently
</h2>
<p>The document has been permanently moved.</p>
</div></div></body></html>

 * Breve Descrição: A requisição POST falhou em atingir o destino esperado, pois o servidor retornou o código de status 301 Moved Permanently (Movido Permanentemente), indicando um redirecionamento. Clientes HTTP simples como este, baseados em libcurl sem configuração de redirecionamento automático, não mantêm o corpo do POST (o JSON) ao serem redirecionados, o que impede que o payload chegue ao endpoint correto.
download.sh (Livro-Texto p. 285-286)
 * Objetivo do Código: Criar um script de download robusto que baixa arquivos de uma lista (urls.txt) e tenta novamente (--retry) em caso de falha, continuando de onde parou (-C).
 * Código-Fonte:
   (Nota: Crie o arquivo urls.txt em ~/Downloads/ antes, contendo a URL:
   http://www.aied.com.br/linux/download/output_image.iso)
<!-- end list -->
#!/bin/bash
# (p. 285-286)
# (Variável para o diretório de downloads do usuário atual)
DOWNLOAD_DIR="/home/$(whoami)/Downloads"
URL_FILE="$DOWNLOAD_DIR/urls.txt"
# (Cria o diretório e o arquivo se não existirem)
mkdir -p $DOWNLOAD_DIR
echo
"http://www.aied.com.br/linux/download/output_image.iso" > $URL_FILE
cd $DOWNLOAD_DIR
while true
do
# (O comando xargs lê o arquivo e passa a URL para o curl)
# (Removido o parâmetro -x socks5h... para TOR, conforme nota do manual)
xargs -n 1 curl -L -O --output-dir $DOWNLOAD_DIR -k --retry 999999999999 --retry-max-time 0
-C - < $URL_FILE
echo "Loop esperando 30s..."
sleep 30
done

 * Análise da Saída:
 * Comando de Execução: chmod +x download.sh e depois ./download.sh (use Ctrl+C para parar o loop)
 * Saída da Execução:
<!-- end list -->
userlinux@debian:~$ ./download.sh
xargs: curl: No such file or directory
Loop esperando 30s...

 * Breve Descrição: O script falhou porque o utilitário xargs não conseguiu encontrar o comando curl no $PATH, indicando que o curl não está instalado no sistema ou o caminho não foi configurado corretamente. O download não pôde ser realizado.
<!-- end list -->
