`nvm`（Node Version Manager）是一个流行的工具，用于在同一台机器上安装和管理多个版本的Node.js。通过使用`nvm`，你可以轻松地在不同的Node.js版本之间切换，以适应不同的项目需求。以下是使用`nvm`切换Node.js版本的步骤：

1. **安装`nvm`**：
   首先，你需要在你的机器上安装`nvm`。安装方法因操作系统而异。以下是在一些常见操作系统上的安装方法：

   - **在Linux或macOS上**，你可以使用`curl`或`wget`来安装`nvm`。以下是使用`curl`的示例命令：

     ```bash
     curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
     ```

     或者，如果你更喜欢使用`wget`：

     ```bash
     wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
     ```

   - **在Windows上**，你可以使用`nvm-windows`，这是一个专门为Windows系统设计的`nvm`版本。你可以从GitHub上的项目页面下载安装程序并安装：https://github.com/coreybutler/nvm-windows

2. **检查`nvm`安装**：
   安装完成后，你需要确保`nvm`已经正确安装并可用。在终端中运行以下命令来检查`nvm`版本：

   ```bash
   nvm --version
   ```

3. **列出可用的Node.js版本**：
   使用以下命令列出所有通过`nvm`可用的Node.js版本：

   ```bash
   nvm list-remote
   ```

4. **安装特定版本的Node.js**：
   如果你想安装一个新的Node.js版本，可以使用以下命令：

   ```bash
   nvm install <version>
   ```

   替换`<version>`为你想要安装的Node.js版本。例如，安装Node.js版本14.17.0：

   ```bash
   nvm install 14.17.0
   ```

5. **切换Node.js版本**：
   安装完特定版本的Node.js后，你可以使用以下命令来切换到该版本：

   ```bash
   nvm use <version>
   ```

   例如，切换到Node.js版本14.17.0：

   ```bash
   nvm use 14.17.0
   ```

6. **设置默认Node.js版本**：
   如果你想为所有新的终端会话设置默认的Node.js版本，可以使用以下命令：

   ```bash
   nvm alias default <version>
   ```

   例如，设置Node.js版本14.17.0为默认版本：

   ```bash
   nvm alias default 14.17.0
   ```

7. **验证当前使用的Node.js版本**：
   切换版本后，你可以使用以下命令来验证当前正在使用的Node.js版本：

   ```bash
   node --version
   ```

通过以上步骤，你可以轻松地使用`nvm`在不同的Node.js版本之间进行切换，以满足不同项目的需求。记得在切换版本之前保存你的工作，因为某些项目可能依赖于特定版本的Node.js。