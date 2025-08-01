# Midea AC LAN

[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg)](https://github.com/hacs/integration)
[![Stable](https://img.shields.io/github/v/release/wuwentao/midea_ac_lan)](https://github.com/wuwentao/midea_ac_lan/releases/latest)
[![Super-Linter](https://github.com/wuwentao/midea_ac_lan/actions/workflows/linter.yml/badge.svg)](https://github.com/marketplace/actions/super-linter)

[English](README.md) | 简体中文 | [Discord交流群](https://discord.com/invite/ZWdd2fXndn) | [QQ交流群](https://qm.qq.com/q/l53SGEwlZ6)

通过本地局域网控制你的美的M-Smart设备

- 通过Home Assistant UI完成设备的自动搜索和配置.
- 生成额外的传感器和开关方便进行设备控制.
- 与设备保持TCP长连接以便实时同步设备状态.

本集成部分技术来源来自 [@mac-zhou](https://github.com/mac-zhou/midea-msmart), 他的美的midea-msmart提供了类似的功能。 该组件包括来自他的项目中经过改写的部分代码。

同时感谢[@NeoAcheron](https://github.com/NeoAcheron/midea-ac-py)

⭐如果本集成对你有所帮助, 请不吝为它点个星, 这将是对我的极大激励。

**_❗注意: 本集成需要 Home Assistant 2023.8 或更高版本_**

## 1. ❗❗❗❗❗❗重要提醒❗❗❗❗❗❗

1. 美的已经关闭国内美居、海外SmartHome等服务器侧Token API服务，目前切换其他NetHome Plus云端Token API后暂时还能继续添加设备，但是应该也会陆续关闭，后续将无法添加新设备。
2. 已经添加成功的设备，请**务必将设备的.json配置文件复制或备份至HAOS之外的其他设备**，供后续使用（通讯协议为v2的旧设备无配置文件，无需备份，仅通讯协议为v3的设备需要备份）
3. 如何获取设备的`.json`配置文件： 请参考[Debug调试和测试](doc/debug_hans.md#%E8%8E%B7%E5%8F%96%E8%AE%BE%E5%A4%87json%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)
4. 关闭原因： 美的设计v1局域网API时，认为客户端通讯已经加密，因此在加密通讯里面使用云端服务生成的token并未设置过期时间。但目前Github存在大量使用破解了客户端加密模式的HA插件，由于Token无法过期，存在安全隐患，因此美的会陆续关闭以上所有云端token API服务，逐步切换至新的v2云端控制API, 从而导致v1局域网控制API无法使用。

## 2. 从[georgezhao2010/midea_ac_lan]迁移

1. 删除旧的集成：[georgezhao2010/midea_ac_lan](https://github.com/georgezhao2010/midea_ac_lan)
2. [安装当前集成](#5-安装), 重启HA
3. 原有的设备不会被删除，应该仍然都存在，因此无需重新Discover搜索和重新添加设备
4. 如果原有设备的实体开关、传感器消失，请通过 `设置 -> 设备与服务 -> Midea AC LAN -> 设备` ，在指定的设备下，点击 `选项`重新启用即可。
5. 完成, 设备仍然像之前一样正常使用即可.

## 3. 已支持的品牌

![beverly](brands/beverly.png) ![bugu](brands/bugu.png) ![carrier](brands/carrier.png) \
![colmo](brands/colmo.png) ![comfee](brands/comfee.png) ![electrolux](brands/electrolux.png) \
![invertor](brands/invertor.png) ![littleswan](brands/littleswan.png) ![midea](brands/midea.png) \
![netsu](brands/netsu.png) ![ProBreeze](brands/probreeze.png) ![rotenso](brands/rotenso.png) \
![toshiba](brands/toshiba.png) ![vandelo](brands/vandelo.png) ![wahin](brands/wahin.png)

以及更多。

## 4. 已支持的设备

请通过以下文档链接查看每种设备支持的功能及使用方法

| 类型 | 名称                        | 文档                         |
| ---- | --------------------------- | ---------------------------- |
| 13   | 灯                          | [13_hans.md](doc/13_hans.md) |
| 26   | 浴霸                        | [26_hans.md](doc/26_hans.md) |
| 34   | 水槽式洗碗机                | [34_hans.md](doc/34_hans.md) |
| 40   | 凉霸                        | [40_hans.md](doc/40_hans.md) |
| A1   | 除湿器                      | [A1_hans.md](doc/A1_hans.md) |
| AC   | 空调器                      | [AC_hans.md](doc/AC_hans.md) |
| AD   | 空气盒子                    | [AD_hans.md](doc/AD_hans.md) |
| B0   | 微波炉                      | [B0_hans.md](doc/B0_hans.md) |
| B1   | 电烤箱                      | [B1_hans.md](doc/B1_hans.md) |
| B3   | 消毒碗柜                    | [B3_hans.md](doc/B3_hans.md) |
| B4   | 小烤箱                      | [B4_hans.md](doc/B4_hans.md) |
| B6   | 油烟机                      | [B6_hans.md](doc/B6_hans.md) |
| BF   | 微蒸烤一体机                | [BF_hans.md](doc/BF_hans.md) |
| C2   | 智能马桶                    | [C2_hans.md](doc/C2_hans.md) |
| C3   | 热泵空调Wi-Fi线控器         | [C3_hans.md](doc/C3_hans.md) |
| CA   | 冰箱                        | [CA_hans.md](doc/CA_hans.md) |
| CC   | 中央空调(风管机)Wi-Fi线控器 | [CC_hans.md](doc/CC_hans.md) |
| CD   | 空气能热水器                | [CD_hans.md](doc/CD_hans.md) |
| CE   | 新风设备                    | [CE_hans.md](doc/CE_hans.md) |
| CF   | 中央空调暖家(水机)          | [CF_hans.md](doc/CF_hans.md) |
| DA   | 波轮洗衣机                  | [DA_hans.md](doc/DA_hans.md) |
| DB   | 滚筒洗衣机                  | [DB_hans.md](doc/DB_hans.md) |
| DC   | 干衣机                      | [DC_hans.md](doc/DC_hans.md) |
| E1   | 洗碗机                      | [E1_hans.md](doc/E1_hans.md) |
| E2   | 电热水器                    | [E2_hans.md](doc/E2_hans.md) |
| E3   | 燃气热水器                  | [E3_hans.md](doc/E3_hans.md) |
| E6   | 壁挂炉                      | [E6_hans.md](doc/E6_hans.md) |
| E8   | 慢炖锅                      | [E8_hans.md](doc/E8_hans.md) |
| EA   | 电饭煲                      | [EA_hans.md](doc/EA_hans.md) |
| EC   | 电压力锅                    | [EC_hans.md](doc/EC_hans.md) |
| ED   | 饮用水设备                  | [ED_hans.md](doc/ED_hans.md) |
| FA   | 电风扇                      | [FA_hans.md](doc/FA_hans.md) |
| FB   | 电取暖器                    | [FB_hans.md](doc/FB_hans.md) |
| FC   | 空气净化器                  | [FC_hans.md](doc/FC_hans.md) |
| FD   | 加湿器                      | [FD_hans.md](doc/FD_hans.md) |

## 5. 安装

请使用以下方式安装:

### 方式1: HACS安装

> 1. 确保`Home Assistant`中已安装HACS [HACS install docs](https://hacs.xyz/docs/setup/download)
> 2. 打开`HACS`, 点击`[Custom repositories]`, `Repository` 输入: `https://github.com/wuwentao/midea_ac_lan`, `Category` 选择 `[Integration]`
> 3. **重启Home Assistant**.

### 方式2: 脚本安装

> 在HomeAssistant的Terminal add-on或者SSH中执行以下脚本

```shell
wget -O - https://github.com/wuwentao/midea_ac_lan/raw/master/scripts/install.sh | ARCHIVE_TAG=latest bash -
```

### 方式3: 手工安装

> 1. 从[Latest Release](https://github.com/wuwentao/midea_ac_lan/releases/latest) 下载 `midea_ac_lan.zip`
> 2. 复制 `midea_ac_lan.zip` 到 `/custom_components/midea_ac_lan`.
> 3. **重启 Home Assistant**.

重启完成后, 打开 `[Settings]`, `[Device & services]`, `[Integrations]`, `[Midea AC Lan]`, 进行初始化设置并添加所有设备.

## 6. 添加设备

**_❗注意: 首先, 在路由器上为你的设备设置一个静态IP地址, 以防设置后设备的IP地址发生改变。_**

安装之后, 在Home Assistant的集成界面搜索添加集成Midea AC LAN, 如果需要添加多台设备, 多次添加本集成并执行自动配置即可。

或者直接点击 [![Configuration](https://my.home-assistant.io/badges/config_flow_start.svg)](https://my.home-assistant.io/redirect/config_flow_start?domain=midea_ac_lan)

**_❗注意: 配置过程中, 可能会要求输入你的美的账号及密码, 这是因为需要去美的云服务器获取设备的信息 (Token and Key)。在完成所有设备配置后, 可以删除美的账户配置, 不影响设备的使用_**

完成美的账户配置之后, 点击'添加设备'进行设备添加。你可以多次重复操作以添加多台设备。

### 6.1 Discover automatically / 自动搜索

使用此选项, 组件会列出网络上或者指定IP地址上的设备, 选择一个并进行添加。

你也可以使用IP地址在指定网络中搜索, 比如`192.168.1.255`

**_❗注意: 自动配置要求设备必须与HA在同一网段, 否则可能搜索不到设备, 请自行确认这点_**

### 6.2 Configure manually / 手动配置

如果之前你已经通过其它集成手工配置过设备, 并知道以下信息, 也可以进行手动配置

- 设备ID
- 设备类型 ([已支持的设备](README_hans.md#%E5%B7%B2%E6%94%AF%E6%8C%81%E7%9A%84%E8%AE%BE%E5%A4%87)之一)
- IP地址
- 端口(默认为6444)
- 协议版本
- Token
- Key

### 6.3 List all appliances only / 仅列出所有设备

使用此选择, 可以列出网络中所有可以被搜索到的美的M-Smart设备, 以及他们的ID, 类型, SN等信息

**_❗注意: 出于某些原因, 可能不是所有受支持的设备都能于此列出_**

## 7. 配置

集成配置位于 `设置 -> 设备与服务 -> Midea AC LAN -> 设备` 在指定的设备下，点击 `选项`。
在配置中, 你可以在设备IP改变后重新指定IP地址, 也可以增加扩展的传感器或开关等实体或者自定义你的设备

### 7.1 IP地址

指定设备的IP地址。当你的设备IP地址变动后, 可以重新设定它

### 7.2 刷新间隔

指定单台设备的主动状态刷新间隔 (单位为秒) (默认值为30, 设0代表不进行主动刷新)

大部分的美的设备在自身状态改变时会主动发送通知, 在这种情况下, 即使将改值设为0, 也不会影响HA中的设备状态更新。组件默认每间隔30秒会进行主动刷新。部分设备没有状态改变时主动通知的机制, 状态同步就会表现得很慢, 这种情况下可以尝试更短的主动状态更新间隔。

**_❗注意: 更小的更新间隔意味着更多的能源消耗_**

## 7.3 额外的传感器及开关实体

配置完成后, 可能会默认生成一个或几个主要实体(比如climate实体)。如果需要其它属性生成为扩展的传感器及开关实体, 在Midea AC LAN集成卡片上点击`选项`, 并选择要生成的传感器及开关(设备必须支持该功能)。

### 7.4 自定义

某些类型的设备有它们自己的自定义项, 可以通过自定义项定制设备的特点。如果你的设备无法正常工作, 也许你需要自定义它。请参阅设备文档以获取具体信息。

自定义Customize的格式必须是JSON。

如果要设置多个自定义项, 请注意遵循JSON的格式要求

示例

```json
{ "refresh_interval": 15, "fan_speed": 100 }
```

## 8. Debug调试和测试

请参考[Debug调试和测试](doc/debug_hans.md)
