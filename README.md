# Minimum-Time-Difference

Given a list of 24-hour clock time points in "HH:MM" format, return the minimum minutes difference between any two time-points in the list.
Constraints:

2 <= timePoints.length <= 2 * 10^4
timePoints[i] is in the format "HH:MM".

class Solution:
    def findMinDifference(self, timePoints: List[str]) -> int:
        def timeToMinutes(time: str) -> int:
            hours, minutes = map(int, time.split(':'))
            return hours * 60 + minutes
        
        minutes = [timeToMinutes(tp) for tp in timePoints]
        
        minutes.sort()
        
        min_diff = float('inf')  # Initialize to a large number
        for i in range(1, len(minutes)):
            min_diff = min(min_diff, minutes[i] - minutes[i - 1])
            circular_diff = 1440 - minutes[-1] + minutes[0]
        min_diff = min(min_diff, circular_diff)
        
        return min_diff
