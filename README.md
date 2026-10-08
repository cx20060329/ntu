# NTU / FRT-HGN 项目完整包

骨骼动作识别研究项目（FRT-HGN / RACF，Quality-Aware 自适应融合，基线 CTR-GCN）的完整发布包：代码 + 预处理数据 + 权重 + 实验结果 + 论文 + 文献。

## 下载方法

完整压缩包因超过 GitHub 单文件 2GB 限制，拆分为 7 个分卷，见 [Releases](../../releases)：

FRT_HGN_release_20261008.zip.00.part … FRT_HGN_release_20261008.zip.06.part
FRT_HGN_release_20261008.zip.sha256

一条命令下载全部分卷（需 GitHub CLI）：`gh release download v1.0 -R cx20060329/ntu`，或在 Release 页面手动下载全部 7 个 .part 文件 + .sha256 文件放到同一目录。

## 合并分卷（复原原文件）

分卷是原 zip 的原始字节顺序切分（00 在最前、06 在最后），全部下载后按顺序拼接：

Windows (cmd)：
copy /b FRT_HGN_release_20261008.zip.00.part+FRT_HGN_release_20261008.zip.01.part+FRT_HGN_release_20261008.zip.02.part+FRT_HGN_release_20261008.zip.03.part+FRT_HGN_release_20261008.zip.04.part+FRT_HGN_release_20261008.zip.05.part+FRT_HGN_release_20261008.zip.06.part FRT_HGN_release_20261008.zip

Linux / macOS / Git Bash：
cat FRT_HGN_release_20261008.zip.??.part > FRT_HGN_release_20261008.zip

校验完整性（推荐）：sha256sum -c FRT_HGN_release_20261008.zip.sha256（Windows 可用 certutil -hashfile FRT_HGN_release_20261008.zip SHA256 对比）

然后正常解压 zip（Windows 自带解压支持 zip64 大文件）。

## 包内容（解压后约 35.9GB）

| 目录 | 内容 |
|---|---|
| 01_项目工程/ | rfh_ctrgcn_project 完整工程：代码、NTU60 CS/CV 预处理数据（各 9.5GB npz）、NTU120 原始骨架（57,600 个 .skeleton）、HD-GCN 权重、best_model.pt、pretrained.zip、3-seed 融合 logits 与评估结果 |
| 02_论文/ | IEEE Access 论文：latex_ieee（英文）+ latex_zh（中文对照）+ 开题提案/报告 |
| 03_导师往来/ | 导师反馈与修订回应材料 |
| 04_实验结果汇总/ | disjoint logits、导师结果汇总包 |
| 05_文献/ | 文献库与关键参考 PDF |
| 06_代码备份与云端补丁/ | 代码快照、SkateFormer 云端对比、热修复补丁 |
| 07_数据tar包/ | disjoint / unseen / skateformer_logits 三个 tar.gz |

包根目录附 README_目录说明.md：完整目录清单、未包含项说明、关键结果速查与复现入口。

## 关键结果

- NTU60 CS 四流融合 3-seed：92.50% ± 0.20%（CTR-GCN 92.4%）
- NTU60 CV 四流：96.69%（CTR-GCN 96.8%）
- 自适应融合鲁棒性：noise 扰动 +13.89pp（3-seed）

## 注意事项

- NTU RGB+D 数据集受研究协议约束（官方申请获取：https://rose1.ntu.edu.sg/dataset/actionRecognition）
- 解压后约 36GB，请确保磁盘空间充足
- 分卷为原始二进制切分，必须全部下载后按顺序合并，单个分卷无法解压
