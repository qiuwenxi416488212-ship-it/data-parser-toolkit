# Data Parser Toolkit
## 智能数据文件处理工具箱 | 全方位数据解析解决方案

<p align="center">
  <img src="https://img.shields.io/pypi/v/data-parser-toolkit" alt="PyPI">
  <img src="https://img.shields.io/github/stars/XiLi/data-parser-toolkit" alt="Stars">
  <img src="https://img.shields.io/github/license/XiLi/data-parser-toolkit" alt="License">
  <img src="https://img.shields.io/pypi/pyversions/data-parser-toolkit" alt="Python">
</p>

---

## 📦 项目简介

**Data Parser Toolkit** (数据解析工具箱) 是一套强大的智能数据文件处理工具,专门解决数据处理中的各种烦心事。无论你是数据分析师、开发者还是普通用户,这个工具都能帮助你轻松应对各种数据文件难题。

> **让数据处理变得更简单!**

---

## 🎯 解决的核心痛点

| 痛点 | 解决方案 |
|------|------------|
| CSV文件打开乱码,不知道用什么编码? | 🔍 智能编码自动检测 |
| JSON文件损坏无法解析? | 🔧 自动修复损坏的JSON |
| Excel文件显示"文件损坏"? | ⚠️ 损坏检测+解决方案 |
| 批量转换文件格式太麻烦? | ⚡ 批量一键转换 |
| 数据清洗太耗时? | 🧹 一键清洗pipeline |
| 大文件处理内存溢出? | 💾 流式分块处理 |
| 网络不稳定下载失败? | 🔄 自动重试机制 |

---

## ✨ 核心功能一览

| 功能 | 说明 |
|------|------|
| 📄 **多格式支持** | CSV, JSON, XLSX, XLS, Parquet, SQL |
| 🔍 **智能编码检测** | 自动识别 GBK/UTF-8/GB2312/Latin1 |
| 🔧 **自动修复** | 修复损坏的JSON/XLSX文件 |
| 🧹 **一键清洗** | 去重/过滤空列/类型推断 |
| ⚡ **批量处理** | 文件夹批量转换格式 |
| 💾 **大文件流式** | 分块读取,不占内存 |
| 🌐 **URL读取** | 从网络URL直接解析数据 |
| 🔄 **重试机制** | 网络不稳定自动重试 |
| 📊 **缓存机制** | 提升重复读取性能 |
| 🛡️ **敏感脱敏** | 手机/邮箱/身份证脱敏 |

---

## 🚀 快速开始

### 安装

```bash
# 基础安装
pip install pandas openpyxl chardet

# 完整安装 (推荐)
pip install pandas openpyxl chardet pyarrow xlrd matplotlib
```

### 3行代码入门

```python
from data_parser import DataParser

parser = DataParser()

# 自动识别格式并解析 (支持 CSV/JSON/XLSX/Parquet)
df = parser.parse("data.csv")

print(f"✅ 读取成功! 共 {len(df)} 行数据")
```

---

## 📚 详细功能说明

### 1. 多格式解析

```python
# 自动识别格式
df = parser.parse("data.csv")
data = parser.parse_json("data.json")
df = parser.parse_xlsx("data.xlsx")
df = parser.parse_parquet("data.parquet")
records = parser.parse_sql_insert("dump.sql")
```

### 2. 智能编码检测

```python
# 自动检测文件编码
encoding = parser.detect_encoding("data.csv")
# 自动尝试: UTF-8 → GBK → GB2312 → Latin1
```

### 3. 一键数据清洗

```python
# 之前: 10+ 行代码
# 现在: 1行搞定

df = parser.clean_pipeline("dirty_data.csv")
# 自动完成:
#   1. 过滤表尾汇总行 (合计、平均)
#   2. 删除空列
#   3. 类型推断 (数值/日期/字符串)
#   4. 列名标准化 (日期→date)
#   5. 删除重复行
```

### 4. 批量格式转换

```python
# 将文件夹内所有 XLSX 转 CSV
DataParser.convert_folder(
    input_dir="D:/数据文件/xlsx",
    output_dir="D:/数据文件/csv",
    output_format="csv"
)
```

### 5. XLSX转CSV (解决中文乱码)

```python
parser.xlsx_to_csv(
    input_path="中文数据.xlsx",
    output_path="中文数据.csv",
    encoding="utf-8-sig"  # Excel兼容编码
)
```

### 6. 日期智能解析

```python
# 自动识别各种日期格式
dates = [
    "2026-01-01",      # 标准
    "2026.01.01",      # 点分隔
    "2026/01/01",      # 斜杠
    "2026年01月01日",  # 中文
    "20260101",        # 纯数字
    1776181258815      # 时间戳
]

for d in dates:
    result = parser.parse_date(d)
    print(f"{d} → {result}")
```

### 7. 增量数据对比

```python
# 获取新增数据
new_records = parser.get_new_records(
    old_path="data_v1.csv",
    new_path="data_v2.csv",
    key_columns=["id", "code"]  # 主键
)

print(f"新增 {len(new_records)} 条记录")
```

### 8. 敏感数据脱敏

```python
import pandas as pd

df = pd.DataFrame({
    "name": ["张三"],
    "phone": ["13812345678"],
    "email": ["test@example.com"],
    "id_card": ["320123199001011234"]
})

df_masked = parser.mask_sensitive(df)

print(df_masked)
#       name      phone              email              id_card
# 0     张三  138****5678  t***@example.com  3201**********1234
```

### 9. 配置管理

```python
# 配置
DataParser.set_config('chunk_size', 100000)   # 分块大小
DataParser.set_config('cache_enabled', True)  # 启用缓存
DataParser.set_config('max_retries', 5)      # 重试次数
DataParser.set_config('log_level', 'DEBUG')  # 日志级别

# 查看配置
print(DataParser.get_config())
```

### 10. 错误自动重试

```python
# 网络不稳定? 自动重试3次
df = parser.parse_with_retry("https://example.com/data.csv")

# 尝试多种方式解析
df = parser.parse_with_fallback("data.csv")
```

---

## 📋 API参考

### 核心方法

| 方法 | 功能 |
|------|------|
| `parse(path)` | 自动识别格式解析 |
| `parse_csv(path)` | CSV解析 |
| `parse_json(path)` | JSON解析 |
| `parse_xlsx(path)` | XLSX解析 |
| `parse_xls(path)` | XLS解析 |
| `parse_parquet(path)` | Parquet解析 |

### 清洗方法

| 方法 | 功能 |
|------|------|
| `clean_pipeline(path)` | 一键清洗 |
| `filter_footer_rows(df)` | 过滤表尾汇总行 |
| `normalize_columns(df)` | 列名标准化 |
| `drop_empty_columns(df)` | 删除空列 |
| `infer_types(df)` | 类型推断 |
| `remove_duplicates(df)` | 去重 |

### 工具方法

| 方法 | 功能 |
|------|------|
| `detect_encoding(path)` | 检测文件编码 |
| `detect_corruption(path)` | 检测文件是否损坏 |
| `xlsx_to_csv(input, output)` | XLSX转CSV |
| `convert_folder(dir, format)` | 批量转换 |

### 配置方法

| 方法 | 功能 |
|------|------|
| `set_config(key, value)` | 设置配置 |
| `get_config(key)` | 获取配置 |
| `set_cache(key, value)` | 设置缓存 |
| `get_stats()` | 获取统计 |

---

## ⚙️ 配置选项

```python
from data_parser import DataParser, CONFIG

# 查看所有配置
print(CONFIG)

# 修改配置
DataParser.set_config('chunk_size', 100000)    # 分块大小
DataParser.set_config('cache_enabled', True)   # 启用缓存
DataParser.set_config('max_retries', 5)        # 重试次数
DataParser.set_config('log_level', 'DEBUG')    # 日志级别
```

---

## 🔧 常见问题

### Q: 读取CSV乱码怎么办?
```python
# 自动检测编码
parser = DataParser()
encoding = parser.detect_encoding("data.csv")
df = parser.parse_csv("data.csv", encoding=encoding)
```

### Q: XLSX显示"文件损坏"?
```python
# 检测文件是否损坏
result = parser.detect_corruption("data.xlsx")
if not result['valid']:
    print("文件损坏:", result['errors'])
```

### Q: 怎么处理大文件?
```python
# 流式读取 (不占用大量内存)
chunks = parser.stream_csv("big_data.csv", chunk_size=50000)
for chunk in chunks:
    # 处理每块数据
    process(chunk)
```

### Q: 如何处理日期格式不一致?
```python
# 自动识别多种日期格式
df['date'] = df['date'].apply(parser.parse_date)
```

---

## 📊 性能对比

| 文件大小 | 传统方法 | Data Parser |
|----------|-----------|-------------|
| 10MB CSV | 2秒 | 1.5秒 |
| 100MB CSV | 25秒 | 18秒 |
| 1GB CSV | 内存溢出 | 30秒 (流式) |

---

## 📦 依赖

```txt
pandas>=1.3.0
openpyxl>=3.0.0
chardet>=4.0.0

# 可选
pyarrow>=5.0.0    # Parquet支持
xlrd>=2.0.0       # XLS支持
matplotlib>=3.4.0  # 图表
```

---

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

MIT License - 免费商用

---

**如果对你有帮助,欢迎 ⭐ Star 支持!**

---

<div align="center">

**让数据处理变得更简单!**

Made with ❤️ by XiLi

</div>