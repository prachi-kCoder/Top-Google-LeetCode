# MIN-TIME-DIFF 
```cpp
class Solution {
public:
    int get_time(const string& s) {
        int h = 0 ;
        if (s[0] != '0') {
            h =  (s[0]-'0');
        }
        h = h*10 + (s[1]-'0');
        
        int mn = 0 ;
        if (s[3] != '0') {
            mn = (s[3]-'0');
        }
        mn = mn*10 + (s[4]-'0');
        
        return h*60 + mn ;
    }

    int findMinDifference(vector<string>& timePoints) {
        int n = timePoints.size();
        vector<int> minutes;

        for (const string& time : timePoints)
            minutes.push_back(get_time(time));

        sort(minutes.begin(), minutes.end());

        int min_diff = INT_MAX;
        for (int i = 1; i < n; ++i)
            min_diff = min(min_diff, minutes[i] - minutes[i - 1]);

        // Circular difference between last and first time
        min_diff = min(min_diff, 1440 - (minutes[n - 1] - minutes[0]));

        return min_diff;
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |   O(NLOGN)     |  sorting n timepoints        |
| 🧠 SPACE |    O(N)        | Mins array            |
