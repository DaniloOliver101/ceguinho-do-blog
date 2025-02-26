

# **Configurando o Ambiente Java com IntelliJ para Usuários de Leitor de Telas no Windows**  

Este artigo orienta usuários de leitor de telas na configuração do ambiente de desenvolvimento Java no Windows, incluindo a instalação do Java 17 da Oracle, configuração do Java Access Bridge, instalação do Maven 3.9.9 e IntelliJ IDEA Community 2024.3.1.1.  

---

## **1. Instalando o Java 17 da Oracle**  

### **Passo 1: Baixar o Java 17**  
1. Acesse o site oficial da Oracle:  
   👉 [https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)  
2. Escolha a versão **Windows x64 Installer (.exe)**.  
3. Aceite os termos de licença e faça o download.  

### **Passo 2: Instalar o Java**  
1. Abra o arquivo baixado (`jdk-17_windows-x64_bin.exe`).  
2. Siga as instruções do instalador. O caminho padrão de instalação será:  
   ```
   C:\Program Files\Java\jdk-17
   ```
3. Aguarde a conclusão e clique em **Fechar**.  

### **Passo 3: Configurar a variável de ambiente `JAVA_HOME`**  
1. Pressione `Win + R`, digite **sysdm.cpl** e pressione `Enter`.  
2. Vá até a guia **Avançado** e clique em **Variáveis de Ambiente**.  
3. Na seção **Variáveis do sistema**, clique em **Novo** e adicione:  
   - **Nome da variável:** `JAVA_HOME`  
   - **Valor da variável:** `C:\Program Files\Java\jdk-17`  
4. Encontre a variável **Path**, selecione e clique em **Editar**.  
5. Clique em **Novo** e adicione o seguinte caminho:  
   ```
   %JAVA_HOME%\bin
   ```
6. Confirme tudo clicando em **OK**.  

### **Passo 4: Testar a instalação**  
Abra o **Prompt de Comando (`cmd`)** e digite:  
```shell
java -version
```
Se a instalação estiver correta, a saída será semelhante a:  
```
java version "17.0.X" 202X-XX-XX LTS
```

---

## **2. Configurando o Java Access Bridge**  

O Java Access Bridge permite que leitores de tela interajam com aplicações Java.  

### **Passo 1: Ativar o Java Access Bridge**  
Abra o **Prompt de Comando (`cmd`)** como **Administrador** e execute:  
```shell
jabswitch -enable
```
Se não houver mensagens de erro, o Access Bridge foi ativado com sucesso.  

### **Passo 2: Verificar se está ativado**  
Execute novamente:  
```shell
jabswitch
```
Se **nenhuma mensagem for exibida**, o Java Access Bridge está ativo.  

---

## **3. Instalando o Maven 3.9.9**  

O Maven é uma ferramenta essencial para gerenciamento de projetos Java.  

### **Passo 1: Baixar o Maven**  
1. Acesse o site oficial:  
   👉 [https://maven.apache.org/download.cgi](https://maven.apache.org/download.cgi)  
2. Baixe o arquivo **Binary zip archive** (`apache-maven-3.9.9-bin.zip`).  

### **Passo 2: Extrair e configurar**  
1. Extraia o conteúdo para:  
   ```
   C:\Apache\Maven
   ```
2. Configure as variáveis de ambiente:  
   - **MAVEN_HOME** → `C:\Apache\Maven`  
   - **Path** → Adicione:  
     ```
     %MAVEN_HOME%\bin
     ```

### **Passo 3: Testar a instalação**  
Abra o **cmd** e execute:  
```shell
mvn -version
```
Se tudo estiver correto, você verá algo como:  
```
Apache Maven 3.9.9
Java version: 17.0.X
```

---

## **4. Instalando o IntelliJ IDEA Community 2024.3.1.1**  

### **Passo 1: Baixar o IntelliJ**  
1. Acesse o site oficial:  
   👉 [https://www.jetbrains.com/idea/download/](https://www.jetbrains.com/idea/download/)  
2. Baixe a versão **Community Edition**.  

### **Passo 2: Instalar**  
1. Execute o instalador (`ideaIC-2024.3.1.1.exe`).  
2. Siga as instruções e marque a opção **Add launchers dir to the PATH**.  
3. Conclua a instalação e abra o IntelliJ.  

---

## **5. Configurar o IntelliJ para Usuários de Leitor de Telas**  

### **Passo 1: Ativar suporte a leitores de tela**
1. **Abra o IntelliJ** e pressione `Ctrl + Shift + A`.  
2. Digite **Screen Reader Support** e pressione `Enter`.  
3. Ative a opção **Enable screen reader support**.  

### **Passo 2: Selecionar o Java 17 no IntelliJ**  
1. Vá em `File > Project Structure > SDKs`.  
2. Clique em **Add JDK** e selecione `C:\Program Files\Java\jdk-17`.  
3. Confirme e feche a janela.  

Agora o ambiente Java está pronto para desenvolvimento com suporte a leitores de tela! 🚀  

Se precisar de mais ajustes ou quiser adicionar mais detalhes, me avise! 😊