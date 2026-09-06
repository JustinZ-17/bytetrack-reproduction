# bytetrack-reproduction
对ByteTrack在Colab上进行复现的笔记
# ByteTrack 复现：从零在 Colab 上跑通多目标跟踪

大二暑假到九月初完成。在 Google Colab（免费 T4 GPU）上复现
[ByteTrack](https://github.com/ifzhang/ByteTrack) 多目标跟踪流程，
并用自己拍摄的视频完成跟踪测试。

## 做了什么
- 在 Colab 上搭建 YOLOX + ByteTrack 完整环境（Python 3.13）
- 跑通官方 demo：785 帧，约 12.8 fps
- 替换为自己拍摄的视频，完成 508 帧行人跟踪
- 整理踩坑记录与解决方案（见下）

## 踩过的坑（部分）
| 问题 | 原因 | 解决 |
| onnxruntime 1.8.0 装不上 | Python 3.13 无对应版本 | 改装新版，忽略版本锁定 |
| cv2.waitKey 报错 | Colab 无 GUI 环境 | 修改 demo_track.py 绕过 |
| 视频尾部跟踪截断 | 源视频 HEVC 编码损坏 | 转码 H.264 后重跑 |
| 运行时被回收文件丢失 | Colab 机制 | 结果持久化到 Google Drive |

## 复现步骤
见 `bytetrack_colab.ipynb`（含完整可运行的 12 个单元格与环境重建流程）。
由于是初学者第一次使用colab，遇到了很多次断连、丢失等问题，故存在许多修复、检查、重做等繁琐步骤，导致代码很繁琐冗长，但作为学习记录就不做优化了。

## 跟踪效果
![跟踪效果](results/demo.gif)

## 参考
- [ByteTrack: Multi-Object Tracking by Associating Every Detection Box](https://arxiv.org/abs/2110.06864)（Zhang et al., ECCV 2022）
- 代码基于 [ifzhang/ByteTrack](https://github.com/ifzhang/ByteTrack)，仅作学习复现
