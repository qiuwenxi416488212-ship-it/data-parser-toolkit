# Data Parser Skill - Complete Version
# 完整的数据解析技能，支持多种格式

## 文件结构
```
data-parser/
├── SKILL.md          # 技能说明
├── README.md         # 使用文档
├── data_parser.py     # 主代码
├── LICENSE          # MIT许可
└── requirements.txt # 依赖
```

## 完整功能列表 (54个方法)

### Core Functions
| 方法 | 功能 |
|------|------|
| parse() | 自动识别格式并解析 |
| parse_csv() | CSV解析 |
| parse_json() | JSON解析 |
| parse_xlsx() | XLSX解析 |
| parse_xls() | XLS解析 |
| parse_parquet() | Parquet解析 |
| parse_sql_insert() | SQL解析 |

### Transform
| 方法 | 功能 |
|------|------|
| xlsx_to_csv() | XLSX转CSV |
| csv_to_xlsx() | CSV转XLSX |
| convert_folder() | 批量转换 |

### Clean
| 方法 | 功能 |
|------|------|
| parse_date() | 日期解析 |
| filter_footer_rows() | 表尾过滤 |
| normalize_columns() | 列名标准化 |
| drop_empty_columns() | 空列删除 |
| infer_types() | 类型推断 |
| remove_duplicates() | 去重 |

### Validate
| 方法 | 功能 |
|------|------|
| detect_corruption() | 损坏检测 |
| validate_data() | 数据验证 |
| find_duplicates() | 重复标记 |

### Advanced
| 方法 | 功能 |
|------|------|
| parse_xlsx_sheets() | 多Sheet处理 |
| stream_csv() | 流式读取 |
| merge_and_dedupe() | 合并去重 |
| mask_sensitive() | 脱敏 |
| get_new_records() | 增量对比 |
| export_template() | 模板导出 |
| clean_pipeline() | 一键清洗 |

### Enterprise
| 方法 | 功能 |
|------|------|
| set_config() | 配置管理 |
| get_config() | 获取配置 |
| set_cache() / get_cache() | 缓存 |
| get_stats() | 统计 |
| parse_with_retry() | 重试机制 |
| parse_with_fallback() | 错误回退 |
| read_from_url() | URL读取 |
| parse_parallel() | 并行处理 |

## Install
```bash
pip install pandas openpyxl chardet pyarrow xlrd
```

## Quick Start
```python
from data_parser import DataParser

parser = DataParser()

# 自动解析任意格式
df = parser.parse("data.csv")

# 一键清洗
df = parser.clean_pipeline("dirty.csv")

# 批量转换
DataParser.convert_folder("input/", "csv")
```