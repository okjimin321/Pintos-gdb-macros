# Pintos GDB Macros
> Tools for Efficient Kernel Debugging in Pintos

<img src="./Pintos로_배우는_운영체제_구조와_원리_표지.png" width="400"/>

## Overview
Pintos는 커널 레벨에서 동작하기 때문에 일반적인 printf 기반 디버깅만으로는  
thread 상태나 스케줄링 흐름을 파악하기 어렵습니다.

본 프로젝트는 Pintos 교재를 집필하는 과정에서  
**커널 디버깅의 한계를 개선하기 위해 GDB Macros를 직접 설계하고 교재에 통합한 결과물**입니다.

---

## Motivation
Pintos 프로젝트를 진행하며 다음과 같은 어려움을 겪었습니다:

- 현재 실행 중인 thread 상태를 확인하기 어려움
- ready / blocked queue를 직접 추적해야 하는 번거로움
- context switching 흐름을 파악하기 어려움

이를 해결하기 위해 반복적인 디버깅 작업을 추상화한  
GDB 매크로를 설계했습니다.

---

## Features

### Thread State Inspection
- `p_ready`  
  → Ready queue에 있는 모든 thread 출력

- `p_blocked`  
  → Blocked 상태의 thread 출력

- `p_all`  
  → 모든 thread 출력 (상태 무관)

- `p_run`  
  → 현재 실행 중인 thread 출력

---

### Debugging Automation
- `connect`  
  → `target remote localhost:1234`를 간단하게 실행

- `trace_run $arg0`  
  → 특정 지점에서 execution이 멈출 때마다  
    현재 running thread를 출력하고 자동으로 계속 실행

---

## Example Usage

```bash
(gdb) connect
(gdb) p_ready
(gdb) p_run
