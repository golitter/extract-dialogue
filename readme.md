# extract-dialogue-MajoTabi

本仓库fork于[KMnO4-zx/extract-dialogue: 从小说中提取对话数据集 (github.com)](https://github.com/KMnO4-zx/extract-dialogue/tree/master)仓库，用来提取轻小说《魔女之旅》中的伊雷娜对话信息，之后处理成Alpaca格式供以微调。

已从轻小说中提取2万＋的对话集，之后手动处理了二百条数据。

对话集详见：`output/elaina.json`

微调数据集详见：`elaina_Alpaca.json`

```json
[
    {
        "instruction": "欢迎来到魔法师之国。请进，魔女大人。",
        "input": "",
        "output": "？奇怪，不用进行我是否身为魔法师的审查吗？"
    },
    {
        "instruction": "啊哇哇哇哇！怎、怎怎怎怎么办，怎么办，我弄掉了这么多瓦片，弄不回来……",
        "input": "",
        "output": "在那之前不先道歉吗？"
    },
    {
        "instruction": "啊，对、对不起！我不是故意的！真的！",
        "input": "",
        "output": "话说回来，你还好吗？飞过来的时候非常豪爽的说。"
    }
]
```



> 项目待改进：
>
> 1. 使用多线程进行处理
> 2. 保存中断信息，以防从头开始
> 3. 需要手动处理的信息放置`config.ini`中

**⚠️ 本项目不包含任何小说原文，仅提供数据处理代码。使用者需自行确保数据来源合法性。**

克隆项目：

```shell
git clone git@github.com:golitter/extract-dialogue-MajoTabi.git
```

进入项目主目录：

```shell
cd extract-dialogue-MajoTabi-master/
```

环境配置：

```shell
# conda
conda create --name my_env --file spec-file.txt
# pip 
pip install -r requirements.txt
```

- 将文本放到`data`目录内，文本文件名为**英文**，文内编码格式为`utf-8`。

- 将`config_pub.ini`更改为`config.ini`，并配置好参数。运行`start.py`脚本进行处理文本，得到的数据在`output`目录内。

  ```python
  [settings]
  # API key for authentication
  api_key = {api_key}
  # Base URL of the API service
  base_url = {base_url}
  # Output file path for storing results
  file_name = ./output/elaina.json
  # Input file path containing the data to process
  file_path = ./data/mnzl.txt
  
  [progress]
  # The starting index for processing, useful for resuming progress
  start_idx = 0
  # Maximum token length allowed for each API request
  max_token_len = 600
  # Number of tokens to overlap between consecutive text chunks
  cover_content = 50
  ```

  

  挂后台运行：

  ```shell
  nohup python start.py > output.log 2>&1 &
  ```

- 在项目主目录内运行所有脚本即可。`test`目录内的文件运行采用`python -m test.example`形式运行。（不带`.py`）

- 将`output`目录内提取的数据集进行检查并手动处理成Alpaca格式。
