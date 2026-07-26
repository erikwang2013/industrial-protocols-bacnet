# BACnet/IP 协议包 — 支持 Who-Is/I-Am 设备发现和 ReadProperty，UDP 通信

> [English](README.en.md)

BACnet 楼宇自动化协议，UDP 通信，端口 47808。支持 Who-Is/I-Am 设备自动发现和 ReadProperty 读取对象属性。

## 安装

```bash
composer require erikwang2013/industrial-protocols-bacnet
```

## 架构

BacnetDriver（UDP）发送 BACnet 帧，BacnetFrame 实现 FrameInterface，支持 Who-Is、I-Am、ReadProperty/WriteProperty 帧类型。

## 功能

Who-Is/I-Am 设备自动发现、ReadProperty 读取对象属性（AnalogInput/BinaryInput 等）、默认 PresentValue 属性（85）、BACnet 帧编解码、UDP 通信驱动

## 使用说明

```php
$conn = $kernel->getConnectionManager()->connect('bacnet-device');
$devices = $conn->discoverDevices(5);   // Who-Is 广播
$result = $conn->read('0:1:85');       // AnalogInput 1, PresentValue
```

## 配置示例

```php
'devices' => [
    'bacnet-device' => [
        'protocol' => 'bacnet', 'variant' => 'ip',
        'host' => '192.168.1.50', 'port' => 47808,
        'device_id' => 1234, 'timeout' => 3000,
    ],
],
```

## 兼容框架

Laravel / Webman / Hyperf / ThinkPHP / Yii2 / Plain PHP

## 系统要求

- PHP >= 8.1
- Composer
- erikwang2013/industrial-protocols-kernel

## License

MIT — Copyright (c) 2026 erik <erik@erik.xyz> — https://erik.xyz
