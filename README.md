# Multimodal Feedback Schema (MFS)

**一种通用的多模态触觉与声光交互描述语言**

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Version](https://img.shields.io/badge/version-v0.2-blue)](https://github.com/your-username/multimodal-feedback-schema/releases)
[![Status](https://img.shields.io/badge/status-draft-orange)](https://github.com/your-username/multimodal-feedback-schema)

---

## 项目更名对比说明 (Name Transition Reference)

为了将协议从单一的触觉反馈拓宽至声音、视频、动作、文字、表情、情绪、空间、位置的全模态联合调度，本项目已正式完成架构升级。以下为新旧名称及内涵对照：

| 维度 | 原名称 / 简称 (Legacy) | 新名称 / 简称 (Current) | 升级核心内涵 |
| :--- | :--- | :--- | :--- |
| **项目名称** | Haptic Event Schema (HES) | **Multimodal Feedback Schema (MFS)** | 从单一触觉事件泛化为多模态综合反馈方案 |
| **描述核心** | 硬件无关的触觉波形语义化标签 | **多物理触点 + 屏幕边缘彩带 + 闪光灯情绪联动** | 视、听、触、光多维物理线索微秒级协同 |

---

## 为什么需要 MFS？
Multimodal Feedback Schema (MFS)：下一代跨平台多模态交互描述协议
MFS 是一套轻量级、机器可读的开源标准，旨在解决多模态交互中的“感官语义断层”问题。它将音视频节奏、文本情感倾向、面部微表情、空间三维导航等数字内容，转化为标准化的物理反馈事件指令。通过解耦“内容生成”与“设备执行”，MFS 为开发者提供了一套统一的跨平台（iOS/Android/Web）多模态渲染 API，让沉浸式反馈的开发效率提升数倍。

今天的触觉与物理反馈开发，

- 为 iPhone 写一套 CoreHaptics 代码
- 为华为写一套 VibrationEffect 代码
- 为屏幕边缘动效写一套 Canvas 图层动画
- 为调用闪光灯写一套硬件控制逻辑……
- 换一款设备，全部重调

**问题是：我们到底在描述底层“怎么驱动”，还是在描述“让用户感受和看到什么”？**

MFS 选择后者。

它定义了一套 **硬件无关的多模态词汇** 和 **通用脚本格式**，让开发者只需要说：

> “这里需要一个‘空间接近且伴随情绪焦虑’”

由底层渲染器自动翻译成 iPhone、Android 各自能理解的四角多点马达顺次震动、屏幕边缘彩带控速流转、以及闪光灯 LED 动态频闪指令。

---

## 核心内容

### 1. 交互世界观（5 大维度与多模态逻辑）

MFS 严格基于内容映射，并遵循五维优先级铁律：**情绪(Emotion) > 运动(Motion) > 力量(Force) > 空间(Space) > 节奏(Rhythm)**。

| 维度 | 说明 | 联动与逻辑演进 (v0.2 新增) |
| :--- | :--- | :--- |
| **力量感 (Force)** | 物理撞击、按键确认的重量与锐度 | 映射瞬态能量突变，提供清脆的物理确认感或爆发感。 |
| **节奏感 (Rhythm)** | 反馈信号的时间排列与生物节律 | 模拟心跳、脉冲，直接关联生物心率及节奏型音效。 |
| **空间感 (Space)** | 物理方位、距离移动与多触点轨迹 | **支持手机左下、右下、左上、右上分别独立震动；实现从上到下、从左到右、从右到左、从下到上的四向定向位移传导，以及沿边缘的线性持续环绕震动。** |
| **运动感 (Motion)** | 物理惯性与屏幕边缘视觉流转 | **联动屏幕边缘彩带环绕转动特效。彩带根据运动速度划分为 4 个分级（Levels 1–4），并支持顺时针/逆时针双向编码控制。** |
| **情绪感 (Emotion)** | 生理心理微反应与外设光影联动 | **联动手机外设闪光灯。闪光灯根据底层文本/表情的情绪严重程度（0.0–1.0）自适应调整闪烁频率（1Hz–20Hz）与亮度。** |

---

### 2. 标准反馈词典（核心 40 个词条示例）

> *注：为了保证协议演进的一致性，标准公开编码均从 101 开始。*

| 编号 | 标准名 | 中文名 | 类型 | 多模态及多触点声光联动细节说明 (v0.2 扩充) |
| :--- | :--- | :--- | :--- | :--- |
| F-101 | Tap.Light | 轻触 | Force | 极短促方波，用于 UI 勾选、按键确认；LED 关闭 |
| F-104 | Shock.Burst | 爆发 | Force | 视频爆炸或情绪破防；LED 瞬时满载强闪 |
| R-104 | Rhythm.Heartbeat| 心跳 | Rhythm | 强弱交替的咚哒模式，直接关联紧张、恐惧等生物数据 |
| M-303 | Motion.Accel | 加速 | Motion | 反馈间隔递减；**屏幕边缘彩带环绕速度等级从 1 级向 4 级跃升** |
| E-401 | Emotion.Tension | 紧张 | Emotion | 映射焦虑表情；**闪光灯执行 8Hz 不规则低亮紧迫频闪** |
| E-402 | Emotion.Oppress | 压迫 | Emotion | 映射愤怒文本；**闪光灯执行 2Hz 低频高亮持续压迫闪烁** |
| **S-207** | **Space.LocBL** | **左下偏置** | **Space** | **精准驱动手机左下角马达独立起振；彩带定位左下闪烁** |
| **S-208** | **Space.LocBR** | **右下偏置** | **Space** | **精准驱动手机右下角马达独立起振；彩带定位右下闪烁** |
| **S-211** | **Space.FlowT2B** | **纵向下传** | **Space** | **触点依序激发：[左上+右上] → [左下+右下]；彩带自上而下滚动** |
| **S-212** | **Space.FlowL2R** | **横向右传** | **Space** | **触点依序激发：[左上+左下] → [右上+右下]；彩带自左向右滚动** |
| **S-215** | **Space.EdgeOrbit**| **边缘线绕** | **Space** | **四象限马达执行线性持续环绕震动；彩带同步沿边缘顺时针旋转** |
| **E-407** | **Emotion.FlashLnk**| **情绪闪光** | **Emotion** | **闪光灯闪烁频率根据情绪强弱系数动态在 1Hz–20Hz 之间线性映射** |

> 完整词典请查阅 [Multimodal Feedback Schema 完整技术规范白皮书](multimodal-feedback-schema.md)

---

### 3. 触觉与声光多轨脚本格式 (HSF)

HSF（Haptic Script Format）是 MFS 的时间线表达格式。在 v0.2 版本中，HSF 具备了**高阶多轨空间分发与多模态扩展性**，支持针对独立物理马达、边缘彩带与闪光灯进行分轨控制：

```json
{
  "schema": "HapticScriptFormat",
  "version": "0.2",
  "meta": {
    "title": "多模态多触点联动示例",
    "duration_ms": 45000,
    "multimodal_source": {
      "audio_track_ref": "action_theme.mp3",
      "video_track_ref": "chase_scene.mp4"
    }
  },
  "tracks": [
    {
      "id": "spatial_vibration_track",
      "device_target": "phone_multi_motor",
      "events": [
        {
          "time_ms": 15000,
          "duration_ms": 600,
          "event_ref": "S-215",
          "intensity": 0.8,
          "note": "手机执行物理边缘线性持续环绕震动（左下->左上->右上->右下）"
        }
      ]
    },
    {
      "id": "screen_ribbon_track",
      "device_target": "phone_screen_edge",
      "events": [
        {
          "time_ms": 15000,
          "duration_ms": 600,
          "event_ref": "S-215",
          "ribbon_parameters": {
            "direction": "clockwise",
            "speed_level": 3,
            "color_hex": "#FF5500"
          },
          "note": "视觉联动：彩带以 3 级速度顺时针沿屏幕边缘转动"
        }
      ]
    },
    {
      "id": "flashlight_led_track",
      "device_target": "rear_flash_led",
      "events": [
        {
          "time_ms": 16200,
          "duration_ms": 1000,
          "event_ref": "E-407",
          "led_parameters": {
            "emotion_severity": 0.80,
            "computed_frequency_hz": 16.0
          },
          "note": "情绪光影联动：画面转入极度愤怒，闪光灯以 16Hz 高频爆闪"
        }
      ]
    }
  ]
}
