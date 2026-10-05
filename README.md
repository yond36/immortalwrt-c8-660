# ImmortalWrt 21.02 for NRadio C8-660 (WT9103)

通过 GitHub Actions 云端编译 [hanwckf/immortalwrt-mt798x](https://github.com/hanwckf/immortalwrt-mt798x)（openwrt-21.02 分支），产出 NRadio WT9103 (C8-660) 4G CPE 固件。

## 产物

| 文件 | 用途 |
|---|---|
| `nradio_wt9103_512m*-factory.bin` | 512M 变体首次刷入（ubi 覆盖整片 NAND，推荐） |
| `nradio_wt9103*-factory.bin` | 112M ubi 变体首次刷入 |
| `*-sysupgrade.bin` | 同机刷机升级 |

在 Actions 页面手动触发，或在 Release 页下载成品。

## 配置说明

- 设备配置：`configs/wt9103.config`（基于上游 defconfig 裁剪到 WT9103 双变体）
- 额外加入了 4G 模组驱动：qmi_wwan / cdc-mbim / ncm / rndis / option 串口，及 `uqmi`、`umbim` 用户态工具
- WiFi 保持 MTK mt_wifi 驱动 + LuCI 管理界面（中文）

## 刷机注意

- 当前固件（原厂 OpenWrt 定制）`board_name` 与本项目不匹配，sysupgrade 会被拒；首次刷入需用 `factory.bin` 走 `mtd write` / uboot
- 只写 `ubi` 分区，切勿碰 BL2 / FIP / factory（factory 存无线校准数据）
