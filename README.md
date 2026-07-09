# LC307

UPIXELS LC307 UART optical flow sensor module for XRobot.

This module binds to the LC307 UART stream, optionally configures the sensor at
boot, parses optical-flow frames in a background thread, publishes flow and
distance samples, and exposes a RamFS shell command for status output.

The UART name is a constructor argument, so projects may use other hardware
aliases if needed.

## Required Hardware

- `lc307_uart`
- `ramfs`

## Constructor Arguments

- `topic_name`: default `"lc307_flow"`
- `task_stack_depth`: default `2048`
- `uart_name`: default `"lc307_uart"`
- `configure_on_boot`: default `true`
- `init_timeout_ms`: default `1500`
- `frame_timeout_ms`: default `200`

## Published Topics

- `topic_name`: `LC307::Sample`, including raw flow, 1 m normalized flow velocity, integration time, distance, quality, and version

## Shell Commands

The module registers `bin/lc307` in `RamFS`.

- `bin/lc307` or `bin/lc307 status`: print frame counters, flow, distance, quality, and version

## XRobot Configuration Example

```yaml
- id: flow
  name: LC307
  constructor_args:
    topic_name: "lc307_flow"
    task_stack_depth: 2048
    uart_name: "lc307_uart"
    configure_on_boot: true
    init_timeout_ms: 1500
    frame_timeout_ms: 200
```
