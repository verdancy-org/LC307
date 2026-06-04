# LC307

LC307 光流模块的 LibXR 封装，参考 `xrobot-org/BMI088` 的模块形态实现：

- 构造时绑定硬件并注册应用
- 启动后台线程解析 UART 数据流
- 发布光流 Topic
- 在 `ramfs/bin/lc307` 暴露状态命令

## Required Hardware

- `usart3` 或等价别名
- `ramfs`

## Constructor Arguments

- `topic_name`
- `task_stack_depth`
- `uart_name`
- `configure_on_boot`
- `init_timeout_ms`
- `frame_timeout_ms`

## Published Topic

`topic_name` 的 payload 为 `LC307::Sample`，包含：
- 原始 `flow_x_raw` / `flow_y_raw`
- 以 1m 高度换算的 `flow_x_at_1m_mps` / `flow_y_at_1m_mps`
- `integration_time`
- `distance_mm` / `distance_m`
- `quality`
- `version`
