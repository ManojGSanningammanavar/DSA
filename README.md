# DSA
question 88 (merge sorted array)
class Solution {
public:
    void merge(vector<int>& a, int m, vector<int>& b, int n) {
        int idx = m+n-1;
        int i = m-1;
        int j = n-1;
        while(i>=0 && j>=0){
            if(a[i]>=b[j]){
                a[idx--] = a[i--];
            }
            else{
                a[idx--]=b[j--];
            }
        }
        while(j>=0){
            a[idx--]=b[j--];
        }

    }
};


que - 75 (0's,1's,2's)

class Solution {
public:
    void sortColors(vector<int>& nums) {
        int n= nums.size();
        int low = 0, mid = 0 , high = n-1;
        while (mid <=high){
            if(nums[mid]== 0){
                swap(nums[low], nums[mid]);
                mid++;
                low++;

            }
            else if(nums[mid]==1){
                mid++;
            }
            else{
                swap(nums[high], nums[mid]);
                high--;
            }

        }
    }
};


//QUESTION 540. (Single Element in a Sorted Array)
/*
class Solution {
public:
    int singleNonDuplicate(vector<int>& a) {
        int n = a.size();
        if(n==1) return a[0];
        int st =0, end = n-1;
        while(st<= end){
            int mid = st + (end-st )/2;
            if(mid ==0 && a[0]!=a[1]) {
                return a[mid];
            }
            if(mid ==n-1 && a[n-1]!=a[n-2]) {
                return a[mid];
            }
            if(a[mid-1] != a[mid] && a[mid]!=a[mid+1]){
                return a[mid];
            }
            if(mid%2 == 0){
                if(a[mid-1]==a[mid]){
                    end = mid-1;
                }
                else{
                    st = mid+1;

                }
            }
            else{
                  if(a[mid-1]==a[mid]){
                    st = mid+1;
                }
                else{
                    end = mid-1;
                }
            }
        }
        return -1;
    }
};
*/

//question 1313
/*
vector<int> result;
    for (int i = 0; i < nums.size(); i += 2) {
        int freq = nums[i];
        int val = nums[i + 1];
        for (int j = 0; j < freq; j++) {
            result.push_back(val);
        }
    }
    return result;
*/

//leetcode : 643

class Solution {
public:
    double findMaxAverage(vector<int>& nums, int k) {
        int n =  nums.size();
        double windowsum = 0;
        for(int i =0; i< k ; i++){
            windowsum += nums[i];
        }

        double max = windowsum;
        for(int i = k ; i<n; i++){
            windowsum += nums[i];
            windowsum -=nums[i-k];
            if(windowsum > max){
                max = windowsum;
            }
        }
        return max/k;

    }
};

//leetcode : 219

class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        unordered_set<int> window;
        int left = 0;
        for(int right =0 ; right < nums.size();i++){
            if(window.count(nums[i])){
                return true;
            }

            window.insert(nums[i]);

            if(window.size()>k){
                window.erase(nums[i-k]);
            }
        }
        return false;
    }
};

// leetcode : 3

class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<int> freq(256,0);

        int n = s.size();
        int left =0;
        int maxlen = 0;
        
        for(int right =0 ; right< n ; right++){
            char ch = s[right];
            freq[ch]++;
          while(freq[ch]>1){
            char leftch = s[left];
            freq[leftch]--;
            left++;
          }

          int curlen = right - left +1;
          if(curlen > maxlen){
            maxlen = curlen;
          }
        }
    return maxlen;
    }
};

//leetcode 209
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int n = nums.size();
        long long sum = 0;
        int left =0;
        int minlen = INT_MAX;

        for(int right =0; right<n; right++ ){
            sum += nums[right];

            while(sum >= target){
                int curlen = right - left + 1;
                if( curlen < minlen ){
                    minlen = curlen;
                }

                sum -= nums[left];
                left++;
            }
        }
        if(minlen == INT_MAX) return 0;
        return minlen;

    }
};
