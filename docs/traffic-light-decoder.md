# Traffic Light Planning


First we need to write all the possible traffic light loop possible


![FSM](assets/SimpleTrafficLightFSM.png)

Inner Circle means it sets T = 1 
### Traffic Light Loop
| State | Next State | $M_r$  | $S_r$  | Pedestrian_Cross? |
| ----- | ---------- | ------ | ------ | ----------------- |
| 00    | 01         | Green  | Red    | No!               |
| 01    | 10         | Yellow | Red    | No!               |
| 10    | 11         | Red    | Green  | No!               |
| 11    | 00         | Red    | Yellow | No!               |

### Traffic Light Loop with T
| State | Next State | $M_r$  | $S_r$  | Pedestrian_Cross? |
| ----- | ---------- | ------ | ------ | ----------------- |
| 0     | 1          | Green  | Red    | No!               |
| 0     | 1          | Green  | Red    | No!               |
| 1     | 2          | Yellow | Red    | No!               |
| 2     | 3          | Red    | Green  | No!               |
| 3     | 4          | Red    | Yellow | No!               |

### Traffic Light Loop
| State | Next State | $M_r$         | $S_r$         | Pedestrian_Cross? |
| ----- | ---------- | ------------- | ------------- | ----------------- |
| 0     | 1          | Green         | Red           | No!               |
| 1     | 2          | Yellow        | Red           | No!               |
| 2     | {3, 7, 9}  | Red           | Red           | No!               |
| 3     | 4          | Red           | {Red, Yellow} | No!               |
| 4     | 5          | Red           | Green         | No!               |
| 5     | 6          | Red           | Yellow        | No!               |
| 6     | {7, 9, 3}  | Red           | Red           | No!               |
| 7     | 8          | Red           | Red           | Yes!              |
| 8     | {9, 3, 7}  | Red           | Red           | No!               |
| 9     | 0          | {Red, Yellow} | Red           | No!               |

> **Note**: If _Next State_ has multiple states, It has an order and is dependant if it needs to do it.

### Traffic Light Loop (Variation 2)
| State | Next State | $M_r$         | $S_r$         | Pedestrian_Cross? |
| ----- | ---------- | ------------- | ------------- | ----------------- |
| 0     | 1          | Green         | Red           | No!               |
| 1     | 2          | Yellow        | Red           | No!               |
| 2     | {3, 6}     | Red           | Red           | No!               |
| 3     | 4          | Red           | {Red, Yellow} | No!               |
| 4     | 5          | Red           | Green         | No!               |
| 5     | 6          | Red           | Yellow        | No!               |
| 6     | {7, 8}     | Red           | Red           | No!               |
| 7     | 8          | Red           | Red           | Yes!              |
| 8     | {9, 2}     | Red           | Red           | No!               |
| 9     | 0          | {Red, Yellow} | Red           | No!               |













### Trafic Light Loop (Variation 2) 
| State | Handle_This_State? | Next State | $M_r$         | $S_r$         | Pedestrian_Cross? |
| ----- | ------------------ | ---------- | ------------- | ------------- | ----------------- |
| 0     | -                  | 1          | Green         | Red           | No!               |
| 1     | -                  | 2          | Yellow        | Red           | No!               |
| 2     | True               | 3          | Red           | Red           | No!               |
| 2     | False              | 6          | Red           | Red           | No!               |
| 3     | -                  | 4          | Red           | {Red, Yellow} | No!               |
| 4     | -                  | 5          | Red           | Green         | No!               |
| 5     | -                  | 6          | Red           | Yellow        | No!               |
| 6     | True               | 7          | Red           | Red           | No!               |
| 6     | False              | 8          | Red           | Red           | No!               |
| 7     | -                  | 8          | Red           | Red           | Yes!              |
| 8     | True               | 9          | Red           | Red           | No!               |
| 8     | False              | 2          | Red           | Red           | No!               |
| 9     |                    | 0          | {Red, Yellow} | Red           | No!               |




















### Traffic Light Loop (Variation 2) Green filter
| State | Next State | $M_r$                       | $S_r$                       | Pedestrian_Cross? |
| ----- | ---------- | --------------------------- | --------------------------- | ----------------- |
| 0     | 1          | Green                       | Red                         | No!               |
| 1     | 2          | Yellow                      | Red                         | No!               |
| 2     | {3, 6}     | Red                         | Red                         | No!               |
| 3     | 4          | Red                         | {Red, Green_filter}         | No!               |
| 4     | 5          | Red                         | {Red, Yellow, Green_filter} | No!               |
| 5     | 6          | Red                         | Green                       | No!               |
| 6     | 7          | Red                         | Yellow                      | No!               |
| 7     | {8, 9}     | Red                         | Red                         | No!               |
| 8     | 9          | Red                         | Red                         | Yes!              |
| 9     | {10, 3}    | Red                         | Red                         | No!               |
| 10    | 11         | {Red, Green_filter}         | Red                         | No!               |
| 11    | 1          | {Red, Yellow, Green_filter} | Red                         | No!               |

























##### Global Flags (variables):
* ${Car}_M$ - If there is a car presence on $M_r$
* ${Car}_S$ - If there is a car presence on $S_r$
* $P_b$ - If there is a Pedestrian Button Pressed.

