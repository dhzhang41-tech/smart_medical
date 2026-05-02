```markdown
# 智医助手

这是我在学习大模型应用开发过程中独立完成的一个项目，结合知识图谱和大语言模型，
实现了一个能回答医疗相关问题的智能助手。

## 项目背景

医疗信息专业性强，普通用户很难快速获取准确的医学知识。
这个项目通过构建医疗领域知识图谱，结合 DeepSeek 大模型，
让用户可以用自然语言查询疾病、症状、药物、饮食等医疗信息。

## 技术栈

- 知识图谱：Neo4j
- 向量数据库：ChromaDB  
- 关系数据库：MySQL
- 大语言模型：DeepSeek API
- 后端框架：FastAPI
- 嵌入模型：bge-base-zh-v1.5

## 项目结构

```
smart_medical/
├── src/
│   ├── agent/          # 意图识别与 Cypher 查询生成
│   ├── backend/        # FastAPI 后端 + 前端页面
│   ├── configuration/  # 数据库连接配置
│   └── datasync/       # 数据清洗、实体对齐、导入
├── data/               # 数据文件（需自行准备，见下方说明）
├── pretrained/         # 预训练模型（需自行下载，见下方说明）
└── .env                # API Key 配置（需自行创建）
```

## 运行方法

### 1. 下载预训练模型
将以下模型下载后放入 `pretrained/` 目录：
- [bge-base-zh-v1.5](https://huggingface.co/BAAI/bge-base-zh-v1.5)
- [bert-base-chinese](https://huggingface.co/google-bert/bert-base-chinese)
- [mengzi-t5-base](https://huggingface.co/Langboat/mengzi-t5-base)

### 2. 准备数据
将以下数据放入 `data/` 目录：
- `data/knowledge_graph/medical_kg.jsonl`
- `data/annotated_data/CMeIE-V2.jsonl`

### 3. 配置环境变量
在项目根目录新建 `.env` 文件：
```
DEEPSEEK_API_KEY=你的DeepSeek API Key
```

### 4. 启动数据库
- 启动 MySQL
- 启动 Neo4j 并安装 APOC 插件

### 5. 数据准备
```bash
cd src/datasync
python data_prepare.py
```

### 6. 启动服务
```bash
cd src/backend
python app.py
```

### 7. 访问页面
浏览器打开 `http://127.0.0.1:8000`

## 可以问什么

- 某个疾病有哪些症状
- 某个疾病应该挂什么科
- 某个疾病不能吃什么
- 某个症状可能是什么病
- 某个疾病怎么预防

## 作者

上海大学
