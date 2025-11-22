

https://grafana.com/docs/k6/latest/testing-guides/test-types/

---

Many things can go wrong when a system is under load. 

The system must run numerous operations simultaneously and respond to different requests from a variable number of users. 

To prepare for these performance risks, teams use load testing.

But a good load-testing strategy requires more than just executing a single script.

Different patterns of traffic create different risk profiles for the application. 

For comprehensive preparation, teams must test the system against different _test types_.


![[Pasted image 20250708123432.png]]

---

# Different tests for different goals

Start with ==smoke tests==, then ==progress== to ==higher loads and longer durations==.

- [**Smoke tests**](https://grafana.com/docs/k6/latest/testing-guides/test-types/smoke-testing/) validate that your script works and that the system performs adequately بشكل مناسب under minimal load.

- [**Average-load test**](https://grafana.com/docs/k6/latest/testing-guides/test-types/load-testing/) assess يٌقيِّم how your system performs under **expected normal conditions**.

- [**Stress tests**](https://grafana.com/docs/k6/latest/testing-guides/test-types/stress-testing/) assess how a system performs at its limits when **load exceeds the expected average**.

- [**Soak نقع tests**](https://grafana.com/docs/k6/latest/testing-guides/test-types/soak-testing/) assess the reliability مصداقية and performance of your system **over extended periods**.

- [**Spike مسمار tests**](https://grafana.com/docs/k6/latest/testing-guides/test-types/spike-testing/) validate the behavior and survival of your system in cases of **sudden**, **short**, and **massive increases** **==in activity==**.

- [**Breakpoint tests**](https://grafana.com/docs/k6/latest/testing-guides/test-types/breakpoint-testing/) gradually تدريجياً increase load **to identify the capacity limits of the system**.

Some systems are more at risk of longer use, in which case soaks should be prioritized.

Others are more at risk of intensive use, in which case stress tests should take precedence.

In any case, **no single test can uncover all issues**.

**Stick to**
>Stick to simple load patterns. 
For all test types, directions is enough: ramp-up, plateau هضبة, ramp-down.

**Avoid**
>Avoid “roller-coaster” series where load increases and decreases multiple times. These will waste resources and make it hard to isolate issues.

---

# Test-type cheat sheet

| Type                                                                                           | VUs/Throughput        | Duration                   | When?                                                                                                              |
| ---------------------------------------------------------------------------------------------- | --------------------- | -------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| [Smoke](https://grafana.com/docs/k6/latest/testing-guides/test-types/smoke-testing/)           | Low                   | Short (seconds or minutes) | When the relevant system or application code changes. It checks functional logic, baseline metrics, and deviations |
| [Load](https://grafana.com/docs/k6/latest/testing-guides/test-types/load-testing/)             | Average production    | Mid (5-60 minutes)         | Often to check system maintains performance with average use                                                       |
| [Stress](https://grafana.com/docs/k6/latest/testing-guides/test-types/stress-testing/)         | High (above average)  | Mid (5-60 minutes)         | When system may receive above-average loads to check how it manages                                                |
| [Soak](https://grafana.com/docs/k6/latest/testing-guides/test-types/soak-testing/)             | Average               | Long (hours)               | After changes to check system under prolonged continuous use                                                       |
| [Spike](https://grafana.com/docs/k6/latest/testing-guides/test-types/spike-testing/)           | Very high             | Short (a few minutes)      | When the system prepares for seasonal events or receives frequent traffic peaks                                    |
| [Breakpoint](https://grafana.com/docs/k6/latest/testing-guides/test-types/breakpoint-testing/) | Increases until break | As long as necessary       | A few times to find the upper limits of the system                                                                 |