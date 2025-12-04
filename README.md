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

//leetcode 303

class NumArray {
public:
    vector<long long> prefix;
    NumArray(vector<int>& nums) {
        int n = nums.size();
       
        prefix.resize(n+1);
        prefix[0]=0;
        for(int i =0; i< n; i++){
            prefix[i+1]= prefix[i]+nums[i];
        }
        // return prefix;
    }
    
    int sumRange(int left, int right) {
        return prefix[right+1]-prefix[left];
    }
};

//leetcode 1590
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int minSubarray(vector<int>& nums, int p) {
        long long total = 0;
        for (int x : nums) total += x;

        int rem = total % p;
        if (rem == 0) return 0;  // already divisible, no need to remove anything

        int n = nums.size();
        unordered_map<int, int> lastPos;  // prefixMod -> last index
        long long prefix = 0;
        int ans = n;

        // prefix before starting = 0 at index -1
        lastPos[0] = -1;

        for (int i = 0; i < n; i++) {
            prefix = (prefix + nums[i]) % p;
            int cur = (int)prefix;

            // We need prev such that (cur - prev) % p == rem
            // => prev = (cur - rem + p) % p
            int need = (cur - rem + p) % p;

            if (lastPos.find(need) != lastPos.end()) {
                int j = lastPos[need];      // index of that prefix
                int len = i - j;            // subarray (j+1 ... i)
                ans = min(ans, len);
            }

            // store/overwrite last index for current prefix mod
            lastPos[cur] = i;
        }

        return ans == n ? -1 : ans;
    }
};

//Leetcode - 3625
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    long long countTrapezoids(vector<vector<int>>& points) {
        int n = points.size();

        // cntLine[k][b] = how many segments lie on line y = kx + b (or x = b if vertical)
        unordered_map<double, unordered_map<double, int>> cntLine;

        // cntMid[p][k] = how many segments have midpoint encoded as p and slope k
        unordered_map<long long, unordered_map<double, int>> cntMid;

        cntLine.reserve(n * n);
        cntMid.reserve(n * n);

        for (int i = 0; i < n; ++i) {
            int x1 = points[i][0];
            int y1 = points[i][1];
            for (int j = 0; j < i; ++j) {
                int x2 = points[j][0];
                int y2 = points[j][1];

                int dx = x2 - x1;
                int dy = y2 - y1;

                // --- 1) Slope & intercept for the supporting line ---
                double k, b;
                if (dx == 0) {
                    // vertical line: use special slope value, intercept = x
                    k = 1e9;
                    b = x1;
                } else {
                    k = (double)dy / dx;
                    // b = y1 - k * x1, but written to reduce precision issues
                    long long num = 1LL * y1 * dx - 1LL * x1 * dy;
                    b = (double)num / dx;
                }

                // normalize -0.0 to 0.0 to avoid separate buckets
                if (k == -0.0) k = 0.0;
                if (b == -0.0) b = 0.0;

                cntLine[k][b]++;

                // --- 2) Midpoint encoding for parallelogram counting ---
                int mx = x1 + x2;  // in [-2000, 2000]
                int my = y1 + y2;  // in [-2000, 2000]
                // shift to non-negative and pack into one 64-bit key
                long long key = (long long)(mx + 2000) * 4001 + (my + 2000);
                cntMid[key][k]++;
            }
        }

        long long ans = 0;

        // (A) Count all pairs of parallel segments on different lines
        for (auto &entry : cntLine) {
            auto &byIntercept = entry.second;
            long long prefix = 0;
            for (auto &p : byIntercept) {
                long long t = p.second;
                ans += prefix * t; // pairs between previous lines and this line
                prefix += t;
            }
        }

        // (B) Subtract parallelograms (each was counted twice above)
        for (auto &entry : cntMid) {
            auto &bySlope = entry.second;
            long long prefix = 0;
            for (auto &p : bySlope) {
                long long c = p.second;
                ans -= prefix * c; // each such pair is one parallelogram
                prefix += c;
            }
        }

        return ans;
    }
};


// Leetcode - 61
class Solution {

public:
    ListNode* FindNth(ListNode* temp , int k ){
        int ct = 1;
        while(temp!=NULL){
            if(ct==k) return temp;
            temp = temp->next;
            ct++;
        }
        return temp;
    }
public:


    ListNode* rotateRight(ListNode* head, int k) {
        ListNode* tail = head;
        int len = 1;
        if(head==NULL || k ==0) return head;
        while(tail->next!=NULL){
            tail = tail->next;
            len+=1;

        }

        if(k%len ==  0) return head;

        k= k % len;

        tail->next = head;

        ListNode* newlastnode = FindNth(head, len-k);

        head = newlastnode->next;
        newlastnode->next = NULL;

        return head;
    }
    
};
