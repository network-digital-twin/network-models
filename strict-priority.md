# Strict Priority / Priority Queuing

SP (Strict Priority) / Priority Queuing (PQ) handles packets strictly following the descending order of the priority values of QoS queues.

## Overview

According to [Cisco](https://www.cisco.com/assets/sol/sb/Switches_Emulators_v2_2_015/help/nk_configuring_quality_service16.html), in SP, "traffic from the lower queues is processed only after the highest queue is transmitted, thus providing the highest level of priority of traffic to the highest queue number". 

- Normally, packets are classified into **4** queues - high, medium, normal and low.
- Packets in the same QoS queue are scanned in FIFO manner.

![sp](http://what-when-how.com/wp-content/uploads/2012/02/tmpC115_thumb2_thumb.jpg)

### Reference

- Cisco: 
  - https://www.cisco.com/assets/sol/sb/Switches_Emulators_v2_2_015/help/nk_configuring_quality_service16.html
  - https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/qos_conmgt/configuration/xe-3s/qos-conmgt-xe-3s-book/qos-conmgt-oview.html#GUID-58E4F027-85B1-471F-8CF2-B5F54D176821
- http://what-when-how.com/qos-enabled-networks/queuing-and-scheduling-qos-enabled-networks-part-2/

## Pseudocode

```pseudocode
Parameters:
  1. List of packets X = [x0, x1, ...].
  2. Set of QoS queues Q = {q0, q1, ...}, where q = {priority p, buffer size s}.
  3. Classifier C: x -> q to map packets to QoS queues.
  4. Output packet x* for transmission.

def sp_enqueue(Q, C, x):
  q = C(x)
  if q.s is enough to hold x:
    q.push(x)

def sp_dequeue(Q) -> x*:
  Q' = sort Q by descending q.p
  for q' in Q':
    if q' is not empty:
      x* = q'.poll()
      return x*
  return null
```
