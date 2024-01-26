# -lamprostechTestShashank-Didwania
#include<bits/stdc++.h>
using namespace std;

//printing LIS
void printLIS(vector<int>& arr) {
    for (int x : arr)
        cout << x << " ";
    cout << endl;
}


// Function to form and print LIS
void solve(int arr[], int n) {
    
    vector<vector<int>> L(n);

    // L[0] is equal to arr[0]
    L[0].push_back(arr[0]);

    //dp starting from here index1
    for (int i = 1; i < n; i++) {
        //checking all the LIS ending ending at all the precious indices
        for (int j = 0; j < i; j++) {
            // If arr[i] is greater than arr[j]
            // and the LIS ending at j is longer by at least 1 element than the LIS ending at i
            if ((arr[i] > arr[j]) && (L[i].size() < L[j].size() + 1))
                L[i] = L[j];
        }

        // L[i] ends with arr[i]
        L[i].push_back(arr[i]);
    }

    vector<int> max = L[0];

    // LIS will be max of all increasing sub-sequences of arr
    for (vector<int> x : L)
        if (x.size() > max.size())
            max = x;

    // max will contain LIS
    printLIS(max);
}

int main() {
    int arr[] = {10, 22, 9, 33, 5, 44};
    int n = sizeof(arr) / sizeof(arr[0]);

    solve(arr, n);

    return 0;
}

Q2. it would also be solved using dp
creating a dp table of (m+1) * (n+1) dimension where m and n are lengths of the strings
dp[i][j] will showcase the min distnce between the first 'i' charcters of first string and 'j' charcaters of second string
iterating though the table
if it matches the set dp[i][j] = dp[i-1][j-1].
