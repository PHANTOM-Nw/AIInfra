# BLIP: 统一理解和生成的自举多模态模型

Author By: 李佳函

## 引言

### 背景与挑战

- 单模态模型的局限性
- 图文数据噪声问题（网络爬取数据质量差）
- 多模态任务需求激增（VQA/图像描述/图文检索）

### BLIP的诞生

- 提出机构：Salesforce Research
- 核心目标：解决数据噪声 + 统一理解/生成任务
- 关键突破：`Bootstrapping`机制 + 多任务架构

## 核心技术：Bootstrapping 机制

### 核心流程

### 关键组件

#### Captioner（生成器）

+ 功能：为图像生成高质量文本描述

+ 架构：基于Transformer的图像条件解码器

#### Filter（过滤器）

+ 功能：评估图文对匹配度

+ 技术：图文匹配（ITM）头部 + 对比学习

## 模型架构设计

### 统一框架

#### 视觉编码器

ViT/ViT-L 结构

224×224 图像输入

#### 文本编码器

BERT-base 架构

特殊设计：跨模态注意力层

#### 多模态混合编码器

插入跨模态注意力层

支持任务：VQA/图文检索

#### 图像条件文本解码器

因果掩码 + 跨模态注意力

支持任务：图像描述生成

### 预训练目标


| 损失函数            | 作用             | 对应模块 |
| :------------------ | :--------------- | :------- |
| ITC（图文对比损失） | 对齐图文特征空间 | 编码器   |
| ITM（图文匹配损失） | 细粒度图文匹配   | 编码器   |
| LM（语言建模损失）  | 生成连贯文本描述 | 解码器   |

## 