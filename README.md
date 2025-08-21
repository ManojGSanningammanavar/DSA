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
