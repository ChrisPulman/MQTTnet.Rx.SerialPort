![License](https://img.shields.io/github/license/ChrisPulman/MQTTnet.Rx.SerialPort.svg) [![Build](https://github.com/ChrisPulman/MQTTnet.Rx.SerialPort/actions/workflows/BuildOnly.yml/badge.svg)](https://github.com/ChrisPulman/MQTTnet.Rx.SerialPort/actions/workflows/BuildOnly.yml) ![Nuget](https://img.shields.io/nuget/dt/MQTTnet.Rx.SerialPort?color=pink&style=plastic) [![NuGet](https://img.shields.io/nuget/v/MQTTnet.Rx.SerialPort.svg?style=plastic)](https://www.nuget.org/packages/MQTTnet.Rx.SerialPort)

<p align="left">
  <a href="https://github.com/ChrisPulman/MQTTnet.Rx.SerialPort">
    <img alt="MQTTnet.Rx.SerialPort" src="https://github.com/ChrisPulman/MQTTnet.Rx.SerialPort/blob/main/Images/logo.png" width="200"/>
  </a>
</p>


# MQTTnet.Rx.SerialPort
A Reactive SerialPort for MQTTnet Broker

## Create a Mqtt Client to Publish data from an Observable SerialPort
```csharp
Create.MqttClient()
    .WithClientOptions(a => a.WithTcpServer("localhost", 9000))
    .PublishMessage(_message)
    .Subscribe(r => Console.WriteLine($"{r.ReasonCode} [{r.PacketIdentifier}]"));
```

## Create a Managed Mqtt Client to Publish data from an Observable SerialPort Subscribe
```csharp
Create.ManagedMqttClient()
    .WithManagedClientOptions(a =>
        a.WithAutoReconnectDelay(TimeSpan.FromSeconds(5))
            .WithClientOptions(c =>
                c.WithTcpServer("localhost", 9000)))
    .PublishMessage(_message)
    .Subscribe(r => Console.WriteLine($"{r.ApplicationMessage.Id} [{r.ApplicationMessage.ApplicationMessage.Topic}] value : {r.ApplicationMessage.ApplicationMessage.ConvertPayloadToString()}"));
```

## Create a Mqtt Client Subscribe to a Topic that will interact with the SerialPort
```csharp
Create.MqttClient()
    .WithClientOptions(a => a.WithTcpServer("localhost", 9000))
    .SubscribeToTopic("FromMilliseconds")
    .Subscribe(r => Console.WriteLine($"{r.ReasonCode} [{r.ApplicationMessage.Topic}] value : {r.ApplicationMessage.ConvertPayloadToString()}"));
```

## Create a Managed Mqtt Client to Subscribe to a Topic that will interact with the SerialPort
```csharp
Create.ManagedMqttClient()
    .WithManagedClientOptions(a =>
        a.WithAutoReconnectDelay(TimeSpan.FromSeconds(5))
            .WithClientOptions(c =>
                c.WithTcpServer("localhost", 9000)))
    .SubscribeToTopic("FromMilliseconds")
    .Subscribe(r => Console.WriteLine($"{r.ReasonCode} [{r.ApplicationMessage.Topic}] value : {r.ApplicationMessage.ConvertPayloadToString()}"));
```