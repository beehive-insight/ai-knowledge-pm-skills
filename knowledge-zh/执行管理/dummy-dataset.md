---
name: dummy-dataset
description: "生成具有可自定义列、约束和输出格式（CSV、JSON、SQL、Python 脚本）的真实测试数据集。适用于创建测试数据、构建模拟数据集或为开发和演示生成样本数据。"
---

# 模拟数据集生成

生成具有可自定义列、约束和输出格式（CSV、JSON、SQL、Python 脚本）的真实测试数据集。创建可执行脚本或直接数据文件以供立即使用。

**适用场景：** 创建测试数据、生成样本数据集、为开发构建真实的模拟数据或填充测试环境。

**参数：**
- `$PRODUCT`：产品或系统名称
- `$DATASET_TYPE`：数据类型（例如，客户反馈、交易、用户资料）
- `$ROWS`：要生成的行数（默认：100）
- `$COLUMNS`：要包含的特定列或字段
- `$FORMAT`：输出格式（CSV、JSON、SQL、Python 脚本）
- `$CONSTRAINTS`：其他约束或业务规则

## 分步流程

1. **识别数据集类型** - 了解数据领域
2. **定义列规范** - 名称、数据类型和值范围
3. **确定行数** - 需要多少样本记录
4. **选择输出格式** - CSV、JSON、SQL INSERT 或 Python 脚本
5. **应用真实模式** - 确保数据看起来真实有效
6. **添加业务约束** - 尊重业务逻辑和关系
7. **生成或脚本数据** - 创建可执行输出
8. **验证输出** - 确保数据质量和完整性

## 模板：Python 脚本输出

```python
import csv
import json
from datetime import datetime, timedelta
import random

# 配置
ROWS = $ROWS
FILENAME = "$DATASET_TYPE.csv"

# 带有真实值生成器的列定义
columns = {
    "id": "auto-increment",
    "name": "first_last_name",
    "email": "email",
    "created_at": "timestamp",
    # 添加更多列...
}

def generate_dataset():
    """生成真实的模拟数据集"""
    data = []
    for i in range(1, ROWS + 1):
        record = {
            "id": f"U{i:06d}",
            # 根据列定义生成值
        }
        data.append(record)
    return data

def save_as_csv(data, filename):
    """将数据集保存为 CSV"""
    with open(filename, 'w', newline='') as f:
        writer = csv.DictWriter(f, fieldnames=data[0].keys())
        writer.writeheader()
        writer.writerows(data)

if __name__ == "__main__":
    dataset = generate_dataset()
    save_as_csv(dataset, FILENAME)
    print(f"在 {FILENAME} 中生成了 {len(dataset)} 条记录")
```

## 示例数据集规范

**数据集类型：** 客户反馈

**列：**
- feedback_id（自动递增，U001、U002...）
- customer_name（真实姓名）
- email（有效电子邮件格式）
- feedback_date（过去 90 天的日期）
- rating（1-5 星）
- category（Bug、功能请求、投诉、表扬）
- text（真实反馈）
- product（电子产品、服装、家居）

**约束：**
- 评分分布：40% 5 星，30% 4 星，20% 3 星，10% 1-2 星
- Bug 类别仅用于 1-3 星评分
- 功能请求仅用于 3-5 星评分
- 电子邮件域名真实（gmail、yahoo、company.com）

## 输出交付物

- 可执行的 Python 脚本或直接数据文件
- 带有适当标题和格式的 CSV 文件
- 具有有效结构和类型的 JSON 文件
- 用于数据库填充的 SQL INSERT 语句
- 数据验证和约束合规性
- 真实、适合业务的值
- 数据生成逻辑的文档
- 使用数据集的快速入门说明

## 输出格式

**CSV：** 扁平表格格式，易于导入电子表格和数据库

**JSON：** 嵌套结构，适合 API 和 NoSQL 数据库

**SQL：** INSERT 语句，可直接在关系型数据库上执行

**Python 脚本：** 用于自定义或大型数据集的可执行生成器
