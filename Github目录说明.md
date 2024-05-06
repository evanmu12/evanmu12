
# Github目录说明

## **Public类型**

### ngpu-partner-doc：
对接文档目录，目录中保存着算力需求方（APP方），接入AINNGPU时所会使用到的API接口，以及API接口说明。目前对接的6家APP方均采用这个文档进行对接。
* en.md：英文对接文档
* zh.md：中文对接文档

### ngpu-install-script：
算力节点安装脚本目录，目录中保存着算力节点接入AINNGPU时的安装脚本。由于算力节点分文两种：
* 算力节点：节点作为GPU算力存在，提供分发的工作空间，同时处理用户提交的AI任务。安装脚本 install_mcNode.sh。
* 测量节点：节点作为测量节点存在，提供对算力节点的网络带宽进行测量工作。安装脚本 install_measure.sh。

## **Private类型**

### **_<span style="color:green">ngpu-schedule</span>_**
调度目录，保存着与调度相关的程序代码：
* **<span style="color:green">match</span>**：撮合服务端代码主要管理算力节点，将算力节点数据上传到区块链，发布工作空间时选择最佳计算节点，算力节点离线时自动重新分配任务，并在用户启动AI任务时选择最适合的算力节点进行AI任务处理。撮合服务器是AINNGPU平台的最核心的服务端代码。因为是从区块链检索数据，因此支持多个撮合服务端实例同时运行。
* **<span style="color:green">pomc</span>**：pomc服务端主要用于定期激励算力节点提供者（网络激励），并将激励代币转移到计算节点的钱包中（如果没有钱包，则转移到算力节点的地址）。此外，pomc稍后还将为算力节点提供者提供任务激励，以及为用户提供任务激励。
* **<span style="color:green">apiServer</span>**：API接口服务端代码，主要用于为算力需求提供统一的API接口。它记录API调用次数、处理请求的算力节点、结果的内容以及处理时间。这些信息将用于后续对用户的激励和算力节点的任务激励。
* **workSpace**：当算力需求方发布工作空间时，这将触发workSpace服务端。workSpace会将分配信息发送到分发服务端进行进一步处理。此外，一旦工作空间分配完成，workSpace将通知算力节点启动工作空间的Docker镜像。
* **autoExport**：自动同步服务器。它的功能是将数据从区块链同步到链下数据库，实现链上数据与链下数据的同步。查询操作使用链下数据进行，而保存操作则在区块链上执行。
* **nodeListen**：nodeListen运行在算力节点上，用于监听区块链上的特定事件，以触发相应的功能（例如要求算力节点开始测试、启动Docker镜像、删除Docker镜像以及停止Docker镜像等）。

### **_<span style="color:green">ngpu-contract（基于OP链）</span>_**
智能合约目录，保存着目前AINNGPU所用到的智能合约代码，以及智能合约发布代码：
* ComputeNode.sol：算力节点存储、管理合约，保存着针对算力节点的注册、上线、下线、心跳、SLA等信息的智能合约。
* DockerContract.sol：Docker镜像管理合约，保存着Docker镜像的信息，包括镜像名、启动指令、目前分发的算力节点以及状态等等。
* Measure.sol：测量节点管理合约，保存着当前测量节点信息，目前正在测量的算力节点等信息。
* Pomc.sol：Token分配日志合约
* Progress.sol：工作空间分发进度合约
* Token.sol：Token合约

### **_<span style="color:green">ngpu-node-client</span>_**
算力节点客户端目录，保存着算力节点客户端相关代码，采用C++代码开发。算力客户端主要功能为空间测量、映射端口可用性测量、启动指定的工作空间等

### **_<span style="color:green">ngpu-business-backend</span>_**
业务后台目录，保存着对接AINNGPU.io官网上的后台API接口功能代码。

### ngpu-frontend：
业务前台目录，保存着AINNGPU.io官网的前台页面代码。

### **_<span style="color:green">ngpu-dispense</span>_**
工作空间分发代码目录，存放着dispense代码，用于定期向match服务端请求分发工作空间，match返回优选后的算力节点，dispense负责将工作空间分发到相应的算力节点。

### ngpu-transfer：
Harq传输客户端与服务端目录，目录中保存着采用Harq开发的客户端与服务端代码，同时采用Go语言编写的调用Harq客户端和服务端的插件代码。

### ngpu-cli：
Demo代码目录，存放着AINNGPU采用命令行运行时调用的脚本代码：
* **<span style="color:green">ngpu-cli/cli</span>**：存放着使用python语言编写的调用后台API接口的代码，以及下发一个工作空间并采用这个工作空间重新生成一个NFT图片。
* ngpu-cli/gen_instance：存放着使用python代码编写的调用gen-Instance的AI接口时的代码（本示例采用了photo2video的接口）

### ngpu-gen-instance：
存放着目前AINNGPU平台中所使用到的gen-instance源代码，这些源码均为开源代码。

### ngpu-download：
下载工作空间程序目录，保存着算力客户端中下载工作空间程序代码。

### ngpu-network-chain：
区块链目录，此目录保存着基于ETH修改成DPOS的链代码（此链基于ETH改成POS共识之前的版本）

### ngpu-config：
用于进行客户端自动更新时的配置服务端代码。

### ngpu-manual：
帮助文档目录，存放着AINNGPU.io官网中的帮助文档
