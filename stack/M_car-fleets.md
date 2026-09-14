```python
class Solution:
    def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        cars = [(position[i], speed[i]) for i in range(0, len(position))]
        cars.sort(reverse=True)

        ## [(10,2), (8,4), (5,1), (3,3), (0,1)]

        fleets = 0
        curr_lead_time = 0

        for (curr_pos, curr_speed) in cars:
            time_taken = (target - curr_pos) / (curr_speed)
            if time_taken > curr_lead_time:
                curr_lead_time = time_taken
                
                # this car at a farther position from target than the curr_lead_time car, will never reach target at the same time as the curr_lead_time car, nor will it catch up with it.

                # that is why this car is treated as its own fleet. 
                fleets += 1           
            else:
                continue
                # this car will eventually merge with the curr_lead_time car, becoming one fleet. 
                # thus no need to do anything

        return fleets
```

## NOTE:

- Need to revisit this tricky problem --> step through the logic more clealry + how is this related to stack?