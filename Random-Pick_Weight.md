# Random-Pick_Weight

- Positive integers : So higher val - > More probablity but rathes than foucsing on discrete probability floating point values , let solve it another way
- Since the prob are dervied out of totalSum of all values  .
- Imaging it as a scale of positive values **[1,total]** , now divide the section of this range differnet index having diff w[i]
- why ? because in lets's say dart games if the board if divided as 1/6 {red} , 2/6 {blue} , 3/6 {yellow} than probality of getting yellow is more  ,
- With this intuition we take up the prefix sum upto any index , then the randomNum generated upto the totalSum (highestnum that can be takes as prob <= 1) , just check in what range does it belongs ?
- Each prefix[i] represents the right edge of the segment for index i

 ```cpp
  class Solution {
  public:
      vector<int> prefix;
      int total ;

    Solution(vector<int>& w) {
        total  = 0 ;
        prefix.resize(w.size());
        for (int i = 0; i < w.size(); i++) {
            total += w[i] ;
            if (i == 0 ) prefix[i] = w[0] ;
            else {
                prefix[i] = prefix[i-1] + w[i] ;
            }
        }
    }

    int pickIndex() {
        int target = rand() % total;
        return lower_bound(prefix.begin(), prefix.end(), target + 1) - prefix.begin();
    }
   };

  ```

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N + k*logN)    | O(N) for prefix  , O(k*logn) is for Binary Search          |
| 🧠 SPACE |   O(N)       | Prefix Sum stored |

  
