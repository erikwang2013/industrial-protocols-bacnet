# BACnet/IP 协议包 — 支持 Who-Is/I-Am 设备发现和 ReadProperty，UDP 通信

> [中文](README.md)

BACnet/IP 协议包 — 支持 Who-Is/I-Am 设备发现和 ReadProperty，UDP 通信。Pure PHP implementation, compatible with 6 PHP runtimes via kernel framework adapters.

## Installation

```bash
composer require erikwang2013/industrial-protocols-kernel erikwang2013/industrial-protocols-bacnet
```

> Depends on [erikwang2013/industrial-protocols-kernel](https://github.com/erikwang2013/industrial-protocols-kernel) for connection management, protocol registry, coroutine adaptation, event system and more.

## Architecture

Built on kernel SDK interfaces (ProtocolInterface/ConnectorInterface/DriverInterface/FrameInterface), with BacnetDriver for transport and BacnetConnector for unified ConnectorInterface.

## Features

Complete bacnet protocol frame encode/decode, driver transport, Connector wrapper, health check, connection strategies (Lazy/Eager/Pooled)

## Supported Frameworks

Compatible with 7 PHP runtimes via kernel framework adapters: Laravel (ServiceProvider+Facade+artisan), Webman (config/plugin auto-discovery+ProtocolProcess), Hyperf (ConfigProvider+DI+KernelFactory), ThinkPHP (services.php+IndustrialProtocolsService), Yii2 (Bootstrap+component), Yii3 (DI container+KernelFactory), Plain PHP (direct Kernel instantiation)

### Laravel

```php
// AppServiceProvider::boot()
$kernel = app(Kernel::class);
$kernel->getProtocolRegistry()->register(new ModbusProtocol());
$kernel->boot();
$conn = $kernel->getConnectionManager()->connect('device-id');
```

### Webman

Auto-boot via ProtocolProcess on worker start. Configure at `config/plugin/erikwang2013/industrial-protocols-kernel/config/industrial-protocols.php`.

### Hyperf

```php
$kernel = \Hyperf\Context\ApplicationContext::getContainer()->get(Kernel::class);
```

## Usage

```php
$conn = $kernel->getConnectionManager()->connect('bacnet-device');
$devices = $conn->discoverDevices(5);       // Who-Is broadcast
$result  = $conn->read('0:1:85');           // ObjectType:Instance:PropertyId
```

## Configuration

```php
'devices' => [
    'device-id' => [
        'protocol' => 'bacnet',
        'host'     => '192.168.1.10',
        'port'     => 47808,
        'timeout'  => 3000,
    ],
],
```

## Adapter Vendors

Hilscher (netX), HMS/Anybus (BACnet Gateway), Moxa (MGate 5217 BACnet Gateway)

## Requirements

- PHP >= 8.1
- Composer
- erikwang2013/industrial-protocols-kernel

## Related Links

- [Industrial Protocols Main Project](https://github.com/erikwang2013/industrial-protocols)
- [Kernel](https://github.com/erikwang2013/industrial-protocols-kernel)
- [All 42 Protocol Packages](https://github.com/erikwang2013/industrial-protocols#supported-protocols)

## License

MIT — Copyright (c) 2026 erik <erik@erik.xyz> — https://erik.xyz
