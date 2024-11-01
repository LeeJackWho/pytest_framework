# pytest_framework

> **说明**：本仓库为个人作品，因历史原因以 fork 形式存在于当前账号下，代码与内容均由本人（LeeJackWho）独立开发与维护，早期版本发布于个人旧账号ljxpython。
基于 Pytest 二次封装的自动化测试框架，把用例管理、数据驱动与测试结果落库整合在一起。

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Pytest](https://img.shields.io/badge/Pytest-7%2B-2ea44f)
![Allure](https://img.shields.io/badge/Allure-2.13%2B-ff6b8b)
![License](https://img.shields.io/badge/License-MIT-green)

## 能解决什么问题

手工写用例时反复处理这些事很枯燥，框架把它们收进配置与基类：

- **用例与代码分离**：用例定义走数据库模型（Suite / Case / TestPlan），改数据不改代码
- **结果自动落库**：每条用例的通过状态、耗时与日志写入数据库，直接对接测试管理平台
- **多格式报告同时产出**：Allure + JUnit XML 一次运行双份输出
- **外部可调用**：`main.py` 提供命令行入口，也支持被其他程序当模块调用发起测试

## 技术栈

Python · Pytest · Allure · Playwright（部分用例）· ORM 模型层 · Click CLI

## 目录结构

```
pytest_framework/
├── main.py                 # 命令行入口：初始化数据库、调度测试、结果落库
├── pytest.ini              # testpaths / addopts（allure、junit 输出目录）
├── conf/                   # 配置层
│   ├── config.py           # 配置读取
│   ├── constants.py        # 常量
│   └── settings.yaml       # 项目级配置
├── src/
│   ├── model/              # 数据模型：Case、Suite、TestPlan、TestResult
│   ├── client/             # 对外调用客户端
│   └── utils/              # 工具函数
├── tests/                  # 用例目录
│   ├── conftest.py         # 全局 fixture
│   ├── example.py          # 示例用例
│   ├── request_demo.py     # 接口用例示例
│   ├── test_user/          # 按模块划分的用例
│   └── test_goods/
└── practice/               # 练习代码（线程示例等）
```

## 快速开始

```bash
# 1. 安装依赖
pip install -r requirements.txt

# 2. 按环境调整配置
vim conf/settings.yaml

# 3. 运行全部用例（同时产出 Allure + JUnit 报告）
pytest

# 或使用命令行入口
python main.py --help
```

### 报告位置

| 报告 | 路径 |
|---|---|
| Allure 原始结果 | `output/allure-result/` |
| JUnit XML | `output/junit/report.xml` |

## 使用建议

- **addopts 已内置 `--strict-markers`**：自定义标记必须在 `pytest.ini` 注册后再用，否则直接报错
- **配置分层**：环境差异部分走本地覆盖文件，避免把环境信息写进版本库
- **新增用例**：在 `tests/` 下按模块建目录，文件名以 `test_` 开头即可被自动收集

## 许可

MIT
